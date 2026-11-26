# Declarative Architecture — Discussion Notes & Source Review

A standalone documentation repository capturing the architectural discussion about KeshavSoft's JSON-first, instruction-driven construction system, together with a source-grounded review of the supplied `25-1.zip` snapshot.

> **Purpose:** preserve the ideas, implementation facts, distinctions, unresolved questions, and next discussion points. This repository documents and analyzes; it does not modify or replace any source package.

## Start here

1. [Executive overview](01-foundation/01-executive-overview.md)
2. [Core principles](01-foundation/02-core-principles.md)
3. [JSON as the representation](02-model/01-json-first-model.md)
4. [Base, changes, and construction](02-model/02-base-changes-construction.md)
5. [Two table construction strategies](03-construction/01-row-column-strategies.md)
6. [Instruction execution model](04-instructions/01-instruction-lifecycle.md)
7. [Mutation and destination resolution](05-mutation/01-how-mutations-work.md)
8. [Serial and options columns](05-mutation/02-serial-and-options-columns.md)
9. [Source review findings](06-codebase-review/01-verified-findings.md)
10. [Open questions and next discussion](08-open-questions/01-open-questions.md)

## Evidence labels

Throughout the documents:

- **Discussed principle** — explicitly explained by the user in the conversation.
- **Verified in ZIP** — confirmed by inspecting files in the supplied `25-1.zip` snapshot.
- **Interpretation** — a reasoned explanation connecting discussion and source; not itself a source fact.
- **Open question** — not yet established; must not be presented as settled.
- **Recommendation** — a proposed next step, not a claim about existing behavior.

## Scope and limitations

The conversation primarily covered the `table/` ecosystem. The source review therefore concentrates on the declarative packages, instruction runner, JSONPath selection, JSON write-path mutations, and table renderer. It does not claim that every package, sample, historical version, or runtime path in the 39 MB ZIP has been exhaustively executed. The findings are static source inspection, not a complete integration test.

The documentation deliberately preserves uncertainty. In particular, the discussion introduced two conceptual row/column construction strategies, but the current code's actual behavior must be described from the relevant instruction types and implementations rather than assuming both strategies are equally used by the table builder.
