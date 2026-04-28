# Skill: changelog

Manages versioned changelog workflow for the CRM Gantt project.

## Usage

- `/changelog start` — begin a new version: determine next version number, create feature branch, inform the user
- `/changelog` — document changes on the current branch into `CHANGELOG.md` (can be run multiple times)
- `/changelog finish` — finalize the version: update `CHANGELOG.md`, commit, push, and open a PR to main

---

## `/changelog start`

1. Read `CHANGELOG.md` to find the highest existing version number (e.g. `## v2`) and increment by 1 to get `vN`.
2. Run `git checkout -b feature/vN` to create and switch to the new branch.
3. Tell the user: which branch was created and what the new version number will be.

---

## `/changelog` (document changes)

1. **Determine current version** — read the branch name (`git branch --show-current`) to get the version number (e.g. `feature/v3` → `v3`). If not on a feature branch, read `CHANGELOG.md` and increment the highest version.

2. **Identify what changed** — run `git diff main...HEAD` and `git log main..HEAD --oneline` to get a full picture of all changes on this branch so far.

3. **Create or update the entry:**
   - If `## vN` already exists in `CHANGELOG.md`: **replace** that entire block with a freshly written version covering all changes on the branch (not just the latest). Update the date to today.
   - If `## vN` does not yet exist: **prepend** a new `## vN – YYYY-MM-DD` block at the top (just below the `# Changelog` heading).
   - The entry always reflects the **complete state of the branch**, not just the last commit — so running `/changelog` multiple times during development is safe and idempotent.

4. **Format each entry** using `###` subsections per logical change group:
   - For data/schedule changes: markdown table with old vs new values
   - For new items: table of key fields
   - For config/style changes: before/after table
   - End notable exceptions with a `> Note:` blockquote

5. **Do not touch other version entries** — only the current `## vN` block is written or replaced.

---

## Format reference

```markdown
## vN – YYYY-MM-DD

### <Change category>
<One sentence explaining why this change was made.>

| Column A | Column B | Column C |
|----------|----------|----------|
| ...      | ...      | ...      |

> Note: any exceptions or caveats
```
