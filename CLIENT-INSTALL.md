# Run a Bytesync Analysis in Claude

Bytesync has built a skill for Claude that runs a short, guided interview and shows where Bytesync could help your business — across cloud, data centre, AI, automation, core business systems, and software development.

> **You'll need Claude** — either **Claude Code** (the terminal tool) or the **Claude desktop app**. The skill runs inside Claude; there's nothing to install on your servers.

---

## Option 1 — Claude Code (recommended, stays up to date)

Paste these three commands into Claude Code, one at a time:

```
/plugin marketplace add ByteSync-Dev/bytesync-skills
/plugin install bytesync@bytesync-skills
/reload-plugins
```

That's it. The skill is now available, and it updates automatically whenever Bytesync improves it.

---

## Option 2 — Claude desktop app (single file)

1. Download the **`bytesync-analysis.skill`** file Bytesync sent you.
2. Double-click it — it opens in the Claude app.
3. Click **Save skill**.

Done. (This version doesn't auto-update; Bytesync will send a new file when there's an update.)

---

## How to run it

Just ask Claude in plain English:

> **"Run a Bytesync analysis on my business."**

(In Claude Code you can also type `/bytesync:bytesync-analysis`.)

Claude will then:

1. **Ask one quick framing question** — whether you're answering about your own business or on behalf of a client.
2. **Walk you through a short, sectioned set of questions** about your current systems and your future plans. Answer as much or as little as you like, and just say *"not relevant"* to skip anything.
3. **Produce a summary**, a fit rating across Bytesync's service lines, and recommended next steps.

At the end, you can ask Claude to **export the result to a Word document or PDF**.

---

## Tips & troubleshooting

- **Wording is flexible.** "Assess us for Bytesync" or "is there an opportunity for Bytesync here?" will also start it.
- **It won't start?** Type `/bytesync:bytesync-analysis` (Claude Code) to run it directly.
- **"Plugin not found" during install?** Run `/plugin marketplace update bytesync-skills`, then retry the install command.
- **Skill not showing up after install?** Run `/reload-plugins`, or restart Claude.
- **It's a conversation** — you can pause and pick it back up later, or tell Claude to skip ahead to the summary at any point.
