# PearPass Claude Code Plugin

A Claude Code plugin to support developers working on the [PearPass Browser Extension](https://github.com/tetherto/pearpass-app-browser-extension).

## Installation

### From GitHub

```bash
claude plugins add https://github.com/grandcamel/pearpass-claude-plugin
```

### Local Development

```bash
# Clone and install locally
git clone https://github.com/grandcamel/pearpass-claude-plugin.git
claude plugins add ./pearpass-claude-plugin
```

## Features

### Skills (Auto-activated)

Skills automatically activate when you ask related questions:

| Skill | Triggers On |
|-------|-------------|
| **build** | "build the extension", "run vite build", "start watch mode" |
| **test** | "run tests", "npm test", "check coverage" |
| **extension** | "load extension", "debug manifest", "reload extension" |

### Agents (Task-specific)

Agents are invoked for specialized tasks:

| Agent | Use For |
|-------|---------|
| **security-reviewer** | Security audits, crypto review, vulnerability checks |
| **i18n-helper** | Find hardcoded strings, translation validation |
| **component-generator** | Scaffold React components, content scripts, handlers |

### Commands (Slash commands)

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

### Run Security Review
```
/pearpass-review
/pearpass-review scope=src/vault/
```

### Prepare Release
```
/pearpass-release version=1.2.0
```

### Trigger Agents
```
Review this code for security issues
Find hardcoded strings that need translation
Create a new React component for password display
```

## Plugin Structure

```
pearpass-claude-plugin/
├── .claude-plugin/
│   └── plugin.json       # Manifest
├── skills/
│   ├── build/SKILL.md    # Vite build guidance
│   ├── test/SKILL.md     # Jest testing guidance
│   └── extension/SKILL.md # Extension dev guidance
├── agents/
│   ├── security-reviewer.md
│   ├── i18n-helper.md
│   └── component-generator.md
└── commands/
    ├── pearpass-dev.md
    ├── pearpass-review.md
    └── pearpass-release.md
```

## PearPass Technology Stack

- **Frontend:** React + Vite (multi-config build)
- **Styling:** Tailwind CSS
- **i18n:** LinguiJS (`@lingui/react/macro`, `@lingui/core/macro`)
- **Testing:** Jest
- **Crypto:** pearpass-lib-vault

## License

[Apache 2.0](LICENSE)
