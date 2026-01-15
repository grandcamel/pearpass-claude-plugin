---
name: test
description: Run Jest tests for PearPass browser extension. Supports running all tests, specific test files, watch mode, and coverage reports.
user_invocable: true
---

# PearPass Test Skill

You are helping run tests for the PearPass browser extension which uses Jest as its testing framework.

## Test Commands

### Run All Tests
```bash
npm test
```

### Run Tests in Watch Mode
```bash
npm test -- --watch
```

### Run Specific Test File
```bash
npm test -- path/to/test.spec.js
```

### Run Tests with Coverage
```bash
npm test -- --coverage
```

### Run Tests Matching Pattern
```bash
npm test -- --testNamePattern="pattern"
```

### Run Tests for Changed Files Only
```bash
npm test -- --onlyChanged
```

## Instructions

1. **Determine what the user needs:**
   - Run all tests → `npm test`
   - Test specific component → `npm test -- <path>`
   - Development mode → `npm test -- --watch`
   - Coverage report → `npm test -- --coverage`

2. **Analyze test failures:**
   - Read the error messages carefully
   - Check for missing mocks (browser APIs, crypto)
   - Verify test setup and teardown

3. **Common test patterns in PearPass:**
   - Vault operations tests (encryption/decryption)
   - UI component tests (React Testing Library)
   - Background script message handling
   - Content script DOM manipulation

## Mocking Browser APIs

PearPass tests need mocks for:
- `chrome.runtime` - Extension messaging
- `chrome.storage` - Local/sync storage
- `chrome.tabs` - Tab management
- `window.crypto` - Web Crypto API

## Test File Locations

Tests are typically located:
- `src/**/*.test.js` - Unit tests alongside source
- `src/**/*.spec.js` - Integration tests
- `__tests__/` - Dedicated test directories

## Coverage Thresholds

When running coverage, check:
- Statement coverage
- Branch coverage
- Function coverage
- Line coverage

Report issues if coverage drops below project thresholds.
