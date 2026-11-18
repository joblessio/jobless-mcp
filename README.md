# Jobless MCP

Connect your AI assistant to [Jobless](https://jobless.io), so it can read your agents,
matches and saved jobs, and search every open role we track.

```
https://api.jobless.io/mcp
```

Read-only. Requires Jobless Pro. New accounts start with a 7-day free trial, and no
credit card is needed to sign up.

## Connect

### claude.ai

1. Open **Settings → Connectors → Add custom connector**.
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
- **Disconnect any time**: remove the connector in claude.ai, or run
  `claude mcp remove jobless -s user` in Claude Code.

What the assistant does with that data is governed by its own provider's terms.

## Troubleshooting

- **"MCP access is a Pro feature"**: open [jobless.io](https://jobless.io) once while
  signed in (that's also where your free trial starts), then try again.
- **The connector keeps asking you to sign in**: remove it and add it again with the exact
  URL above, `https://api.jobless.io/mcp`, with no trailing slash.

## Contact

Questions or problems: [help@jobless.io](mailto:help@jobless.io), or open an issue here.
