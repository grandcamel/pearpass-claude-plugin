# PearPass Plugin Examples

Practical examples of using the pearpass-dev plugin.

## Development Workflows

### Example 1: Starting a New Feature

**Scenario:** Adding a password generator to the popup.

```
User: I want to add a password generator feature to the popup

Claude: I'll help you create a password generator. Let me first understand
the existing popup structure...

[Claude explores src/popup/ to understand patterns]

Let me generate a component that follows your existing patterns:

[Uses component-generator agent to scaffold PasswordGenerator.jsx]

The component has been created at src/popup/components/PasswordGenerator.jsx.
It includes:
- Configurable length slider
- Character type toggles (uppercase, lowercase, numbers, symbols)
- Copy to clipboard functionality
- Proper i18n wrapping with <Trans>

Would you like me to integrate it into the popup main view?
```

### Example 2: Security Review Before PR

**Scenario:** Reviewing changes before creating a pull request.

```
User: /pearpass-review scope=branch

Claude: # PearPass Security Review

**Scope:** branch (vs main)
**Files Changed:** 8

## Summary
- Critical: 0
- High: 0
- Medium: 1
- Low: 2

## Findings

### [MEDIUM] Potential timing attack in password comparison
**File:** src/auth/verify.js:45
**Issue:** Using `===` for password comparison
**Impact:** Timing side-channel could leak password length
**Fix:** Use constant-time comparison from pearpass-lib-vault

### [LOW] Console.log in production code
**File:** src/popup/Login.jsx:23
**Issue:** Debug log statement left in code
**Fix:** Remove or wrap in development check

### [LOW] Missing input sanitization
**File:** src/content/form-detector.js:89
**Issue:** URL not validated before use
**Fix:** Validate URL format before processing

## Passed Checks
- ✅ No hardcoded secrets
- ✅ Proper vault library usage
- ✅ Chrome storage API used correctly
- ✅ No eval() or innerHTML

## Recommendations
1. Fix the timing attack issue before merge
2. Add URL validation utility
3. Consider adding ESLint rule for console.log
```

### Example 3: Internationalization Audit

**Scenario:** Checking translation coverage before release.

```
User: Check if all strings in the popup are translated

Claude: [Uses i18n-helper agent]

# i18n Audit: src/popup/

## Hardcoded Strings Found

### src/popup/Settings.jsx:34
**Text:** "Save Changes"
**Fix:**
```jsx
<button><Trans>Save Changes</Trans></button>
```

### src/popup/VaultList.jsx:67
**Text:** "No passwords saved yet"
**Fix:**
```jsx
<p><Trans>No passwords saved yet</Trans></p>
```

### src/popup/Header.jsx:12
**Text:** "PearPass"
**Status:** OK - Brand name, no translation needed

## Summary
- Files scanned: 12
- Hardcoded strings: 2 (need wrapping)
- Properly wrapped: 45
- Coverage: 95.7%

Would you like me to fix these strings automatically?
```

## Build Scenarios

### Example 4: Debugging Build Failure

**Scenario:** Build fails with cryptic error.

```
User: The build is failing, can you help?

Claude: Let me run the build and analyze the error.

[Runs npm run build]

Build failed with:
Error: Cannot find module 'pearpass-lib-vault'

This typically happens when the git submodule isn't initialized.
Let me fix this:

[Runs git submodule update --init --recursive]

Submodule initialized. Running build again...

[Runs npm run build]

Build succeeded! Output in dist/:
- background.js (45 KB)
- content.js (12 KB)
- inject.js (8 KB)
- popup/ (156 KB)

The extension is ready to load in your browser.
```

### Example 5: Building Specific Target

**Scenario:** Only need to rebuild background script.

```
User: /pearpass-dev target=background

Claude: Starting background script build in watch mode...

[Runs npx vite build --config vite.config.background.js --watch]

Background build watching for changes.

To test:
1. Go to chrome://extensions/
2. Find PearPass and click the reload icon
3. Check service worker console for logs

Changes to src/background/ will auto-rebuild.
Press Ctrl+C when done developing.
```

## Testing Scenarios

### Example 6: Running Specific Tests

**Scenario:** Running tests for a specific module.

```
User: Run tests for the vault encryption module

Claude: [Uses test skill]

Running tests for vault module...

[Runs npm test -- --testPathPattern="vault" --coverage]

Test Results:
 PASS src/vault/encryption.test.js
  ✓ encrypts data with master password (45ms)
  ✓ decrypts data correctly (23ms)
  ✓ fails with wrong password (12ms)
  ✓ generates unique IVs (8ms)
  ✓ handles empty data (5ms)

 PASS src/vault/storage.test.js
  ✓ saves encrypted vault (34ms)
  ✓ loads and decrypts vault (28ms)
  ✓ handles missing vault (6ms)

Coverage:
- Statements: 94.2%
- Branches: 88.5%
- Functions: 100%
- Lines: 94.2%

All 8 tests passed!
```

## Release Scenarios

### Example 7: Full Release Workflow

**Scenario:** Preparing version 1.2.0 for release.

```
User: /pearpass-release version=1.2.0

Claude: # Release Preparation: v1.2.0

## Pre-flight Checks
✓ Clean working directory
✓ On branch: release/1.2.0
✓ Current version: 1.1.0

## Test Suite
Running tests...
✓ 47 tests passed
✓ Coverage: 91.3%

## Production Build
Building...
✓ background.js (42 KB, gzipped: 14 KB)
✓ content.js (11 KB, gzipped: 4 KB)
✓ inject.js (7 KB, gzipped: 2 KB)
✓ popup/ (148 KB, gzipped: 45 KB)

## Manifest Validation
✓ Version updated to 1.2.0
✓ All permissions valid
✓ Icons present
✓ Content script matches correct

## Security Scan
✓ npm audit: 0 vulnerabilities
✓ No secrets in build

## Changelog

### [1.2.0] - 2026-01-15

#### Added
- Password generator in popup
- Keyboard shortcuts for autofill

#### Fixed
- Form detection on dynamic pages
- Memory leak in content script

#### Security
- Updated encryption library to v2.1.0

## Artifacts Created
- dist/ (unpacked extension)
- pearpass-extension-v1.2.0.zip (ready for upload)

## Next Steps
1. git tag v1.2.0
2. git push origin v1.2.0
3. Upload to Chrome Web Store
4. Upload to Firefox Add-ons
5. Create GitHub release
```

## Component Generation

### Example 8: Creating a Content Script

**Scenario:** Adding form autofill detection.

```
User: Create a content script that detects login forms on pages

Claude: [Uses component-generator agent]

I'll create a content script for login form detection following
your existing patterns.

Created: src/content/login-detector.js

```javascript
/**
 * Content Script: login-detector
 * Detects login forms and injects autofill UI
 */
(function() {
  'use strict';

  const LOGIN_SELECTORS = [
    'input[type="password"]',
    'input[name*="pass"]',
    'input[autocomplete="current-password"]'
  ];

  function findLoginForms() {
    const passwordFields = document.querySelectorAll(
      LOGIN_SELECTORS.join(',')
    );
    return Array.from(passwordFields).map(field => {
      const form = field.closest('form');
      return { form, passwordField: field };
    });
  }

  function injectAutofillIcon(field) {
    // Implementation following existing icon injection pattern
  }

  // ... rest of implementation
})();
```

Don't forget to:
1. Add to vite.config.content.js
2. Update manifest.json content_scripts
3. Add corresponding tests
```
