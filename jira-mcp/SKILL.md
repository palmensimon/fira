---
name: jira-mcp
description: Fetch Jira ticket information using the jura CLI. Use when you need context about the Jira task currently being worked on, or to list all tickets assigned to the user.
---

# Fira Jira Skill

This skill lets you retrieve Jira ticket data via the `jura` CLI, which reads from a local cache populated by the `jura` TUI. No network calls are made — only locally cached data is accessible.

## Security & Privacy
`jura` reads from `~/.config/jura/mine_cache.json`, which is populated when the user opens the Mine tab in the jura TUI. The user controls what data is available.

## Commands

### List all assigned tickets
```
jura tickets
```
Returns a JSON array of all tickets in the local cache:
```json
[{ "key": "PROJ-123", "summary": "...", "status": "In Progress",
   "type": "Story", "priority": "Medium", "assignee": "Jane Doe" }]
```

### Get full details for a specific ticket
```
jura ticket PROJ-123
```
Returns a JSON object with all fields:
```json
{ "key": "PROJ-123", "summary": "...", "description": "...",
  "status": "In Progress", "type": "Story", "priority": "Medium",
  "assignee": "Jane Doe", "components": ["Frontend"],
  "labels": ["auth"], "parent": { "key": "PROJ-100", "summary": "..." },
  "sprint": "Sprint 42" }
```

## Workflow

### Understand the current task
1. Get the current branch: `git branch --show-current`
2. Extract the ticket key (pattern: `[A-Z]+-\d+`, e.g. `PROJ-123`)
3. Run `jura ticket PROJ-123` to get full details

### Browse all assigned tickets
Run `jura tickets` to get a list, then `jura ticket <KEY>` for any ticket needing more detail.

## Handling Missing Data
If `jura tickets` returns `{"error": "No tickets cached..."}`, ask the user to open the jura TUI — loading the Mine tab automatically populates the cache.

## Important Notes
- Read-only — cannot comment, transition, or create tickets
- Keys are case-insensitive (`proj-123` and `PROJ-123` both work)
