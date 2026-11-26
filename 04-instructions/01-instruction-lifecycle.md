# Instruction lifecycle

## Conceptual lifecycle

1. Resolve which component definition is requested.
2. Obtain the component's base specification.
3. Clone the base so a run starts with its own mutable tree.
4. Resolve caller options into ordered instruction keys.
5. Combine the definition's required instructions with option-driven instructions.
6. Execute each instruction or instruction bundle in order.
7. Return the mutated base.
8. Convert the JSON specification into browser DOM when the caller uses the table renderer.

## Verified V20 implementation

Source: `json-renderers-run-instructions/src/v20/index.js`.

The entry point imports:
- `declarative-definitions`
- `declarative-instructions`
- `declarative-spec`
- option resolution
- instruction sequence execution
- global registration

It looks up `definitions[instructionMainKey]?.[instructionSubKey]`, obtains `spec[definition.baseFromSpec]`, clones it with `structuredClone`, resolves option steps, builds an ordered sequence, and calls `runInstructionSequence`.

## Shared state

Source: `src/v20/instructions/index.js`.

The sequence runner creates:

```js
const state = { base, data };
```

It loops over the sequence in order. An instruction value that is an array is treated as a write bundle; otherwise it is dispatched as a build instruction. The same `state.base` is returned after all steps.

This confirms that instructions in one run share and progressively mutate the same base object.

## Build instruction types

Source: `src/v20/instructions/executeBuildInstruction.js`.

- `single`: resolve a source, obtain one template, then either apply a primitive template transformation or map a collection into the template.
- `rowOnColumn`: invoke the two-dimensional row-on-column transformation with columns, data, column spec, and row spec.
- `columnOnRow`: invoke the two-dimensional column-on-row transformation with the same categories of inputs.

After a result is generated, `writeResult` writes it to the destination.

## Write bundles

Source: `src/v20/instructions/executeWriteBundle.js`.

A bundle is an ordered array of write steps. For each step, the runner:
- checks an optional `skipIf` JSONPath condition;
- checks whether the destination exists;
- looks up the named template in the spec;
- clones the template;
- calls `writePath` with the shared state, destination path, and template.

This is the mechanism used by multi-step features such as serial and options columns.

## Options resolution

V20 normalizes modern grouped options and legacy `show*` shorthand, resolves each feature to instruction keys, preserves order, and deduplicates instruction keys. For a boolean `true`, it can include the feature's `set-<feature>` bundle and matching `<feature>-...` switches. For an object, enabled switches are converted to kebab-case instruction keys.

The table renderer V58 also performs a compatibility normalization for `showSearch`, `showSerial`, and `showOptions` before passing options to the instruction runner.
