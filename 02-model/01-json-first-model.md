# JSON-first model

## Inspiration

The user was inspired by the HTML DOM's clean tree pattern and JavaScript's representation of elements as objects with properties and child nodes. They studied the DOM model and explored representing a similar structure in JSON. The user reports that this approach worked for their use case.

## Node model

The discussion named familiar structural nodes:

- table
- thead
- tbody
- tr
- th
- td

The header and body are separate branches. Each can contain its own row node(s), and those rows contain their cells. A node's properties and child relationships are represented in JSON.

This is a conceptual description, not a complete formal schema. The exact JSON schema, required properties, allowed child types, and validation rules should be taken from the declarative specification repositories and documented separately.

## Presentation independence

The desired direction is:

`information → JSON representation → construction/transformation → presentation`

A table is one presentation. Other presentations may include a list, data list, select, or other UI. The same underlying information should not have to be defined in HTML-specific terms.

## What “valid JSON” means remains to be formalized

At minimum, there are two different notions:

1. **JSON syntax validity:** the text parses as JSON.
2. **System/model validity:** the parsed object follows the expected node/specification conventions and can be interpreted by the relevant definitions and instructions.

The second contract is essential. The user asked whether “valid JSON” means syntax alone or a particular structure; that question was posed but not yet answered in the discussion.
