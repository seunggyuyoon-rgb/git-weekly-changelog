# git-weekly-changelog

A [Claude Code](https://claude.ai/code) plugin that turns a week of git commits into a readable, themed Markdown changelog — in seconds.

Instead of scrolling through `git log`, this skill groups commits by feature area and produces a clean summary suitable for team updates, release notes, or sprint reviews.

## Installation

```
/plugin install https://github.com/seunggyuyoon-rgb/git-weekly-changelog
```

## Usage

```
/git-weekly-changelog:git-weekly-changelog
```

With a custom range:

```
/git-weekly-changelog:git-weekly-changelog last 2 weeks
/git-weekly-changelog:git-weekly-changelog since Monday
```

## Example output

```markdown
# Git Weekly Changelog

**Analysis basis**
- Generated: 2026-05-06 09:00:00 UTC+9
- Range: 2026-04-29 → 2026-05-06
- Branch: main
- Method: read-only git inspection

---

## 🚀 New Features
- Added OAuth2 token refresh support (#42)
- Introduced dark mode toggle in settings panel (#44)

## 🐛 Bug Fixes
- Fixed race condition in job queue flush (#45)
- Resolved memory leak in WebSocket handler (#47)

## 📚 Documentation
- Updated API reference for v2 endpoints
- Added contributing guide

---

**Summary**

This week's focus was auth reliability, UX polish, and API docs cleanup.
```

## Notes

- Uses read-only `git log` / `git diff` only — no side effects, safe on any machine
- Responds in the user's language (Korean output if asked in Korean)
- No external dependencies or scripts required
- Works on any git repository

## Plugin structure

```
git-weekly-changelog/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── git-weekly-changelog/
│       └── SKILL.md
└── README.md
```
