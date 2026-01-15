---
name: pearpass-release
description: Prepare PearPass for release. Run tests, build production bundle, validate manifest, and generate changelog.
user_invocable: true
arguments:
  - name: version
    description: "Version number for release (e.g., 1.2.0)"
    required: false
  - name: skip-tests
    description: "Skip test suite (not recommended)"
    required: false
    default: "false"
---

# PearPass Release Preparation

You are preparing PearPass browser extension for release.

## Release Checklist

### 1. Pre-flight Checks

```bash
# Ensure clean working directory
git status

# Check current version
cat package.json | grep '"version"'

# Verify on correct branch
git branch --show-current
```

### 2. Run Test Suite

Unless `skip-tests` is true:

```bash
# Run all tests
npm test

# Run with coverage
npm test -- --coverage
```

**Requirements:**
- All tests must pass
- No console errors
- Coverage meets thresholds

### 3. Production Build

```bash
# Clean previous build
rm -rf dist/

# Run production build
npm run build

# Verify build output
ls -la dist/
```

### 4. Manifest Validation

Check `dist/manifest.json`:

```bash
# Display manifest
cat dist/manifest.json
```

**Verify:**
- [ ] Correct version number
- [ ] All required fields present
- [ ] Permissions are minimal
- [ ] Icons exist at specified paths
- [ ] Background script path correct
- [ ] Content script matches correct

### 5. Update Version (if provided)

If `version` argument provided:

```bash
# Update package.json
npm version {{version}} --no-git-tag-version

# Update manifest.json version
# (may need manual edit or script)
```

### 6. Generate Changelog

Review commits since last release:

```bash
# Get last tag
git describe --tags --abbrev=0

# Commits since last tag
git log $(git describe --tags --abbrev=0)..HEAD --oneline
```

**Changelog format:**
```markdown
## [X.Y.Z] - YYYY-MM-DD

### Added
- New feature description

### Changed
- Updated functionality

### Fixed
- Bug fix description

### Security
- Security improvements
```

### 7. Security Scan

```bash
# Check for known vulnerabilities
npm audit

# Check for secrets in code
grep -rn "password\s*=" --include="*.js" dist/
```

### 8. Final Validation

**Manual checks:**
- [ ] Load extension in Chrome
- [ ] Load extension in Firefox
- [ ] Test core functionality:
  - [ ] Create vault
  - [ ] Add password entry
  - [ ] Autofill works
  - [ ] Popup opens correctly
- [ ] No console errors

### 9. Package for Distribution

```bash
# Create zip for Chrome Web Store
cd dist && zip -r ../pearpass-extension-v{{version}}.zip . && cd ..

# Firefox uses the same zip
```

## Output

Provide release summary:

```markdown
# Release Preparation Complete

**Version:** X.Y.Z
**Date:** YYYY-MM-DD

## Build Info
- Build size: X KB
- Files: X

## Test Results
- Tests: X passed, X failed
- Coverage: X%

## Changelog
[Generated changelog]

## Artifacts
- `dist/` - Unpacked extension
- `pearpass-extension-vX.Y.Z.zip` - Distribution package

## Next Steps
1. Create git tag: `git tag vX.Y.Z`
2. Push tag: `git push origin vX.Y.Z`
3. Upload to Chrome Web Store
4. Upload to Firefox Add-ons
5. Create GitHub release with changelog
```

## Store Submission Notes

**Chrome Web Store:**
- Requires developer account ($5 one-time)
- Review takes 1-3 days
- Update existing listing or create new

**Firefox Add-ons:**
- Requires Mozilla account (free)
- Review typically faster
- Source code may be requested
