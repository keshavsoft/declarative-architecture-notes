# Source map for claims in this repository

All paths below are relative to `25-1/table/` in the supplied ZIP.

| Topic | Source file | What it supports |
|---|---|---|
| Package versions | Each package's `package.json` | Snapshot package versions |
| Runner entry | `json-renderers-run-instructions/src/v20/index.js` | Definition lookup, base clone, option steps, sequence assembly |
| Sequence execution | `json-renderers-run-instructions/src/v20/instructions/index.js` | Shared state and ordered execution |
| Build dispatch | `json-renderers-run-instructions/src/v20/instructions/executeBuildInstruction.js` | `single`, `rowOnColumn`, `columnOnRow` dispatch |
| Write bundle | `json-renderers-run-instructions/src/v20/instructions/executeWriteBundle.js` | Ordered mutation steps, skipIf, template lookup |
| Destination existence | `json-renderers-run-instructions/src/v20/instructions/writeResult.js` | JSONPath destination check and result writing |
| Source resolution | `json-renderers-run-instructions/src/v20/instructions/resolveSource.js` | Source JSONPath/filePath resolution |
| Options normalization | `json-renderers-run-instructions/src/v20/runOptions/normalizeOptions.js` | Modern options and legacy show* aliases |
| Feature keys | `json-renderers-run-instructions/src/v20/runOptions/resolveFeatureKeys.js` | Feature-to-instruction mapping |
| Table renderer | `json-renderers-build-table/src/v58/index.js` | Config parsing, options normalization, runner call, JSON-to-DOM |
| Instruction definitions | `declarative-instructions/src/v2/instructions.json` | Table, serial, options, select, data-list instruction declarations |
| Destination resolution | `json-write-path/src/v6/resolveParent.js` | JSONPath selection, legacy dataRole fallback, filePath parent/key |
| Mutation dispatch | `json-write-path/src/v6/index.js` | Action selection and invocation |
| Row-aware actions | `json-write-path/src/v4/actions/rows.js` | pushToRows, unshiftToRows, unshiftSerialToRows |

## Evidence handling

When citing a code fact in future work, reopen the relevant file from the repository snapshot or the user's current source tree. Do not treat this documentation as a substitute for the code if the repository has changed.
