# Rebuild versus incremental update

A question was raised about what should happen when the data changes after the table has already been constructed.

## Option A — rebuild from the base

- Keep or retrieve the original clean base specification.
- Supply the latest data and options.
- Clone the base.
- Execute the same instruction sequence again.
- Replace or re-render the previous output.

Potential strengths: deterministic construction, simpler state reasoning, fewer stale-node risks.

Potential costs: repeated work and potentially more DOM replacement than necessary.

## Option B — incrementally mutate the existing structure

- Compare old and new data.
- Identify changed, added, and removed records/cells.
- Select affected nodes.
- Apply only the necessary mutations.

Potential strengths: less work for small changes and potential preservation of UI state.

Potential costs: more complex reconciliation, identity/key requirements, ordering issues, and risk of stale or duplicated nodes.

## Status

No choice was made in the conversation. The current instruction engine's mutations during initial construction do not prove that it has a complete incremental update/reconciliation model.

## Recommendation for a future decision

First establish whether the current product requirement needs incremental updates. If not, rebuilding from a clean base is a simpler baseline. If incremental updates become necessary, define stable record identity and reconciliation semantics before implementing them.
