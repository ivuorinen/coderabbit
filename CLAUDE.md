# CLAUDE.md

## Repository Purpose

Centralized CodeRabbit AI code review configuration. Contains a single `coderabbit.yaml`
referenced by other repositories via `remote_config`. No source code — configuration only.

## Validation Commands

```bash
# Run all checks (YAML lint, schema validation, editorconfig)
pre-commit run --all-files

# Individual checks
yamllint --strict .                # YAML linting
check-jsonschema --schemafile \
  'https://storage.googleapis.com/coderabbit_public_assets/schema.v2.json' \
  coderabbit.yaml                  # Schema validation
```

CI runs `pre-commit/action@v3.0.1` on push/PR to `main`.

Schema validation does not reject unknown keys under `reviews`. After changing a key name, run
`@coderabbitai configuration` on a pull request in a consuming repository and confirm the
resolved YAML contains the setting.

## Architecture

```
coderabbit.yaml          # Main config — schema.v2.json validated
.yamllint.yaml           # yamllint rules (120 char lines, strict)
.pre-commit-config.yaml  # Pre-commit hooks: check-yaml, yamllint, schema, editorconfig
.editorconfig            # 2-space indent, UTF-8, LF line endings
.github/workflows/       # CI validation via pre-commit
```

Other repos consume this config by adding to their `.coderabbit.yaml`:
```yaml
remote_config:
  repository: "coderabbit"
  ref: "main"
  path: "coderabbit.yaml"
```

## Conventions

- YAML files start with `---` document marker
- 2-space indentation, UTF-8, LF line endings
- Max line length: 120 characters
- Schema reference: `# yaml-language-server: $schema=https://storage.googleapis.com/coderabbit_public_assets/schema.v2.json`
- Always validate against the official CodeRabbit schema before committing
