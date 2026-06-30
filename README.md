# Bytesync Skills for Claude

A Claude plugin marketplace that distributes Bytesync's client tools. The first plugin, **bytesync**, contains the **bytesync-analysis** skill: a guided discovery interview that assesses whether there's potential for a Bytesync engagement across cloud, data centre, AI, automation, core business systems, and development services.

> **Prerequisite:** these tools run *inside Claude* (the Claude desktop app / Cowork, or Claude Code). A client who doesn't use Claude can't run them from a web browser. If you need to reach non-Claude prospects, host a web version of the questionnaire instead.

---

## For clients — install in ~30 seconds

In Claude Code, run:

```
/plugin marketplace add ByteSync-Dev/bytesync-skills
/plugin install bytesync@bytesync-skills
/reload-plugins
```

That's it. The skill now lives in that Claude install and **updates automatically** when Bytesync publishes a new version.

### Using it

Either just describe the task and Claude will trigger the skill automatically:

> "Run a Bytesync analysis on us."

…or invoke it explicitly:

```
/bytesync:bytesync-analysis
```

Claude then runs a short, sectioned interview and produces a discovery summary, a per-service-line fit rating, and recommended next steps.

---

## Alternative: the single-file `.skill`

If a client just wants the skill without adding a marketplace, hand them the **`bytesync-analysis.skill`** file (hosted for download or emailed). In the Claude desktop app they open it and click **Save skill**. Simpler, but it does **not** auto-update — you'd resend the file when you publish a new version.

---

## For Bytesync — host & maintain

1. **Publish this folder as a Git repo.** GitHub is recommended (built-in versioning + the `owner/repo` shorthand). Push the whole `bytesync-marketplace/` directory contents to the repo root so that `.claude-plugin/marketplace.json` sits at the top level.
2. **Tell clients the add command:** `/plugin marketplace add ByteSync-Dev/bytesync-skills` then `/plugin install bytesync@bytesync-skills`.
3. **Publish updates:** edit the skill, **bump `version`** in both `.claude-plugin/marketplace.json` and `plugins/bytesync/.claude-plugin/plugin.json` (e.g. `1.0.1`), and push. Clients receive the update automatically on next start. (If you omit `version`, every commit counts as a new version instead.)
4. **Validate before publishing:**

   ```
   claude plugin validate .
   ```

### Repo layout

```
bytesync-skills/                         (repo root)
├── .claude-plugin/
│   └── marketplace.json                 catalog: lists the "bytesync" plugin
├── plugins/
│   └── bytesync/
│       ├── .claude-plugin/
│       │   └── plugin.json              plugin manifest (name, version)
│       └── skills/
│           └── bytesync-analysis/
│               └── SKILL.md             the skill itself
└── README.md
```

### Adding more skills later

Drop another `skills/<new-skill>/SKILL.md` under `plugins/bytesync/skills/`, bump the version, and push. It ships under the same `bytesync` plugin — clients get it on the next update with nothing new to install.

---

*Distribution requires the client to trust and install the plugin — Claude never auto-installs code from a link, by design. The marketplace command above is the closest one-step path.*
