# Contributing

This repository contains the base CodeRabbit configuration, `coderabbit.yaml`, that other
repositories reference through `remote_config`. It holds configuration only. Consumers track
the `main` branch, so a merged change applies to them without further steps.

## Code style

`.editorconfig` and `.yamllint.yaml` define the formatting rules:

- Use UTF-8, LF line endings, 2-space indentation, and a final newline.
- Trim trailing whitespace in every file, Markdown included. `.editorconfig` exempts Markdown,
  but the `trailing-whitespace` pre-commit hook still removes it.
- Start YAML files with the `---` document marker.
- Keep lines to 120 characters or fewer.

`coderabbit.yaml` keeps its `yaml-language-server` schema comment on the second line.

## Validation

Run every check from the repository root:

```bash
pre-commit run --all-files
```

Run a single check:

```bash
yamllint --strict .
check-jsonschema --schemafile \
  'https://storage.googleapis.com/coderabbit_public_assets/schema.v2.json' \
  coderabbit.yaml
```

Schema validation does not reject unknown keys under `reviews`. Before merging a key name change,
point the `remote_config.ref` of a test consuming repository at your branch, run
`@coderabbitai configuration` on a pull request there, and confirm the setting shows the intended
value with the shared configuration as its source. A value from defaults, UI settings, or an
override does not prove that the shared key is spelled correctly. A bare `repository:` name
resolves within the consuming repository's owner, so for a branch in a fork, use a test repository
under the fork's owner and give CodeRabbit access to the fork.

## Commit convention

Commit subjects use the Conventional Commits format, for example
`feat: add validation tooling and expand path review instructions`.

## Pull requests

Open pull requests against `main`. The `Validate Configuration` workflow runs the pre-commit
hooks on every pull request and on pushes to `main`.

The `main` ruleset requires one approving review, a review from the code owner listed in
`.github/CODEOWNERS`, and resolved review threads. It allows squash merges only.

## License

This project is licensed under the [MIT License](LICENSE). Contributions fall under the same
license.
