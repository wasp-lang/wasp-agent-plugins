# Wasp Plugins for Coding Agents

Official Wasp full-stack framework plugins for coding agents like [Claude Code](https://claude.com/product/claude-code), [Codex](https://openai.com/codex/), [Cursor](https://www.cursor.com/), [Gemini CLI](https://geminicli.com/), [Copilot](https://github.com/features/copilot/cli), [OpenCode](https://opencode.ai/), etc.

## Available Plugins

### Wasp

The main plugin that provides an optimal experience developing full-stack web apps with Wasp (React, Node.js, Prisma) through curated access to docs, workflows and best practices.

-> [Wasp Plugin for Claude Code](./plugins/wasp)

## Installation

### Claude Code

To install this marketplace and browse the available Wasp plugins, run the following command:

```bash
claude plugin marketplace add wasp-lang/wasp-agent-plugins
```

### Other Agents (Cursor, Codex, Gemini, Copilot, OpenCode, etc.)

To install the Wasp agent skills for other agents like Codex, Gemini, Copilot, etc., run the following command:

```bash
npx skills add wasp-lang/wasp-agent-plugins
```

## Contributing

To add a new plugin:

1. Create your plugin in the `plugins/` directory
2. Add an entry to `.claude-plugin/marketplace.json`
3. Submit a pull request

## License

MIT - See individual plugin directories for specific licenses.
