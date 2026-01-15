# Contributing to PearPass Claude Code Plugin

Thank you for your interest in contributing to the pearpass-dev plugin!

## Getting Started

### Prerequisites

- Claude Code CLI installed
- Familiarity with [Claude Code plugins](https://docs.anthropic.com/claude-code/plugins)
- Understanding of PearPass browser extension architecture

### Setup

1. Clone this repository:
   ```bash
   git clone <repo-url>
   cd pearpass-claude-plugin
   ```

2. Install the plugin locally:
   ```bash
   claude plugins add .
   ```

3. Test in a PearPass project:
   ```bash
   cd /path/to/pearpass-app-browser-extension
   claude
   ```

## Project Structure

```
pearpass-claude-plugin/
├── plugin.json          # Plugin manifest
├── skills/              # Contextual guidance
│   ├── build.md
│   ├── test.md
│   └── extension.md
├── agents/              # Specialized assistants
│   ├── security-reviewer.md
│   ├── i18n-helper.md
│   └── component-generator.md
├── commands/            # Slash commands
│   ├── pearpass-dev.md
│   ├── pearpass-review.md
│   └── pearpass-release.md
└── docs/                # Documentation
    ├── USAGE.md
    └── EXAMPLES.md
```

## Contributing Guidelines

### Adding a New Skill

1. Create a new file in `skills/`:
   ```markdown
   ---
   name: skill-name
   description: Brief description of what this skill helps with
   user_invocable: true
   ---

   # Skill Title

   Detailed instructions for Claude...
   ```

2. Add the file path to `plugin.json`:
   ```json
   "skills": [
     "skills/existing.md",
     "skills/skill-name.md"
   ]
   ```

3. Test the skill by triggering it in conversation

### Adding a New Agent

1. Create a new file in `agents/`:
   ```markdown
   ---
   name: agent-name
   description: What this agent specializes in
   tools:
     - Glob
     - Grep
     - Read
   color: blue
   model: inherit
   ---

   # Agent Title

   System prompt and instructions...
   ```

2. Add to `plugin.json`

3. Test by invoking the agent

### Adding a New Command

1. Create a new file in `commands/`:
   ```markdown
   ---
   name: command-name
   description: What this command does
   user_invocable: true
   arguments:
     - name: arg1
       description: Argument description
       required: false
       default: "value"
   ---

   # Command Title

   Steps to execute...
   ```

2. Add to `plugin.json`

3. Test with `/command-name`

## Code Standards

### Markdown Frontmatter

- Use YAML format
- Include all required fields
- Keep descriptions concise but informative

### Content Guidelines

- Write clear, actionable instructions
- Include code examples where helpful
- Consider security implications (PearPass handles passwords)
- Support i18n patterns with LinguiJS
- Follow existing component patterns

### Security Focus

Since PearPass handles sensitive data:

- Never suggest logging passwords or keys
- Always recommend secure patterns
- Include security checks in code generation
- Follow OWASP guidelines for extensions

## Testing Changes

### Manual Testing

1. Install the modified plugin
2. Open Claude Code in a PearPass project
3. Test affected skills/agents/commands
4. Verify expected behavior

### Checklist

- [ ] Frontmatter is valid YAML
- [ ] All file paths in plugin.json exist
- [ ] Commands work with and without arguments
- [ ] Agents have appropriate tool access
- [ ] No security anti-patterns suggested

## Submitting Changes

### Pull Request Process

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

### PR Description

Include:
- What the change does
- Why it's needed
- How to test it
- Any breaking changes

### Review Criteria

PRs will be reviewed for:
- Correctness and completeness
- Security considerations
- Alignment with PearPass patterns
- Documentation quality

## Reporting Issues

### Bug Reports

Include:
- Steps to reproduce
- Expected behavior
- Actual behavior
- Claude Code version
- Plugin version

### Feature Requests

Describe:
- The problem you're solving
- Your proposed solution
- Alternative approaches considered

## Questions?

- Open an issue for discussion
- Check existing documentation
- Review the PearPass extension repo for context

## License

By contributing, you agree that your contributions will be licensed under Apache 2.0.
