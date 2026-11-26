# findByRole and JSONPathly: migration status

## Historical context from the discussion

The user explained that `findByRole` originated in an earlier period, around the initial JSONPath/JSONPathly work. It was used as a practical way to find a node by role before the more general JSONPath approach became the preferred selection mechanism.

## Current source fact

`json-write-path/src/v6/resolveParent.js` still imports `findByRole` from `json-transformer-funcs` and calls it only when `path.dataRole` is supplied and `path.jsonPath` is absent.

When `path.jsonPath` is supplied, the resolver uses `query(root, path.jsonPath, { returnArray: true })` and enforces exactly one match.

## Correct status wording

The safest description is:

> JSONPathly is the primary destination-selection mechanism for JSONPath-based instructions. `findByRole` remains as a backward-compatibility path for `dataRole` destinations in `json-write-path` V6.

Do not say that `findByRole` is completely unused or that `json-transformer-funcs` can immediately be removed. The fallback proves a current dependency path exists.

## Migration recommendation

Before deprecating the aggregate `json-transformer-funcs` package:

1. Search all active packages for imports from `json-transformer-funcs`.
2. Search instruction/configuration data for `dataRole` destinations.
3. Identify whether external consumers rely on the legacy path.
4. Decide whether to migrate those destinations to JSONPath.
5. Add tests for JSONPath destination selection and legacy behavior (or intentional rejection).
6. Remove the import and package dependency only after no supported consumer remains.
7. Keep historical versions intact if versioned examples are expected to remain reproducible.

## Do not confuse the aggregate package with the focused transformation packages

The conversation's recommendation was to review the older aggregate `json-transformer-funcs` package, not to discontinue the focused primitive, one-dimensional, or two-dimensional transformation packages. Those focused packages are imported directly by the V20 instruction runner.
