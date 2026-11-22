# Install the skills

Pick the tool you use. Each skill is a folder under `skills/` with a `SKILL.md`
file and a `references/` folder.

<!-- REVIEW: Nurlin to walk through each method once and update the screen names if they've moved. -->

- [Claude on the web or desktop app](#claude-on-the-web-or-desktop-app)
- [Claude Code](#claude-code)
- [Microsoft Copilot Studio](#microsoft-copilot-studio)
- [Other AI assistants](#other-ai-assistants)

---

## Claude on the web or desktop app

Skills work in claude.ai and the Claude desktop app on plans where Skills are
available. Code execution and file creation must be turned on under
**Settings > Capabilities**. On Team and Enterprise plans, an owner controls this.

1. Download the skill zip files from the repository's **Releases** page, one per
   skill. Or build them yourself (see [Build the zip files](#build-the-zip-files)).
2. In Claude, open **Customize > Skills**.
3. Select **+**, then **+ Create skill**, then **Upload a skill**. Upload one zip
   at a time.
4. Turn each skill on from its row in the list.
5. Start a new chat and ask an F&O question, for example: *"Why didn't my vendor
   invoice post? The error says Account number for transaction type Vendor
   balance does not exist."* Claude picks the right skill by itself.

Team and Enterprise admins can also add the skills for everyone in the
organization.

### Build the zip files

Each zip must contain the skill folder at the top level (for example
`posting-error-explainer/SKILL.md`).

With Python 3 installed, from the repository folder:

```bash
python3 scripts/build_zips.py
```

The zips are written to `dist/`.

Without Python, on Windows PowerShell:

```powershell
Get-ChildItem skills -Directory | ForEach-Object {
  Compress-Archive -Path $_.FullName -DestinationPath "dist\$($_.Name).zip" -Force
}
```

(Create the `dist` folder first.)

---

## Claude Code

### As a plugin (recommended)

In Claude Code, run:

```text
/plugin marketplace add DynAax-AB/dynaax-d365fo-functional-skills
/plugin install d365fo-functional-skills@d365fo-functional-skills
```

Restart Claude Code if the skills don't show straight away.

### By copying the folders

Copy the folders under `skills/` to one of these places:

- `~/.claude/skills/` to use them in every project, or
- `.claude/skills/` inside a project folder to use them in that project only.

On Windows, `~` is your user folder, for example `C:\Users\you\.claude\skills\`.

---

## Microsoft Copilot Studio

Copilot Studio can [upload skill files](https://learn.microsoft.com/en-us/microsoft-copilot-studio/agents-experience/skills-add-existing) directly on agents built with
the Microsoft Copilot harness. Using these agents can consume Copilot Credits.

The zips on the Releases page are built for Claude, with the skill inside a
folder. For Copilot Studio, make zips with `SKILL.md` at the top level. From the
repository folder on macOS or Linux:

```bash
mkdir -p dist && for s in skills/*/; do n=$(basename "$s"); (cd "$s" && zip -r "../../dist/$n-copilot.zip" . -x test-questions.md); done
```

On Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force dist | Out-Null
Get-ChildItem skills -Directory | ForEach-Object {
  $files = Get-ChildItem $_.FullName -Exclude test-questions.md
  Compress-Archive -Path $files.FullName -DestinationPath "dist\$($_.Name)-copilot.zip" -Force
}
```

Then add each skill to your agent:

1. Open your agent in Copilot Studio and select the **Build** tab.
2. In the components panel, select **Skills**.
3. In **Add skill**, select **Upload a skill**, then upload one zip.
4. Repeat for each skill, then test in the **Preview** tab with the questions in
   each skill's `test-questions.md`.

### If your agent doesn't show Skills

Older agents can use the same files as knowledge:

1. In Copilot Studio, open the agent.
2. Under **Knowledge**, choose **Add knowledge > Files** and upload:
   - each `SKILL.md` (rename them so you can tell them apart, for example
     `posting-error-explainer.md`), and
   - every file in each skill's `references/` folder.
   If your tenant doesn't accept `.md` files, rename them to `.txt`.
3. Paste the text below into the agent's **Instructions**.
4. Test with the questions in each skill's `test-questions.md`.

Instructions to paste:

```text
You help Dynamics 365 Finance and Supply Chain Management key users and
functional consultants with posting errors, posting setup, parameters and
setup checklists.

Your knowledge files contain one guide per topic. Pick the guide that fits
the question and follow it: ask its "Ask these first" questions when the
answer is missing, follow "How to work through it", answer in the format
under "How to answer", and hand over to a person when "When to hand over"
applies.

Never suggest changing data in the database. Never say a setup change is
safe in production without a sandbox test. If you don't know where a field
or menu is, say so rather than guessing.
```

---

## Other AI assistants

Any assistant that accepts custom instructions or uploaded documents can use the
skills as knowledge: upload the `SKILL.md` and `references/` files as documents,
and paste the instructions above.

---

## Updating

When a new version is released, upload the new zip (Claude), pull the plugin
update (Claude Code: `/plugin marketplace update`), or use **Replace** on the
uploaded skill (Copilot Studio).
