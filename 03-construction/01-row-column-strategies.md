# Two row/column construction strategies

The discussion identified two practical ways to construct a table's row/cell structure. Neither was declared universally better.

## Strategy A — row-first nested construction (`rowOnColumn` as discussed)

Concept:

1. Iterate the data rows.
2. Create a TR for the current row.
3. Inside that row, iterate the columns.
4. Create each cell and append it to the current TR.
5. Append the completed TR to the relevant row container.

Illustrative pseudocode:

```js
for (const record of records) {
  const tr = buildRow(record);
  for (const column of columns) {
    tr.children.push(buildCell(record, column));
  }
  tbody.children.push(tr);
}
```

This approach naturally creates one row and fills it before moving to the next row.

## Strategy B — two-phase construction (`columnOnRow` as discussed)

Concept:

1. First create the required rows.
2. Keep the created rows available.
3. In a separate phase, iterate columns.
4. For each column, visit the appropriate existing rows and insert the corresponding cell.

Illustrative pseudocode only:

```js
const rows = buildRows(records);
for (const column of columns) {
  for (const row of rows) {
    row.children.push(buildCell(row, column));
  }
}
```

The user described this as an alternative that had not been fully explored. It may be useful where rows are established first and columns are applied afterward.

## Header and body are not necessarily the same operation

The user clarified that header and body have separate construction logic. It is not accurate to assume that all rows across head, body, and footer are built as one homogeneous collection.

## What the current ZIP verifies

In `declarative-instructions/src/v2/instructions.json`:

- `buildHeader` is a `single` instruction using `fromCollection` over `$.columns`.
- `buildFooter` is also a `single` instruction using `fromCollection` over `$.columns`.
- `buildBody` is declared as `rowOnColumn`, with `buildBodyTr` and `buildBodyCell` templates.
- `buildSelectWithOptions` and `buildDataListWithOptions` are declared as `columnOnRow`.

The runner's V20 implementation dispatches `rowOnColumn` and `columnOnRow` to separate functions from `json-transformer-funcs-two-dimensions`.

**Caution:** the current source confirms that both instruction types are supported and where they are used. It does not, by itself, establish that the user's conceptual Strategy B is fully explored or preferable for table construction. The implementation details of the two-dimensional package should be inspected before making a stronger claim.

## Decision status

No winner has been selected. Preserve both strategies as valid design alternatives pending explicit tests and comparison of ordering, data mapping, performance, and ease of expressing header/body/footer behavior.
