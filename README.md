# ChatBotKit GitHub Actions

Official GitHub Actions for ChatBotKit.

Available actions:

- `agent` - Run the ChatBotKit CLI agent inside a GitHub Actions job

## Versioning

Versioning is driven by the root `VERSION` file.

- Update `VERSION` when you want to publish a new release.
- Merge the change to `main` in the `chatbotkit/github-actions` repository.
- The release workflow creates the immutable `vX.Y.Z` tag and updates the floating major tag such as `v0`.

Consumers should normally pin to a major tag such as `@v0`.
