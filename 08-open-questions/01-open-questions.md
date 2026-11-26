# Open questions and next discussion

These questions were not fully answered in the conversation. They are intentionally left open.

## A. JSON model and meaning

1. What exact JSON shape is considered a valid node in the platform?
2. Which properties are universal node properties, and which are element-specific?
3. Is the JSON model intended to represent only DOM-like output nodes, or broader application meaning as well?
4. What is the boundary between semantic base and presentation-specific spec?

## B. Base and external changes

5. Which parts of a component must always exist in the base?
6. Which features must always be external data/options?
7. Can a base be shared by multiple presentation renderers?
8. Is the base immutable after cloning, or is mutation the intended normal execution model?

## C. Construction strategies

9. What are the exact semantics of `rowOnColumn` and `columnOnRow` in the two-dimensional package?
10. Which strategy is best for table body construction, and under what conditions?
11. How should header, body, and footer construction differ?
12. Can a single column-oriented instruction consistently handle header, body, and footer, or should these remain distinct steps?

## D. Instruction and mutation model

13. What is the formal contract for an instruction: type, sourcePath, destinationPath, templateKey, func, action, skipIf, narration?
14. Should instructions be declarative only, or may an action contain specialized imperative behavior?
15. How are ordering dependencies represented and validated?
16. Should every destination JSONPath resolve to exactly one node, or should some instruction types explicitly support many matches?
17. Should row-aware actions remain custom write-path actions, or become first-class instruction types?

## E. Runtime lifecycle

18. When data changes, should the system rebuild from the original base or incrementally reconcile the existing tree?
19. How should stable row identity be represented?
20. How should sorting, filtering, pagination, and row insertion interact with serial numbers?
21. How should mutations preserve UI state and event bindings when DOM is re-rendered?

## F. Compatibility and package lifecycle

22. Can all active `dataRole` destinations be migrated to JSONPath?
23. Is `findByRole` still required for any supported consumer?
24. Which focused transformation packages are current public contracts?
25. What is the compatibility matrix among definitions, instructions, spec, runner, write-path, and renderer versions?
26. Which historical versions are supported, and which are archival only?

## Suggested next discussion

The most useful next topic is the formal meaning of the JSON node model and the boundary between semantic base and presentation spec. This follows naturally from the user's JSON-first philosophy and avoids prematurely optimizing individual table operations.
