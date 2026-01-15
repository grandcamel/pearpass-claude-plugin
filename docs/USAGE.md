# PearPass Plugin Usage Guide

This guide covers how to use the pearpass-dev Claude Code plugin for PearPass browser extension development.

## Installation

### Option 1: Claude CLI

```bash
cd /path/to/pearpass-app-browser-extension
claude plugins add ~/Projects/pearpass-claude-plugin
```

### Option 2: Manual Configuration

Add to your project's `.claude/settings.json`:

```json
{
  "plugins": [
    "~/Projects/pearpass-claude-plugin"
  ]
}
```

## Skills

Skills provide contextual guidance for common development tasks.

### Build Skill (`pearpass:build`)

Helps with Vite multi-configuration builds.

**When to use:**
- Building the extension for development or production
- Understanding the build system
- Troubleshooting build errors

**Trigger phrases:**
- "Build the extension"
- "Run a production build"
- "Start watch mode"
- "Build only the background script"

### Test Skill (`pearpass:test`)

Guides Jest testing workflows.

**When to use:**
- Running tests
- Debugging test failures
- Checking coverage
- Writing new tests

**Trigger phrases:**
- "Run the tests"
- "Check test coverage"
- "Run tests for vault component"
- "Why is this test failing?"

### Extension Skill (`pearpass:extension`)

Browser extension development utilities.

**When to use:**
- Loading the extension in a browser
- Debugging extension issues
- Understanding manifest configuration
- Checking permissions

**Trigger phrases:**
- "How do I load the extension?"
- "Debug the service worker"
- "Check manifest permissions"
- "Extension not working"

## Agents

Agents are specialized assistants for complex tasks.

### Security Reviewer

Performs security-focused code reviews.

**Capabilities:**
- Cryptographic operation analysis
- Password handling audit
- Extension security checks
- OWASP vulnerability scanning

**Invocation:**
```
Review this code for security issues
Check the vault encryption implementation
Audit password handling in login.js
```

### i18n Helper

Manages internationalization with LinguiJS.

**Capabilities:**
- Find hardcoded strings
- Extract translation strings
- Validate .po files
- Generate translation templates

**Invocation:**
```
Find untranslated strings in the popup
Extract strings for translation
Check translation coverage
```

### Component Generator

Scaffolds new components following project patterns.

**Capabilities:**
- React UI components
- Content scripts
- Background handlers
- Popup pages

**Invocation:**
```
Create a new password strength component
Generate a content script for form detection
Scaffold a background message handler
```

## Commands

Commands are quick-access workflows invoked with `/`.

### /pearpass-dev

Start the development environment.

```
/pearpass-dev
```

With specific target:
```
/pearpass-dev target=background
```

**Targets:** `all`, `background`, `content`, `inject`, `main`

**What it does:**
1. Checks prerequisites (Node.js, npm)
2. Installs dependencies if needed
3. Starts watch build
4. Provides browser loading instructions

### /pearpass-review

Run a security-focused code review.

```
/pearpass-review
```

Review specific scope:
```
/pearpass-review scope=staged
/pearpass-review scope=branch
/pearpass-review scope=src/vault/
```

**Scopes:**
- `staged` - Git staged files (default)
- `branch` - All changes on current branch
- `all` - Full codebase scan
- `<path>` - Specific file or directory

**What it does:**
1. Identifies files to review
2. Checks for security anti-patterns
3. Analyzes crypto usage
4. Reports findings by severity

### /pearpass-release

Prepare a release.

```
/pearpass-release
```

With version:
```
/pearpass-release version=1.2.0
```

Skip tests (not recommended):
```
/pearpass-release skip-tests=true
```

**What it does:**
1. Runs pre-flight checks
2. Executes test suite
3. Creates production build
4. Validates manifest
5. Generates changelog
6. Packages for distribution

## Workflow Examples

### Daily Development

```
# Start your session
/pearpass-dev

# Make changes...

# Before committing
/pearpass-review scope=staged

# Commit your changes
```

### Adding a New Feature

```
# Ask for component scaffold
"Create a React component for displaying password strength"

# Implement the feature...

# Check for i18n
"Find any hardcoded strings in the new component"

# Run tests
"Run tests for the password strength component"
```

### Preparing a Release

```
# Full release workflow
/pearpass-release version=1.3.0

# Review the changelog
# Upload to browser stores
```

## Tips

1. **Security first**: Always run `/pearpass-review` before merging
2. **Use agents**: For complex tasks, let agents handle the heavy lifting
3. **Check i18n**: New UI text should be wrapped with `<Trans>` or `t` macro
4. **Test coverage**: Run coverage checks regularly with the test skill
