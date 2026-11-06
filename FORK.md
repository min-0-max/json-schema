# Fork of opis/json-schema

This fork is the base that polyspec depends on; it is not assumed that
upstream accepts its fixes. Upstream is
[opis/json-schema](https://github.com/opis/json-schema).

## What it fixes

- In the collect-all-errors mode (`setStopAtFirstError(false)`, max errors
  above 1), a property that failed its `properties` subschema kept the
  keyword from recording the checked properties, so
  `additionalProperties: false` reported every property, valid ones
  included, as not allowed. A failing keyword group also stopped the later
  groups, so `unevaluatedProperties` never ran. Both keywords now report
  only the properties no keyword applies to (`tests/CollectAllErrorsTest.php`).

## How it is consumed

The package is named `min-0-max/json-schema` and keeps the namespace
`Opis\JsonSchema`. A root declares the repository and requires a release
tag of the line:

```json
"repositories": [{"type": "vcs", "url": "https://github.com/min-0-max/json-schema", "no-api": true}],
"require": {"min-0-max/json-schema": "2.6.0-p2"}
```

A library requires `"min-0-max/json-schema": "*"` in place of
`opis/json-schema`. The tag `v2.6.0-p1` predates the rename and keeps
the name `opis/json-schema`.

## Branches and tags

- `master` mirrors upstream and holds no commit of this fork.
- `min-0-max/polyspec/2.6.0-1-g85d8523` is the line, the default branch:
  upstream at `2.6.0-1-g85d8523` (the `git describe --tags` value of the
  base) with the fixes and the fork's own files.
- `min-0-max/fix/collect-checked-properties/2.6.0-1-g85d8523` holds the
  fix alone on the same base, without the fork's files.
- A release is a tag `v<upstream version>-p<n>` on the line. A newer
  upstream base gets a new line `min-0-max/polyspec/<base>`, and roots
  move to that line's tags.
