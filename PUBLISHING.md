# Publishing the Bytesync marketplace to GitHub

**Repo:** https://github.com/ByteSync-Dev/bytesync-skills (already created)

**Goal:** get these files into the repo so that `.claude-plugin/marketplace.json` sits at the **repository root**.

> ## ⚠️ The one thing people get wrong
> The download is a folder named `bytesync-marketplace/`. You publish the **contents** of that folder to the repo root — **not the folder itself**.
>
> After publishing, the top level of your repo must look like this:
> ```
> .claude-plugin/marketplace.json
> plugins/bytesync/.claude-plugin/plugin.json
> plugins/bytesync/skills/bytesync-analysis/SKILL.md
> README.md
> CLIENT-INSTALL.md
> PUBLISHING.md
> ```
> If instead you see `bytesync-marketplace/.claude-plugin/...`, everything is nested one level too deep and client installs will fail.

---

## Method A — Git command line (recommended)

Prerequisites: `git` installed and push access to the repo.

1. **Unzip** `bytesync-marketplace.zip`. You get a `bytesync-marketplace/` folder.

2. **Clone** the (empty) repo and enter it:
   ```bash
   git clone https://github.com/ByteSync-Dev/bytesync-skills.git
   cd bytesync-skills
   ```

3. **Copy the contents** of the unzipped folder into the clone. The trailing `/.` matters — it includes the hidden `.claude-plugin` folder:
   ```bash
   # macOS / Linux
   cp -R /path/to/bytesync-marketplace/. .
   ```
   ```powershell
   # Windows PowerShell
   Copy-Item -Path "C:\path\to\bytesync-marketplace\*" -Destination . -Recurse -Force
   ```

4. **Confirm the layout** — you should see `.claude-plugin`, `plugins`, and `README.md` at the top level:
   ```bash
   ls -a
   cat .claude-plugin/marketplace.json
   ```

5. **Commit and push:**
   ```bash
   git add .
   git commit -m "Add Bytesync marketplace and bytesync-analysis skill"
   git push origin main
   ```
   (If your default branch is `master`, push to that instead.)

---

## Method B — GitHub web UI (no git needed)

1. **Unzip** `bytesync-marketplace.zip`.

2. Show hidden files so you can see the `.claude-plugin` folder (its name starts with a dot):
   - **macOS Finder:** press `Cmd + Shift + .`
   - **Windows Explorer:** View → Show → Hidden items

3. Open https://github.com/ByteSync-Dev/bytesync-skills → **Add file** → **Upload files**.

4. Open the unzipped `bytesync-marketplace` folder, select **everything inside it** (the `.claude-plugin` folder, the `plugins` folder, `README.md`, and the other `.md` files), and **drag them onto the upload area**. GitHub keeps the folder structure.

5. Add a commit message and click **Commit changes**.

6. **Verify:** the repo's root page should now show `.claude-plugin/` and `plugins/` at the top level — not a single `bytesync-marketplace/` folder.

---

## Make the repo public

So clients can add the marketplace without GitHub credentials:

**Settings → General → Danger Zone → Change repository visibility → Public.**

If you keep it private, every client must be authenticated to this repo — fine for internal teams, awkward for prospects.

---

## Validate (optional, needs Claude Code)

From inside the repo folder:
```bash
claude plugin validate .
```
This checks the marketplace JSON and the skill's frontmatter. Fix anything it flags.

---

## Test it yourself

In Claude Code:
```
/plugin marketplace add ByteSync-Dev/bytesync-skills
/plugin install bytesync@bytesync-skills
/reload-plugins
```
Then type **"run a bytesync analysis"** to confirm it triggers and behaves well.

---

## Publishing updates later

1. Edit the skill at `plugins/bytesync/skills/bytesync-analysis/SKILL.md`.
2. **Bump the `version`** in **both** files (e.g. `1.0.0` → `1.0.1`):
   - `.claude-plugin/marketplace.json` (the plugin entry's `version`)
   - `plugins/bytesync/.claude-plugin/plugin.json`
3. Commit and push.

Clients pick up the new version automatically on next start, or immediately with `/plugin marketplace update bytesync-skills`.

> If you *don't* bump the version, existing clients stay on the cached copy and won't see your changes. (Alternative: delete the `version` fields entirely and every push automatically counts as a new version.)
