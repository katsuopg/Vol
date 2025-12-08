# CLAUDE.md - AI Assistant Guidelines for Vol

This document provides essential context for AI assistants working with this codebase.

## Project Overview

**Repository:** Vol
**Status:** New repository (initialized, awaiting initial development)
**Last Updated:** December 2024

Vol is a new project repository. This CLAUDE.md file establishes foundational conventions and should be updated as the project evolves.

---

## Repository Structure

```
Vol/
├── CLAUDE.md          # AI assistant guidelines (this file)
└── .git/              # Git repository data
```

> **Note:** This structure should be updated as source files and directories are added to the project.

---

## Development Setup

### Prerequisites

<!-- Update this section when dependencies are established -->
- Git

### Getting Started

```bash
# Clone the repository
git clone <repository-url>
cd Vol

# Additional setup steps to be documented as project develops
```

---

## Development Workflow

### Branching Strategy

- **Main branch:** Primary development branch
- **Feature branches:** Use descriptive names (e.g., `feature/add-authentication`)
- **Bug fix branches:** Prefix with `fix/` (e.g., `fix/login-error`)

### Commit Messages

Follow conventional commit format:
```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

Types:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

### Pull Request Guidelines

1. Create feature branch from main
2. Make changes with clear, atomic commits
3. Ensure all tests pass (when applicable)
4. Update documentation as needed
5. Submit PR with clear description

---

## Code Style & Conventions

<!-- Update this section based on the primary language(s) used -->

### General Principles

- Write clean, readable, self-documenting code
- Follow DRY (Don't Repeat Yourself) principles
- Prefer simplicity over complexity
- Add comments only when logic isn't self-evident
- Keep functions focused and single-purpose

### Naming Conventions

- Use descriptive, meaningful names
- Be consistent with the existing codebase style
- Avoid abbreviations unless widely understood

---

## Testing

<!-- Update when testing framework is established -->

### Running Tests

```bash
# Commands to be documented when testing is set up
```

### Writing Tests

- Write tests for new features
- Maintain existing test coverage
- Follow the existing test patterns in the codebase

---

## Common Tasks

### Task 1: [To be defined]

```bash
# Commands for common task
```

---

## AI Assistant Guidelines

### Working with This Codebase

1. **Read before modifying:** Always read relevant files before making changes
2. **Understand context:** Explore related files to understand patterns and conventions
3. **Minimal changes:** Make only the changes necessary to complete the task
4. **Preserve style:** Match existing code style and patterns
5. **Test changes:** Run tests after modifications when available

### File Operations

- Prefer editing existing files over creating new ones
- Don't create documentation files unless explicitly requested
- Keep changes focused and atomic

### Git Operations

- Create clear, descriptive commit messages
- Commit logical units of work
- Don't push to main/master without explicit permission
- Always verify branch before pushing

### What to Avoid

- Don't add unnecessary features or "improvements"
- Don't refactor code that isn't directly related to the task
- Don't add error handling for impossible scenarios
- Don't create abstractions for one-time operations
- Don't guess at requirements - ask for clarification

### Security Considerations

- Never commit secrets, API keys, or credentials
- Be cautious with user input handling
- Follow OWASP security guidelines
- Report potential security issues immediately

---

## Environment Variables

<!-- Document required environment variables when applicable -->

| Variable | Description | Required |
|----------|-------------|----------|
| (none yet) | | |

---

## Troubleshooting

### Common Issues

<!-- Document common issues and solutions as they arise -->

1. **Issue:** [Description]
   - **Solution:** [Steps to resolve]

---

## Additional Resources

- [Project Documentation](#) (to be added)
- [Contributing Guidelines](#) (to be added)

---

## Changelog

| Date | Changes |
|------|---------|
| December 2024 | Initial CLAUDE.md created |

---

*This file should be updated as the project evolves. When adding new features, dependencies, or workflows, update the relevant sections.*
