# How mutations locate and change a destination

## The three responsibilities

1. **Selection:** find the target node in the JSON tree.
2. **Path resolution:** identify the property/array on that target where the write belongs.
3. **Action:** perform the requested mutation, such as set, push, unshift, or a row-aware custom operation.

Selection and insertion-parent resolution are related but not identical. For example, selecting a `tbody` does not mean a new `td` belongs directly under `tbody`; the cell belongs under a particular `tr`, or under each applicable row.

## Verified write-path V6

Source: `json-write-path/src/v6/resolveParent.js`.

The resolver:
- obtains the registry entry named by `path.fileName`;
- if `path.jsonPath` exists, queries that root using JSONPathly;
- requires exactly one match (throws on zero or multiple matches);
- otherwise, if `path.dataRole` exists, uses `findByRole` as a backward-compatibility fallback;
- takes the final segment of `filePath` as the property key;
- resolves the preceding segments to the parent object;
- returns `{ parent, key, target }`.

Source: `json-write-path/src/v6/index.js`.

The writer resolves the parent, selects `actions[path.action]` or defaults to `set`, invokes the action, and returns the registry.

## JSONPathly versus findByRole

The current V6 resolver imports both:

```js
import { query } from "jsonpathly";
import { findByRole } from "json-transformer-funcs";
```

JSONPath is used when `path.jsonPath` is present. `findByRole` is only used in the `else if (path.dataRole)` compatibility branch.

Therefore:
- JSONPathly is the active selection path for JSONPath-based destinations.
- `findByRole` remains in the active package dependency graph because the fallback still exists.
- If every active caller uses `jsonPath`, that fallback may be unused at runtime for those calls, but it is not safe to remove the dependency without checking all callers and supported legacy path formats.

## Important distinction: one target versus many rows

V6 `resolveParent` requires one JSONPath match. Row-aware actions can then mutate multiple row objects inside the selected target's child collection. This is a useful design: JSONPath selects the container once; the action performs the per-row operation.

## Row-aware actions

Source: `json-write-path/src/v4/actions/rows.js`.

- `pushToRows(parent, key, value)`: for every row in `parent[key]`, clone the supplied value(s) and append them to `row.children`.
- `unshiftToRows(parent, key, value)`: same pattern, inserting at the beginning.
- `unshiftSerialToRows(parent, key, value)`: clone the value for each row, set `textContent` to `rowIndex + 1`, and prepend it to that row's children.

These actions explain how a selected body container can be the destination for an operation that inserts a cell into every TR under it.
