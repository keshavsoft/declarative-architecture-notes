# Discussion claims versus source evidence

| Statement | Classification | Notes |
|---|---|---|
| Base is meaning/stable structure, not code | Discussed principle | Explicitly stated by the user |
| External changes should be represented as data | Discussed principle | Examples: data, files/collections, columns, tags, options |
| JSON is preferred over HTML as the source representation | Discussed principle | HTML is viewed as one presentation method |
| DOM tree inspired the JSON model | Discussed principle | User studied the DOM representation and adapted the idea |
| Header and body use separate construction logic | Discussed principle + source support | `buildHeader`/`buildFooter` are single collection instructions; `buildBody` is rowOnColumn |
| Two practical row/column strategies exist | Discussed principle | Comparative evaluation remains open |
| V20 shares one mutable base through the sequence | Verified in ZIP | `state = { base, data }`; same state is passed through sequence |
| JSONPath identifies write target | Verified in ZIP | `json-write-path` V6 uses JSONPathly when `jsonPath` supplied |
| `filePath` identifies property/parent | Verified in ZIP | `resolveParent.js` resolves parent and final key |
| Action performs mutation | Verified in ZIP | `writePath` selects action registry entry or default set |
| `findByRole` is completely unused | Not supported | V6 still has a `dataRole` fallback |
| Options feature has four steps | Verified in ZIP | `options-show-button` array in instructions V2 |
| Serial feature has four steps | Verified in ZIP | `serial` array in instructions V2 |
| Data changes trigger incremental update | Open question | Not established by the source review |
| JSON syntax alone is enough for validity | Not established | Formal system contract remains open |
