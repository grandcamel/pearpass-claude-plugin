---
name: pearpass-dev
description: Start PearPass development environment with watch builds and helpful setup instructions
user_invocable: true
arguments:
  - name: target
    description: "Specific build target: all, background, content, inject, main"
    required: false
    default: "all"
---

# PearPass Development Environment

You are setting up the PearPass development environment for the user.

## Steps to Execute

### 1. Check Prerequisites

First, verify the environment:

```bash
# Check Node.js version
node --version

# Check npm version
npm --version

# Verify in correct directory
ls package.json
```

### 2. Install Dependencies

If needed:

```bash
# Install dependencies
npm install

# Initialize submodules (pearpass-lib-vault)
git submodule update --init --recursive
```

### 3. Start Development Build

Based on the `target` argument:

**All targets (default):**
```bash
npm run build:watch
```

**Specific target:**
```bash
npx vite build --config vite.config.{{target}}.js --watch
```

### 4. Provide Browser Loading Instructions

After build starts, tell the user:

---

**Development build is running!**

To load the extension in your browser:

**Chrome:**
1. Go to `chrome://extensions/`
2. Enable "Developer mode" (top right)
3. Click "Load unpacked"
4. Select the `dist/` folder

**Firefox:**
1. Go to `about:debugging#/runtime/this-firefox`
2. Click "Load Temporary Add-on"
3. Select `dist/manifest.json`

**Tips:**
- Changes will auto-rebuild with watch mode
- Click reload on the extension after rebuilds
- Check the service worker console for background script logs
- Use browser DevTools for popup/content script debugging

---

### 5. Common Development Tasks

Remind the user of available commands:

| Command | Description |
|---------|-------------|
| `npm test` | Run tests |
| `npm run build` | Production build |
| `npx lingui extract` | Extract i18n strings |

## Troubleshooting

If build fails:
1. Check for syntax errors in output
2. Verify all dependencies installed
3. Check submodule is initialized
4. Look for port conflicts if Vite fails to start

## Output

After starting, confirm:
- Build process is running
- Which config(s) are being watched
- How to reload after changes
