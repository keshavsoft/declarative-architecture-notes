# Glossary

| Term | Meaning in these notes |
|---|---|
| Base | Stable semantic structure from which a component run begins. Not source code. |
| Change | External or variable requirement supplied as data/options. |
| JSON node | An object representing a node in the JSON tree, with properties and possibly children. |
| Spec | Repository/package of reusable base structures and templates used by instructions. |
| Definition | Component-level declaration that selects a base spec and required instructions. |
| Instruction | Declarative unit describing a build or write/mutation step. |
| Instruction bundle | Ordered array of write steps grouped under one instruction key. |
| Template | Reusable JSON fragment used to create or insert a structure. |
| Selection | Finding a node in a JSON tree, here commonly with JSONPathly. |
| Destination path | The selected target plus a property path describing where the write occurs. |
| Mutation action | Operation such as set, push, unshift, or row-aware insertion. |
| `rowOnColumn` | Instruction type dispatched to the two-dimensional transformation package. |
| `columnOnRow` | Instruction type dispatched to the two-dimensional transformation package. |
| `findByRole` | Legacy role-based node lookup retained as a `dataRole` fallback in write-path V6. |
| JSONPathly | Query library used to select nodes in JSON trees. |
| DOM | Browser Document Object Model; inspiration for the tree-like JSON representation. |
| Presentation | The rendered form shown to a user, such as a table, list, or select. |
