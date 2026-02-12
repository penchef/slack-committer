# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

**slack-committer** is a GitHub Action that resolves the current GitHub committer to a Slack user ID or channel ID, using a JSON mapping provided as input.

Based on [spatie/slack-committer](https://github.com/spatie/slack-committer). Typically used in CI workflows to notify the right person on Slack after builds/deploys.

## Architecture

- `index.js` - Single-file action entry point (uses `@actions/core` and `@actions/github`)
- `action.yml` - GitHub Action metadata (inputs: `user-mapping`, outputs: `username`)
- `users.json` - Example user mapping file
- `.github/workflows/notify.yml` - Reusable notification workflow
- `.github/workflows/caller.yml` - Example caller workflow

## Development

```bash
# Install dependencies
yarn install
```

No build step. The action runs `index.js` directly via Node 16.

## Usage

The action is referenced in workflows as:
```yaml
uses: penchef/slack-committer@v1.2
```

Input `user-mapping` is a JSON string mapping GitHub usernames (case-insensitive) to Slack IDs. A `"fallback"` key is used when no user matches.

## Git Workflow

### Branch Naming Convention
Use the format: `<initials>/<type>/CAN-XXXXX-description`

**Types:** `chore`, `feature`, `fix`

**Examples:**
- `js/feature/CAN-12345-add-watch-list` - Feature with JIRA ticket
- `js/fix/CAN-12346-fix-login-bug` - Bug fix with JIRA ticket
- `js/chore/update-dependencies` - Chore without JIRA ticket
