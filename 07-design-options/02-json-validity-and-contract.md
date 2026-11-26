# What makes JSON valid for the platform?

This was raised as an open question in the conversation.

## Level 1 — syntactic validity

The text is parseable JSON: valid objects, arrays, strings, numbers, booleans, and null values.

## Level 2 — structural validity

The JSON follows a known node model: expected properties, child arrays, attribute representation, and supported node relationships.

## Level 3 — semantic validity

The structure has recognized meaning for the platform. For example, a table base has identifiable semantic regions such as `table-header-row`, `table-body`, and `table-footer-row`.

## Level 4 — executable validity

The required definition, instruction keys, spec templates, source paths, destination paths, and actions exist and are compatible. A syntactically and structurally valid JSON document may still fail at execution if a referenced instruction/template/path is missing.

## Recommendation

Document these as separate validation layers. Avoid calling all four simply “valid JSON.” A future formal contract could distinguish parse validation, schema validation, semantic validation, and instruction preflight validation.
