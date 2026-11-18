# Jobless MCP

Connect your AI assistant to [Jobless](https://jobless.io), so it can read your agents,
matches and saved jobs, and search every open role we track. It connects over
MCP (Model Context Protocol), the standard way AI assistants use other apps.

```
https://api.jobless.io/mcp
```

Read-only. Requires Jobless Pro. New accounts start with a 7-day free trial, and no
credit card is needed to sign up.

**Jump to your assistant:**

- [claude.ai or the Claude desktop app](#claude-claudeai-and-the-desktop-app)
- [Claude Code](#claude-code)
- [ChatGPT or Codex](#chatgpt-and-codex)
- [Antigravity (and Gemini)](#antigravity-and-gemini)
- [Anything else](#other-apps)

Then see [things to ask](#things-to-ask), the [tools](#tools), [privacy](#privacy) and
[troubleshooting](#troubleshooting).

## Connect

### Claude (claude.ai and the desktop app)

Set it up once in either and it works in both, as long as both are signed in to the same
Claude account.

1. Add a custom connector: on claude.ai, **Settings → Connectors → Add custom connector**;
   in the desktop app, **Customize → Connectors → Add → Add custom connector**.
2. Name it `Jobless` and paste `https://api.jobless.io/mcp`.
3. Keep the detected defaults (**Sign in now**, **Use Claude's published identity**) and click **Add**.
4. Sign in with your Jobless account and click **Allow**.

Optional: under the connector's tool permissions, set **Read-only tools** to
**Always allow** so Claude doesn't ask before every call.

### Claude Code

1. In your terminal (not inside a Claude Code session), add the server:

   ```bash
   claude mcp add --transport http --scope user jobless https://api.jobless.io/mcp
   ```

   `--scope user` makes Jobless available in every folder, not just the current one.

2. Start Claude Code (`claude`), run `/mcp`, select **jobless**, and sign in with your
   Jobless account in the browser window that opens.
3. Ask Claude *"list my Jobless agents"* to confirm it works.

### ChatGPT and Codex

Set it up once in either app and it works in both.

1. Open **Plugins**: in ChatGPT, **Settings → Plugins**; in the Codex app, **Plugins** in
   the left sidebar.
2. Add a custom server: in ChatGPT, **Browse directory → Add → Add custom MCP server**; in
   Codex, **Add → Add MCP server**.
3. Fill in:
   - **Name**: `Jobless`
   - **Connection**: Server URL, `https://api.jobless.io/mcp`
   - **Authentication**: `OAuth`
4. Tick **I understand and want to continue** and click **Create as a plugin**.
5. Click **Connect Jobless**, sign in with your Jobless account, and click **Allow**.

Then ask *"list my Jobless agents"* to confirm it works. No need to change anything under
**Advanced OAuth settings**: ChatGPT detects everything on its own.

### Antigravity (and Gemini)

Antigravity is Google's Gemini-powered app, so this is also the way to use Jobless with Gemini.

1. In your terminal, add the server:

   ```bash
   agy mcp add jobless https://api.jobless.io/mcp
   ```

2. In Antigravity, run `/mcp`, select **jobless**, and click **Authenticate**.
3. Sign in with your Jobless account. Antigravity then shows a code: copy it and paste it
   back into Antigravity.
4. Ask *"list my Jobless agents"* to confirm it works.

### Other apps

Some apps can't sign you in, so they ask for an access key instead.

1. In Jobless, open **AI assistants** in the sidebar (on a phone, in the account menu), choose
   **Other apps**, and click
   **Create access key**. Copy it right away: it's shown only once.
2. In your app, add an MCP server with the address `https://api.jobless.io/mcp` and one
   header:
   - **Name**: `Authorization`
   - **Value**: copy it from the dialog's **Header value** field. It already starts with
     `Bearer`, so don't type `Bearer` yourself.

Treat the key like a password. If it leaks, revoke it in the same dialog and create a new one.

## Things to ask

- *List my Jobless agents and how many matches each has this week.*
- *Go through this week's strong and possible matches, pick the ones you think fit me best, and build me a job tracker as an HTML artifact or a spreadsheet: company, role, pay, why it fits, and the apply link.*
- *Rank this week's matches against my resume and tell me which two to apply to first.*
- *Compare my top three matches on compensation, remote policy, and anything the agent flagged as a concern.*
- *Which of my saved jobs are still open?*
- *Search for staff platform engineer roles in New York posted in the last 14 days.*

## Tools

| Tool | What it reads |
|---|---|
| `list_agents` | Your agents and their match counts |
| `list_matches` | Your matches, filterable by agent, strength, date and read status |
| `get_match` | One match: the full posting plus each agent's reasoning |
| `list_saved_jobs` | Jobs you saved, applied to, or are interviewing for |
| `get_profile` | Your profile preferences; your resume text only when asked for it |
| `search_jobs` | Every open role we track (shares the app's daily search limit) |
| `get_job` | One job's full posting and company details |

## Privacy

- **Read-only.** No tool can create, change or delete anything in your account.
- **Only your data.** Every call is scoped to the account you signed in with.
- **Your resume is shared only when a tool asks for it**, which assistants do when judging fit.
- **Disconnect any time**: remove the connector in claude.ai or the Claude desktop app, remove the plugin in
  ChatGPT or Codex, run `claude mcp remove jobless -s user` in Claude Code, or revoke your access key in Jobless.

What the assistant does with that data is governed by its own provider's terms.

## Troubleshooting

- **"MCP access is a Pro feature"**: open [jobless.io](https://jobless.io) once while
  signed in (that's also where your free trial starts), then try again.
- **"Account mismatch" when connecting from the Claude desktop app**: your browser is
  signed in to claude.ai with a different Claude account than the desktop app. Sign in to
  claude.ai in the browser with the same account, then connect again.
- **The connector or plugin keeps asking you to sign in**: remove it and add it again with the exact
  URL above, `https://api.jobless.io/mcp`, with no trailing slash.

## Contact

Questions or problems: [help@jobless.io](mailto:help@jobless.io), or open an issue here.
