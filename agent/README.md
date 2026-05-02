# Agent Action

`agent` runs the ChatBotKit CLI agent inside a GitHub Actions job.

This action executes `cbk agent` via an isolated `npm exec` invocation of `@chatbotkit/cli` in the target working directory.

## Inputs

- `prompt` - Required task prompt passed to `cbk agent --prompt`
- `tools` - Optional tool list passed to `cbk agent --tools`
- `bot` - Optional bot id passed to `cbk agent --bot`
- `model` - Optional model name passed to `cbk agent --model`
- `dataset` - Optional dataset id passed to `cbk agent --dataset`
- `skillset` - Optional skillset id passed to `cbk agent --skillset`
- `cli-version` - Optional CLI version to execute, defaults to `latest`
- `node-version` - Optional Node.js version, defaults to `20`
- `working-directory` - Optional working directory, defaults to `.`

The optional CLI-facing inputs are applied in this order: `tools`, `bot`, `model`, `dataset`, `skillset`.

## Required Environment

Set the secrets and environment variables required by your ChatBotKit CLI configuration. In most cases that means exporting `CHATBOTKIT_API_KEY` from repository or organization secrets.

## Example

```yaml
jobs:
  agent:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: chatbotkit/github-actions/agent@v0
        with:
          tools: read,write,edit,find,exec
          bot: bot_123
          model: gpt-5
          dataset: dataset_123
          skillset: skillset_123
          prompt: >-
            Read the repository and propose a small documentation improvement.
          cli-version: 1.34.0
          working-directory: .
        env:
          CHATBOTKIT_API_KEY: ${{ secrets.CHATBOTKIT_API_KEY }}
```

## Notes

- Prefer pinned `cli-version` values for reproducible workflows.
- The CLI is executed without a global install, which avoids leaving shared state on self-hosted runners.
- The action runs with the permissions, checked-out files, and runner access provided by the calling workflow.
- For centralized orchestration across many repositories, pair this action with a reusable workflow in the same repository.
