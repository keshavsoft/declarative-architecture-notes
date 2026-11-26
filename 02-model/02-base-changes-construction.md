# Base, changes, and construction

## Base

The base is the stable semantic foundation. It is not source code. It expresses what the component is and provides the fixed structural places into which later work can be applied.

For the table example, the user described the table skeleton and its major structural regions as being established before optional or data-driven mutations. The header and body have their own construction logic; the base may contain fixed structural nodes that later instructions target.

## Changes

Changes are external and variable requirements, represented as data rather than hardcoded into the base. Examples explicitly mentioned include data, files/collections, columns, tags, and options.

## Construction

Construction is the process that combines the base with the external inputs by executing the required instructions and transformations.

A useful conceptual separation is:

| Concern | Question it answers |
|---|---|
| Base | What stable semantic structure exists? |
| Input/change data | What varies for this particular use? |
| Instruction | What ordered work should happen? |
| Selection | Where in the existing JSON tree should it happen? |
| Template/transform | What value or structure should be created? |
| Mutation action | How should the destination be changed? |

## Avoid conflating base with code

A base may be serialized JSON. Instructions and functions are executable mechanisms. The base describes meaning/structure; code executes the instructions. This distinction is foundational to the user's philosophy.

## Rebuild versus incremental update

A question was raised: when data changes after a table is constructed, should the system rebuild from a clean base and rerun instructions, or incrementally mutate the existing rendered structure?

**Status: unanswered.** Do not assume the current architecture supports efficient incremental updates merely because it supports mutations during initial construction. Initial construction mutations and later data-refresh lifecycle are separate concerns.
