
# ivuorinen's CodeRabbit.ai Configuration Repository

This repository contains my base CodeRabbit configuration that I use in my other repositories.

To use it, create a `.coderabbit.yaml` file in the project root and add this:

```yaml
remote_config:
  repository: "coderabbit"
  ref: "main"
  path: "coderabbit.yaml"
```

The consuming repository must have the same owner as this one, and CodeRabbit must have access to this repository.

You can see the full configuration here: [coderabbit.yaml](coderabbit.yaml)

This way the repository is always using the latest configuration.

## Links

- [Documentation](https://docs.coderabbit.ai) - Comprehensive docs covering all aspects of CodeRabbit.
- [YouTube Channel](https://www.youtube.com/@CodeRabbitAI) - Official YouTube channel with tutorials and updates.
- [AI Code Reviewer Examples](https://www.coderabbit.ai/blog/how-to-use-an-ai-code-reviewer-on-github-in-4-examples) - Four practical examples of using CodeRabbit.
- [OpenAPI Documentation](https://api.coderabbit.ai/api/swagger/) - Complete Swagger documentation for CodeRabbit's REST API endpoints.
