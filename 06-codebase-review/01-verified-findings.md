# Verified source findings from `25-1.zip`

## Snapshot package versions

The following versions were read from package.json files in the extracted ZIP:

| Package | Version |
|---|---:|
| `json-renderers-run-instructions` | 1.20.1 |
| `json-write-path` | 1.6.1 |
| `declarative-instructions` | 1.2.3 |
| `declarative-definitions` | 1.3.1 |
| `declarative-spec` | 1.4.1 |
| `jsonpathly` | 4.0.0 |
| `json-transformer-funcs` | 1.24.8 |
| `json-transformer-funcs-primitive` | 1.10.3 |
| `json-transformer-funcs-one-dimension` | 1.9.9 |
| `json-transformer-funcs-two-dimensions` | Not independently confirmed in this review table |
| `json-renderers-build-table` | 1.58.1 |

## Runner

`json-renderers-run-instructions/src/v20/index.js`:
- resolves a component definition;
- loads and clones its base spec;
- resolves option-driven steps;
- combines definition instructions and option instructions;
- runs the sequence and returns the mutated base.

`src/v20/instructions/index.js` creates shared `{ base, data }` state and executes steps in order. Arrays are write bundles; other entries are build instructions.

## Build instruction dispatch

`src/v20/instructions/executeBuildInstruction.js` imports:
- `json-transformer-funcs-primitive` as `applyTemplate`;
- `json-transformer-funcs-one-dimension` as `fromCollection`;
- `rowOnColumn` and `columnOnRow` from `json-transformer-funcs-two-dimensions`.

It supports `single`, `rowOnColumn`, and `columnOnRow` instruction types.

## Table renderer V58

`json-renderers-build-table/src/v58/index.js`:
- guards the config;
- parses `config.type` into main/sub instruction keys;
- normalizes legacy options such as `showSearch`, `showSerial`, and `showOptions`;
- calls the instruction runner with `data` and `columns`;
- converts the resulting JSON spec using `@keshavsoft/json-to-dom`.

## Legacy findByRole fallback

`json-write-path/src/v6/resolveParent.js` uses JSONPathly for `jsonPath` and `findByRole` for the legacy `dataRole` branch. Therefore the older helper is not fully removed from the current V6 implementation.

## Scope of confidence

These are static source findings from the supplied ZIP. They establish imports, control flow, declared instruction bundles, and action code. They do not establish full runtime correctness, browser rendering in every configuration, or the absence of consumers in all packages and historical versions.
