# Core principles captured from the discussion

## 1. JSON-first, not HTML-first

**Discussed principle:** HTML is a presentation mechanism, not the whole source of truth. The user prefers JSON because it is a widely accepted structured data format and can describe information independently of one presentation. A table should be an output, not necessarily the canonical description of the information.

**Important qualification:** syntactically valid JSON is not automatically meaningful to this system. A consumer needs a recognized shape, semantic conventions, specifications, and instructions. The precise validation contract remains to be documented.

## 2. Stable base plus variable changes

**Discussed principle:** distinguish a stable base from changes. The base represents meaning and stable structure, not implementation code. External or changing requirements should be represented as data and applied to the base.

Examples of changing inputs mentioned:
- data collections;
- file collections;
- columns;
- tags;
- options/features.

## 3. Instructions are declarative steps

Instructions describe what should be done, where it should happen, and which reusable template/transformation/action participates. Instructions can be individual steps or ordered bundles.

## 4. Mutation is central after the skeleton exists

**Discussed principle:** avoid repeatedly constructing independent internal pieces when a stable base already exists. Establish the skeleton (for the table example, table/head/body and relevant rows), then apply steps that mutate the existing structure.

An instruction may insert a row; a later instruction may append a label or input into that already-inserted row. The steps rely on the structure produced by earlier steps.

## 5. Construction and mutation are not identical

Some instructions generate structures from collections/templates. Other instructions take a ready-made template and mutate an existing destination. The system supports both kinds of work.

## 6. The table is an example, not the boundary

The user said other data presentations—data lists, selects, and related forms—are already covered in the existing ecosystem. The current discussion should not assume the platform is only a table builder.
