# Wasp Plugin

A Wasp full-stack framework plugin for your coding agent (Claude Code, Cursor, Codex, Gemini, Copilot, OpenCode, etc.) that provides an optimal experience developing full-stack web apps with Wasp (React, Node.js, Prisma) through curated access to docs, workflows and best practices.

## Features

- **Wasp documentation**: Ensures that your coding agent always accesses the right version of the Wasp framework documentation (in sync with your current Wasp project) at the right times, with additional enhancements (coming in the future: caching, additional knowledge from Wasp Github and Discord, ...).
- **Adds Wasp Knowledge**: Import Wasp best practices and conventions to your project's CLAUDE.md
- **Configures Wasp**: Easily add Wasp framework features like authentication, database, email, styling (tailwind, shadcn), and other integrations
- **Deployment Guidance**: Your coding agent will guide you through deploying your Wasp app to Railway or Fly.io via the Wasp CLI

## Installation

### Claude Code

#### Add the Wasp marketplace

```bash
claude plugin marketplace add wasp-lang/wasp-agent-plugins
```

#### Install the Wasp plugin

```bash
claude plugin install wasp@wasp-agent-plugins --scope project
```

> [!NOTE]
> We suggest installing the plugin at the `project` scope (`settings.json` are commited to git).
> Or by using the `local` scope (`settings.local.json` are not commited to git).


### Other Agents (Codex, Cursor, Gemini, Copilot, OpenCode, etc.)

Run the following command and select all the skills:

```bash
npx skills add wasp-lang/wasp-agent-plugins
```

### Configure and Initialize the plugin

After installing, in an active session, run:
```bash
/wasp-plugin-init
```
- This will add Wasp knowledge to your project's CLAUDE.md or AGENTS.md file.

```
Run the 'start-dev-server' skill.
```
- This will start the Wasp development environment as a background task so the agent can have full insight into the Wasp app while developing/debugging.

Finally, to access more information about the plugin and its features, run:
```bash
/wasp-plugin-help
```
- This will show the plugin's features and skills.

## Skills

Check out the individual [skills](./skills) to learn more about what they are and what they do.

## Recommended Permissions

For the best experience, add these permissions to your Claude project or user settings:

```json
{
  "permissions": {
    "allow": [
      "Bash(wasp:*)",
      "Skill(wasp:*)",
      "WebFetch(domain:wasp.sh)",
      "WebFetch(domain:raw.githubusercontent.com)",
      "mcp__plugin_wasp_chrome-devtools__*"
    ]
  }
}
```

## License

MIT
