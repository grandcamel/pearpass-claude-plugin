# PearPass Claude Code Plugin

A Claude Code plugin to support developers working on the [PearPass Browser Extension](https://github.com/tetherto/pearpass-app-browser-extension).

## Installation

Add this plugin to your Claude Code configuration:

```bash
# From the PearPass project directory
claude plugins add ~/Projects/pearpass-claude-plugin
```

Or add to your `.claude/settings.json`:

```json
{
  "plugins": [
    "~/Projects/pearpass-claude-plugin"
  ]
}
```

## Features

### Skills

| Skill | Description |
|-------|-------------|
| `pearpass:build` | Build management with Vite multi-config system |
| `pearpass:test` | Jest testing workflow |
| `pearpass:extension` | Browser extension development utilities |

### Agents

| Agent | Description |
|-------|-------------|
| `security-reviewer` | Security-focused code review for crypto and extension vulnerabilities |
| `i18n-helper` | LinguiJS internationalization support |
| `component-generator` | Generate components following project patterns |

### Commands

| Command | Description |
|---------|-------------|
| `/pearpass-dev` | Start development environment with watch builds |
| `/pearpass-review` | Security-focused code review |
| `/pearpass-release` | Prepare release with tests, build, and changelog |

## Usage Examples

### Start Development
```
/pearpass-dev
```

### Run Security Review on Staged Changes
```
/pearpass-review
```

### Review Specific File
```
/pearpass-review scope=src/vault/encryption.js
```

### Prepare Release
```
/pearpass-release version=1.2.0
```

## PearPass Technology Stack

- **Frontend:** React + Vite (multi-config build)
- **Styling:** Tailwind CSS
- **i18n:** LinguiJS
- **Testing:** Jest
- **Crypto:** pearpass-lib-vault

## License

Apache 2.0 (matching the PearPass project)
