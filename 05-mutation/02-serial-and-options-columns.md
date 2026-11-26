# Serial and options columns

This document records the actual instruction bundles found in `declarative-instructions/src/v2/instructions.json`.

## Serial feature

The `serial` bundle contains four ordered steps:

| Order | Narration / purpose | JSONPath target | Action | Template |
|---:|---|---|---|---|
| 1 | Prepend serial column width | `table-colgroup` | `unshift` | `colGroupForSerial` |
| 2 | Prepend serial header cell | `table-header-row` | `unshift` | `headerSerialCell` |
| 3 | Prepend serial cell into each body row | `table-body` | `unshiftSerialToRows` | `buildBodyCell` |
| 4 | Prepend serial footer cell | `table-footer-row` | `unshift` | `headerSerialCell` |

The custom body action assigns sequential text using the zero-based row index plus one.

There is also a split pair of instruction keys, `set-serial` and `serial-show-serial`. In the supplied V2 instruction file, `set-serial` includes the colgroup/header/footer setup, while `serial-show-serial` inserts the serial cells into body rows. The feature resolver can combine a `set-<feature>` bundle with matching feature switch instructions.

## Options feature

The `options-show-button` bundle contains four ordered steps:

| Order | Purpose | JSONPath target | Action | Template |
|---:|---|---|---|---|
| 1 | Append options column width | `table-colgroup` | `push` | `colGroupForOption` |
| 2 | Append options header cell | `table-header-row` | `push` | `headerForOption` |
| 3 | Append options button cell to every body row | `table-body` | `pushToRows` | `optionsButtonCell` |
| 4 | Append options footer cell | `table-footer-row` | `push` | `tdWithButtonSaveWarning` |

The body step selects the body container once and delegates insertion into each row to `pushToRows`.

## Edit and delete switches

The V2 instruction file also contains `options-show-edit-button` and `options-show-delete-button`. Each follows the same four-region pattern:
- append the relevant colgroup width;
- append a header cell;
- append a button cell to each body row using `pushToRows`;
- append a footer cell (the supplied definitions use `emptyCell` for these footer entries).

## Architectural significance

The feature is not implemented as one monolithic “build options column” function. It is an ordered bundle of smaller mutations across the table's structural regions. The instruction describes each step; the reusable action knows how to apply a template to every row in the selected body.

## Caveat

The documentation records the supplied V2 instruction definitions and V20 execution path. Runtime behavior also depends on the matching specification templates, action registry, and package versions. This source review did not execute the complete browser output for every feature combination.
