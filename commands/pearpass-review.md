---
name: pearpass-review
description: Security-focused code review for PearPass changes. Checks for vulnerabilities, crypto issues, and extension security problems.
user_invocable: true
arguments:
  - name: scope
    description: "Review scope: staged (git staged files), branch (current branch changes), all (full codebase), or a file path"
    required: false
    default: "staged"
---

# PearPass Security Review

You are performing a security-focused code review on PearPass.

## Review Scope

Based on the `scope` argument:

**staged (default):** Review git staged changes
```bash
git diff --cached --name-only
```

**branch:** Review all changes on current branch vs main
```bash
git diff main...HEAD --name-only
```

**all:** Review entire codebase (focus on security-critical files)

**file path:** Review specific file or directory

## Security Review Checklist

### 1. Credential & Secret Handling

Search for potential leaks:
```bash
# Check for console.log with sensitive data
grep -rn "console\.\(log\|debug\|info\)" --include="*.js" --include="*.jsx" | grep -iE "password|secret|key|token|credential"

# Check for hardcoded secrets
grep -rn "password\s*[:=]" --include="*.js" --include="*.jsx"
```

**Verify:**
- [ ] No passwords/keys in logs
- [ ] No hardcoded credentials
- [ ] Secrets cleared after use
- [ ] Secure comparison for auth

### 2. Cryptographic Operations

Check vault library usage:
```bash
# Find crypto-related code
grep -rn "pearpass-lib-vault\|crypto\|encrypt\|decrypt" --include="*.js"
```

**Verify:**
- [ ] Proper encryption modes (AEAD)
- [ ] Random IV/nonce generation
- [ ] No key reuse
- [ ] Proper key derivation

### 3. Extension Security

Check manifest and CSP:
```bash
# Review manifest permissions
cat dist/manifest.json | grep -A 20 "permissions"

# Check for dangerous patterns
grep -rn "eval\|innerHTML\|outerHTML" --include="*.js" --include="*.jsx"
```

**Verify:**
- [ ] Minimal permissions
- [ ] No eval() usage
- [ ] Safe DOM manipulation
- [ ] Validated message passing

### 4. Input Validation

```bash
# Find user input handling
grep -rn "getElementById\|querySelector\|value" --include="*.js"
```

**Verify:**
- [ ] URL validation
- [ ] Input sanitization
- [ ] XSS prevention
- [ ] Injection protection

### 5. Storage Security

```bash
# Check storage usage
grep -rn "localStorage\|sessionStorage\|chrome\.storage" --include="*.js"
```

**Verify:**
- [ ] Sensitive data encrypted
- [ ] No localStorage for secrets
- [ ] Proper chrome.storage.local usage

## Output Format

Provide a structured report:

```markdown
# PearPass Security Review

**Scope:** [staged/branch/all/path]
**Date:** [current date]
**Files Reviewed:** [count]

## Summary
- Critical: X
- High: X
- Medium: X
- Low: X

## Findings

### [CRITICAL] Issue Title
**File:** path/to/file.js:123
**Issue:** Description
**Impact:** What could be exploited
**Fix:** Recommended solution

### [HIGH] Issue Title
...

## Passed Checks
- ✅ Check that passed
- ✅ Another passing check

## Recommendations
1. Priority fixes
2. Improvements to consider
```

## Severity Definitions

| Level | Definition | Example |
|-------|------------|---------|
| CRITICAL | Immediate exploitation risk, data exposure | Password logged to console |
| HIGH | Significant vulnerability | Missing input validation |
| MEDIUM | Security weakness | Overly broad permissions |
| LOW | Best practice violation | Missing error handling |

## After Review

Suggest next steps:
1. Fix critical/high issues before merge
2. Create issues for medium/low items
3. Re-run review after fixes
