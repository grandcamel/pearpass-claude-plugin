---
name: build
description: Build PearPass browser extension with Vite multi-config system. Use for running specific builds (background, content, inject, main), watch mode, or full production builds.
user_invocable: true
---

# PearPass Build Skill

You are helping build the PearPass browser extension which uses a multi-configuration Vite build system.

## Build Configurations

The project has four separate Vite configurations:

| Config | File | Purpose |
|--------|------|---------|
| background | `vite.config.background.js` | Service worker for extension background |
| content | `vite.config.content.js` | Content scripts injected into pages |
| inject | `vite.config.inject.js` | Scripts injected into page context |
| main | `vite.config.main.js` | Main extension UI (popup, options) |

## Available Commands

### Build All (Production)
```bash
npm run build
```

### Build with Watch Mode (Development)
```bash
npm run build:watch
```

### Build Specific Configuration
```bash
npx vite build --config vite.config.background.js
npx vite build --config vite.config.content.js
npx vite build --config vite.config.inject.js
npx vite build --config vite.config.main.js
```

## Instructions

1. **Determine what the user needs:**
   - Full build → Run `npm run build`
   - Development with auto-reload → Run `npm run build:watch`
   - Specific component → Run the appropriate vite build command

2. **Check for build errors:**
   - TypeScript/JavaScript syntax errors
   - Missing dependencies
   - Vite configuration issues

3. **After successful build:**
   - Output is in the `dist/` directory
   - Remind user to reload the extension in browser if testing

## Common Issues

- **Module not found**: Run `npm install` first
- **Submodule issues**: Run `git submodule update --init --recursive`
- **Port conflicts**: Check if another Vite process is running

## Output Location

All builds output to `dist/` directory:
- `dist/background.js` - Background service worker
- `dist/content.js` - Content scripts
- `dist/inject.js` - Injection scripts
- `dist/popup/` - Popup UI
- `dist/manifest.json` - Extension manifest
