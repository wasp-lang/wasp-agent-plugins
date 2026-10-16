---
name: start-dev-server
description: Start the Wasp dev server and set up full debugging visibility. This includes running the server (with access to logs), and connecting browser console access so the agent can see client-side errors. Essential for any development or debugging work.
---

## Step 0: Get User Preferences

- [ ] Ask the user if they want to start the dev server(s) as a background task in the current session, or on their own in a separate terminal:
  - Starting as a background task
    - Pros: The agent has more autonomy, can respond directly to dev server logs (warnings, errors).
    - Cons: Certain actions can be slower, and the user has less direct control. Server logs are only visibile to the user from within the `background tasks` tab.
  - Starting externally (User)
    - Pros: The user has more direct control over app development and the Wasp CLI commands. Can be advantageous for more advanced users.
    - Cons: Debugging and feature discovery can be slower, as the agent doesn't have direct access to dev server logs (warnings, errors) or Wasp CLI commands.
- [ ] Depending on the user's choice, follow the steps below and run the commands for the user as background tasks, or guide them through running them manually in a separate terminal.

### Step 1: Prepare the Checkout

If `node_modules` is missing, install the project dependencies:

```bash
wasp install
```

If `.env.server` or `.env.client` are missing and `.env.server.example` or `.env.client.example` are available, create the missing file from the example file. Ask the user to edit the file to set the correct values.

### Step 2: Ensure the Development Database is Running

Grep the `.env.server` file for `DATABASE_URL`. If no line starts with `DATABASE_URL`, continue following this step.
If the user does have their own DATABASE_URL env var set, move on to [Step 3](#step-3-run-database-migrations).

Check the `schema.prisma` file in the project root for the `datasource` block to see which database is being used.

#### SQLite

**Skip to [Step 3](#step-3-run-database-migrations):** SQLite stores data in a local file, no database server needed.

#### PostgreSQL

Start the managed database container as a background task:

```bash
wasp start db
```

**Docker needs to be installed and running** for the managed Postgres database container (`wasp start db`) to work.

Run this as a background task in the current session.
Wait 5-15 seconds for the database to be ready.

### Step 3: Run Database Migrations

If this is the first time starting the app, or if there are pending migrations, run the following command:

```bash
wasp db migrate-dev --name <migration-name>
```

Some apps require seed data to work properly. Run the following command to seed the database:

```bash
wasp db seed <name>
```

### Step 4: Start Dev Server

Start the Wasp development server as a background task:

```bash
wasp start
```

### Step 5: Verify Server is Running

Read the client and server URLs from `wasp start` output and verify the client loads. In Wasp 0.26+, occupied ports are replaced automatically and the server health check is `/up` (HTTP 200).

For Wasp 0.26+, use `--client-port` and `--server-port` to choose ports, or `--client-url` and `--server-url` for externally accessible URLs. URL overrides do not choose listening ports. Development ports and URLs are managed by Wasp, so remove `PORT`, `WASP_SERVER_URL`, and `WASP_WEB_CLIENT_URL` from `.env.server`, `REACT_APP_API_URL` from `.env.client`, and `server.port`/`server.strictPort` from Vite config. Keep deployment environment variables unchanged.

Managed databases also select a free port in Wasp 0.26+. Wasp discovers it automatically. Use `wasp start db --db-port <port>` when a fixed database port is needed.

**If started as background task in current session:** Listen to the output for development and debugging information.
**If started externally:** Instruct the user to check the output of the external terminal and share its output with you.

### Step 6: Connect Browser Console Access (Important!)

**This step is critical for effective development and debugging.** Without browser console access, the agent cannot see client-side errors, warnings, or React issues that occur in the browser.

Ask the user (via the AskUserQuestion tool) which method they'd like to use for giving the agent visibility into the browser console:

| Option                                | Description                                                                         |
| ------------------------------------- | ----------------------------------------------------------------------------------- |
| **Chrome DevTools MCP (recommended)** | Must be installed                                                                   |
| **Built-in Chrome**                   | Use Claude Code's built-in browser connection (check status with `/chrome` command) |
| **Manual**                            | User will manually copy/paste console output when needed                            |
| **Other**                             | User has another preference                                                         |

For the Chrome DevTools MCP option, if not already installed, add the following config to their mcp client:

```json
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": ["-y", "chrome-devtools-mcp@latest"]
    }
  }
}
```
