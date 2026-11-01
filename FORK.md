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
`Opis\JsonSchema`. A root declares the repository and requires a branch:

```json
"repositories": [{"type": "vcs", "url": "https://github.com/min-0-max/json-schema", "no-api": true}],
"require": {"min-0-max/json-schema": "dev-polyspec-origin-2.6.0"}
```

A library requires `"min-0-max/json-schema": "*"` in place of
`opis/json-schema`. The tag `v2.6.0-p1` predates the rename and keeps
the name `opis/json-schema`.

The branch `polyspec-origin-2.6.0` is the default branch and carries the
upstream version it is based on in its name; `master` follows upstream
and keeps the name `opis/json-schema`. A rebase onto a newer upstream
version gets a new branch `polyspec-origin-<version>`, which roots then
require as `dev-polyspec-origin-<version>`.
