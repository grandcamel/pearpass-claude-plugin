# PearPass Claude Code Plugin - Planning Document

## Project Research Summary

### About PearPass Browser Extension

PearPass is an open-source browser extension password manager with:
- Peer-to-peer syncing and end-to-end encryption
- Integration with PearPass desktop application
- Support for logins, identities, credit cards, notes, and passkeys

### Technology Stack

| Component | Technology |
|-----------|------------|
| Frontend | React |
| Build Tool | Vite (multi-config) |
| Styling | Tailwind CSS |
| i18n | LinguiJS |
| Testing | Jest |
| Crypto | pearpass-lib-vault |
| Language | JavaScript (98.8%) |

### Architecture

The extension uses separate Vite configurations for:
- `vite.config.background.js` - Background service worker
- `vite.config.content.js` - Content scripts
- `vite.config.inject.js` - Injection scripts
- `vite.config.main.js` - Main UI

Repository structure includes `packages/` (monorepo), `public/`, `scripts/`, and `src/`.

---

## Plugin Design

### Phase 1: Core Skills

#### 1. `pearpass:build` - Build Management
- Run specific Vite builds (background, content, inject, main)
- Watch mode for development
- Build all configurations

#### 2. `pearpass:test` - Testing Workflow
- Run Jest tests
- Watch mode
- Coverage reporting
- Test specific components

#### 3. `pearpass:extension` - Extension Development
- Load extension in browser
- Reload after changes
- Debug manifest issues
- Check extension permissions

### Phase 2: Specialized Agents

#### 1. `pearpass:security-reviewer`
- Review crypto operations for vulnerabilities
- Check vault operations usage
- Audit password handling
- Validate encryption implementations

#### 2. `pearpass:i18n-helper`
- Extract strings for translation
- Validate LinguiJS usage
- Check for hardcoded strings
- Generate translation templates

#### 3. `pearpass:component-generator`
- Generate React components following project patterns
- Create content script boilerplate
- Scaffold background service handlers

### Phase 3: Commands

#### 1. `/pearpass-dev`
- Quick development environment setup
- Start watch builds
- Open browser with extension loaded

#### 2. `/pearpass-review`
- Security-focused code review
- Check for common extension vulnerabilities
- Validate CSP compliance

#### 3. `/pearpass-release`
- Build production bundle
- Run full test suite
- Generate changelog

---

## Implementation Tasks

### Setup
- [x] Create plugin.json manifest
- [x] Set up directory structure
- [ ] Create .mcp.json if needed

### Skills
- [x] Implement build skill
- [x] Implement test skill
- [x] Implement extension skill

### Agents
- [x] Create security reviewer agent
- [x] Create i18n helper agent
- [x] Create component generator agent

### Commands
- [x] Create /pearpass-dev command
- [x] Create /pearpass-review command
- [x] Create /pearpass-release command

### Documentation
- [x] Write usage documentation (docs/USAGE.md)
- [x] Add examples (docs/EXAMPLES.md)
- [x] Create contribution guide (CONTRIBUTING.md)

---

## Security Considerations

Since PearPass handles sensitive data (passwords, credentials), the plugin should:

1. **Never log or expose** vault contents, passwords, or encryption keys
2. **Emphasize security review** in all code generation
3. **Follow OWASP guidelines** for browser extension security
4. **Validate crypto patterns** against pearpass-lib-vault best practices

---

## References

- [PearPass Browser Extension](https://github.com/tetherto/pearpass-app-browser-extension)
- [Chrome Extension Development](https://developer.chrome.com/docs/extensions/)
- [Vite Build Tool](https://vitejs.dev/)
- [LinguiJS](https://lingui.dev/)
- [Claude Code Plugin Development](https://docs.anthropic.com/claude-code/plugins)
