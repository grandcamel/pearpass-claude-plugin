---
name: extension
description: |
  Provides guidance for browser extension development tasks in PearPass.
  Use this skill when the user asks to "load the extension", "debug manifest", "fix extension errors",
  "reload extension", "check permissions", or troubleshoot Chrome/Firefox/Edge extension issues.
---

# PearPass Extension Development Skill

Handle browser extension-specific development tasks for PearPass.

## Loading the Extension

### Chrome/Chromium
1. Navigate to `chrome://extensions/`
2. Enable "Developer mode" (top right toggle)
3. Click "Load unpacked"
4. Select the `dist/` directory

### Firefox
1. Navigate to `about:debugging#/runtime/this-firefox`
2. Click "Load Temporary Add-on..."
3. Select `dist/manifest.json`

### Edge
1. Navigate to `edge://extensions/`
2. Enable "Developer mode"
3. Click "Load unpacked"
4. Select the `dist/` directory

## Reloading After Changes

After running a build:
1. Go to the extensions page
2. Click the reload icon on the PearPass extension
3. Or use keyboard shortcut (if configured)

## Manifest Validation

Check `dist/manifest.json` for:
- Correct `manifest_version` (should be 3)
- Valid `permissions` array
- Proper `background.service_worker` path
- Content script `matches` patterns
- Web accessible resources

## Common Extension Issues

### "Service worker registration failed"
- Check `background.js` for syntax errors
- Verify the path in manifest is correct
- Check browser console for detailed errors

### Content scripts not running
- Verify URL matches patterns in manifest
- Check for CSP violations
- Ensure scripts are listed in `web_accessible_resources`

### Popup not showing
- Check popup path in `action.default_popup`
- Look for JavaScript errors in popup console
- Verify popup HTML file exists in dist

### Permission errors
- Add required permissions to manifest
- Check for `host_permissions` for specific sites
- Some APIs need `activeTab` permission

## Debugging Tools

### Background Service Worker
```
chrome://extensions/ → Details → Inspect views: service worker
```

### Content Scripts
```
Right-click page → Inspect → Console (filter by extension ID)
```

### Popup
```
Right-click extension icon → Inspect popup
```

## Extension API Reference

Key APIs used by PearPass:
- `chrome.runtime` - Messaging, lifecycle
- `chrome.storage.local` - Local encrypted storage
- `chrome.tabs` - Tab interaction
- `chrome.scripting` - Dynamic script injection
- `chrome.action` - Toolbar button/popup

## Security Checklist

For PearPass, always verify:
- [ ] No sensitive data in logs
- [ ] Proper CSP headers
- [ ] Secure message passing
- [ ] No eval() or inline scripts
- [ ] HTTPS-only external requests
