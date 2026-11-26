# Executive overview

## The central idea

The architecture is moving toward a **JSON-first, declarative, instruction-driven construction model**. Information and requirements are described as structured data. A stable semantic base is prepared, and ordered instructions apply transformations or mutations to that base to produce a presentation structure.

The table is an example used to explain the architecture; it is not the limit of the architecture. HTML is one possible presentation output. The user's preference is to describe information in JSON and use a capable tool to turn a valid, understood JSON representation into a suitable presentation, such as a table, list, select, or other UI structure.

## Main conceptual layers

1. **Information/data** — the records and values to be represented.
2. **JSON representation** — a structured description of nodes, properties, and child relationships.
3. **Base** — the stable semantic skeleton for a component; it is not the code and should not contain every variable external requirement.
4. **Changes/options** — external and variable requirements represented as data: collections, files, columns, tags, and requested features.
5. **Instructions** — ordered declarative steps that describe construction or mutation work.
6. **Transformations/actions** — reusable operations that create values from data or mutate an existing JSON tree.
7. **Output/presentation** — the resulting structure, which may then be converted to browser DOM.

## Key architectural statement

> The base is not the code. The base is the meaning.

The base expresses the stable meaning and structure of a component. Variable requirements are supplied separately and applied through instructions.

## Current maturity

The supplied source snapshot already contains a working instruction runner, table instructions, JSONPath-based destination selection, mutation actions, and a table renderer. Some ideas discussed—especially the full comparative evaluation of `rowOnColumn` versus `columnOnRow`, and the future lifecycle for changing data—remain open design topics rather than completed conclusions.
