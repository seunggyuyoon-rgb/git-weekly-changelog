---
name: git-weekly-changelog
description: Summarize the last week of git history into a grouped Markdown changelog organized by feature area. Use when the user asks for weekly update notes, recent branch changes, release-style summaries, or a changelog grouped by theme rather than by commit.
---

# Git Weekly Changelog

Produce a concise, readable weekly changelog from repository history. Group by user-visible capability or operational area — not a raw commit list.

## Workflow

1. **Establish the time window** from the current local time:
   - Default: the last 7 days.
   - Honor a different range if the user specifies one (e.g. "last 2 weeks", "since Monday").
   - State the exact start and end timestamps, including timezone.

2. **Read repository context** before doing any work:
   - Check for `CLAUDE.md` for project conventions.
   - Use read-only git and file inspection only. Do not run builds, tests, or other side-effecting commands.

3. **Inspect git history** with lightweight read-only commands:
   ```bash
   git status --short --branch
   git log <branch> --since='<window>' --date=iso-strict --pretty='%h %ad %s (%an)'
   git log <branch> --since='<window>' --first-parent --date=iso-strict --pretty='%h %ad %s'
   git diff --shortstat <base>..<branch>
   git diff --dirstat=files,5 <base>..<branch>
   ```
   Use `git show --stat` on key merge commits when needed.

4. **Group by theme**, not by time:
   - Merge related `feat`, `fix`, `refactor`, `docs`, and `test` commits under a single feature heading.
   - Reference PR numbers or branch names only when they clarify the grouping.
   - Aim for 4–8 sections. Skip a label if nothing fits it.

5. **Write output**:
   - Chat output by default.
   - If the user requests a file, save to `docs/changelog-YYYY-MM-DD.md` unless another path is specified.
   - Use the Write tool, not shell heredocs.

## Output Format

```markdown
# Git Weekly Changelog

**Analysis basis**

- Generated: `YYYY-MM-DD HH:MM:SS TZ`
- Range: `YYYY-MM-DD` → `YYYY-MM-DD`
- Branch: `main`
- Method: read-only git inspection

---

## 🚀 New Features

- ...

## 🐛 Bug Fixes

- ...

## ♻️ Refactoring & Internals

- ...

## 📚 Documentation

- ...

---

**Summary**

This week's work focused on ...
```

Respond in the user's language. If the user writes in Korean, write the changelog in Korean.

## Grouping Labels

Use whichever labels fit the actual changes. Common options:

- 🚀 New Features
- 🐛 Bug Fixes
- ♻️ Refactoring & Internals
- 🔧 Configuration & Infrastructure
- 📚 Documentation
- 🧪 Tests & CI
- ⚡ Performance
- 🔒 Security
- 🗂️ Dependencies & Tooling
- 💥 Breaking Changes

Don't force every label. Use only what the commits support.

## Quality Bar

- Each bullet must be traceable to at least one commit, diff, or changed file.
- Describe what changed and why it matters to a reader unfamiliar with the commits.
- Omit commit hashes from bullets; mention them only as supporting evidence when useful.
- If tests or builds were not run, say so explicitly.
