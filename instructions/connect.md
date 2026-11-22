# Connect NorthList Posts

Read this file only when the user pastes a setup prompt from NorthList Posts ("Connect NorthList Posts to this AI app", with a server address and a token), or types `connect`.

The values in the prompt:
- `<mcp>`: the server address, ending in `/mcp`, for example `https://posts.northlist.site/mcp`.
- `<token>`: the token. It starts with `nlpost_`.

If the user typed `connect` without a prompt, tell them to open the Connect page in NorthList Posts, create a setup prompt and paste it here. Stop.

## The token

- The token goes only into the AI app's own MCP settings for this user, which live outside this folder.
- Never write it into a file in this folder, including `.mcp.json`, `.codex/` or `.agents/`.
- Never repeat it in your messages. Call it "your token".
- If a step would put it anywhere else, stop and ask the user.
- Never change the app's permission or approval settings. The user allows the tools in the app itself, the first time each one runs.

## 1. Which app is this?

Say in one line which app you are running in: Antigravity, Claude Code (also the Code tab of the Claude desktop app), or Codex (the CLI, the IDE extension or the ChatGPT desktop app). If you cannot tell, ask the user once.

## 2. Add the server to the app

The app asks the user to allow these changes, because they are outside this folder. If a server named `northlist-posts` already exists (an older token), replace it. Leave every other server as it is.

**Claude Code**
1. If `claude mcp list` shows `northlist-posts`, run `claude mcp remove northlist-posts --scope user`.
2. Run:
   ```
   claude mcp add --transport http --scope user northlist-posts <mcp> --header "Authorization: Bearer <token>"
   ```
3. Check with `claude mcp list`: `northlist-posts` must be listed with `<mcp>`. Never run `claude mcp get northlist-posts`, which can show the token.

**Codex**
1. Open `~/.codex/config.toml`. Create it if it is missing.
2. Remove an existing `[mcp_servers.northlist-posts]` table, then add:
   ```toml
   [mcp_servers.northlist-posts]
   url = "<mcp>"
   http_headers = { "Authorization" = "Bearer <token>" }
   ```
3. Keep everything else in the file as it is.

**Antigravity**
1. Open `~/.gemini/config/mcp_config.json`. Create it as `{ "mcpServers": {} }` if it is missing.
2. Under `mcpServers`, set:
   ```json
   "northlist-posts": { "serverUrl": "<mcp>", "headers": { "Authorization": "Bearer <token>" } }
   ```
3. Keep everything else in the file as it is, and keep it valid JSON. Never use the folder's own `.agents/mcp_config.json`.

**Another app**

Do not guess where it keeps its settings. Tell the user to add an MCP server named `northlist-posts` in that app's settings: the address `<mcp>`, and the header `Authorization` with the value `Bearer` followed by the token from the setup prompt.

## 3. Tell the user

In a few short lines, without the token:
- NorthList Posts was added to this app's settings for this user.
- **What to do now:**
  - Claude Code: open a new chat in this folder, because new servers load at the start of a chat.
  - Codex: restart the app (desktop: Restart; IDE: Restart extension; CLI: start a new session).
  - Antigravity: Refresh the MCP servers.
- Their spaces are already set up in the app. Then `daily` each morning (or set it as a scheduled task if this app can run them, before the time in the setup prompt).
- The first time each tool runs, the app asks. Allow it for good: "Yes, and don't ask again" in Claude Code, "Allow and don't ask me again" in Codex, "Always allow" in Antigravity.

If the tools already work in this chat (some apps load new servers at once), call `get_profile` and name the spaces you see, so the user knows it worked (the app also ticks "Connected" by itself).

**Reconnect.** When a token expires or is revoked, the user creates a new setup prompt on the Connect page and pastes it here. The same steps replace the old token.
