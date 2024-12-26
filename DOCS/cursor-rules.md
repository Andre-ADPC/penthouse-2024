# Cursor Rule Set Documentation

This document outlines the rules and tasks for managing dependencies in the project.

## Rules

### Dependency Updates

Ensures all dependencies are kept up to date with their latest compatible versions. This rule is enabled and will automatically update dependencies when possible.

### Lockfile Consistency

Maintains consistency in the lockfile across different development environments. This rule is enabled and enforces consistent lockfile usage.

### Peer Dependencies

Automatically handles and resolves peer dependency warnings. This rule is enabled and will resolve peer dependency conflicts.

## Tasks

### Manual Tasks

#### Update Single Dependency

- **Description**: Update a specific dependency and verify changes through tests
- **Command**: `pnpm add <dependency-name>@latest && pnpm test`
- **Trigger**: Manual execution required

#### Inspect Dependency Tree

- **Description**: Analyze dependency relationships and check for outdated packages
- **Command**: `pnpm why <dependency-name> && pnpm outdated`
- **Trigger**: Manual execution required

#### Post-Commit Rollback

- **Description**: Provides ability to revert the last commit if dependency issues are discovered
- **Command**: `git revert HEAD`
- **Trigger**: Manual execution required

### Automated Tasks

#### Pre-Commit Check

- **Description**: Performs comprehensive dependency checks before committing changes
- **Command**: `pnpm audit && pnpm explain peer-dependencies && pnpm test`
- **Trigger**: Automatically runs before each commit

#### Daily Updates

- **Description**: Performs automated dependency updates daily
- **Command**: `pnpm update --latest && pnpm dedupe && pnpm audit`
- **Trigger**: Automatically runs every 24 hours

## Cursor Rules in JSON Format

```json
{
  "rules": {
    "dependency-updates": {
      "description": "Ensure all dependencies are updated to their latest compatible versions",
      "enabled": true,
      "action": "update"
    },
    "lockfile-consistency": {
      "description": "Maintain consistent lockfile across environments",
      "enabled": true,
      "action": "enforce"
    },
    "peer-dependencies": {
      "description": "Fix peer dependency warnings",
      "enabled": true,
      "action": "resolve"
    }
  },
  "tasks": {
    "update-single-dependency": {
      "description": "Update a single dependency and test changes.",
      "command": "pnpm add <dependency-name>@latest && pnpm test",
      "enabled": true,
      "trigger": "manual"
    },
    "inspect-dependency-tree": {
      "description": "Inspect the dependency tree for issues or outdated packages.",
      "command": "pnpm why <dependency-name> && pnpm outdated",
      "enabled": true,
      "trigger": "manual"
    },
    "pre-commit-check": {
      "description": "Run dependency audits, peer dependency checks, and tests before committing changes.",
      "command": "pnpm audit && pnpm explain peer-dependencies && pnpm test",
      "enabled": true,
      "trigger": "pre-commit"
    },
    "post-commit-rollback": {
      "description": "Revert the last commit if a dependency issue arises.",
      "command": "git revert HEAD",
      "enabled": true,
      "trigger": "manual"
    },
    "schedule-daily-updates": {
      "description": "Automatically update dependencies once every 24 hours.",
      "command": "pnpm update --latest && pnpm dedupe && pnpm audit",
      "enabled": true,
      "trigger": "schedule:24h"
    }
  }
}
```
