# Code Review Expert

A comprehensive code review skill for AI agents. Performs structured reviews with a senior engineer lens, covering architecture, security, performance, and code quality.

## Installation

```bash
npx skills add sanyuan0704/code-review-expert
```

## Features

- **SOLID Principles** - Detect SRP, OCP, LSP, ISP, DIP violations
- **Security Scan** - XSS, injection, SSRF, race conditions, auth gaps, secrets leakage
- **Performance** - N+1 queries, CPU hotspots, missing cache, memory issues
- **Error Handling** - Swallowed exceptions, async errors, missing boundaries
- **Boundary Conditions** - Null handling, empty collections, off-by-one, numeric limits
- **Removal Planning** - Identify dead code with safe deletion plans

## Usage

After installation, simply run:

```bash
# Use default model (gpt-4o)
/code-review-expert

# Use a specific model
/code-review-expert --model gpt-4o-mini
/code-review-expert --model claude-3-5-sonnet
/code-review-expert --model claude-3-5-haiku
```

The skill will automatically review your current git changes.

### Model Selection

Choose the right model for your needs:

| Scenario | Recommended Model | Why |
|----------|------------------|-----|
| **Large PR (>500 lines)** | `claude-3-5-sonnet` | Better context handling |
| **Quick review** | `gpt-4o-mini` or `claude-3-5-haiku` | Faster feedback |
| **Security-critical** | `gpt-4o` or `claude-3-5-sonnet` | Thorough analysis |
| **General use** | `gpt-4o` (default) | Balanced performance |

## Workflow

1. **Preflight** - Scope changes via `git diff`
2. **SOLID + Architecture** - Check design principles
3. **Removal Candidates** - Find dead/unused code
4. **Security Scan** - Vulnerability detection
5. **Code Quality** - Error handling, performance, boundaries
6. **Output** - Findings by severity (P0-P3)
7. **Confirmation** - Ask user before implementing fixes

## Severity Levels

| Level | Name | Action |
|-------|------|--------|
| P0 | Critical | Must block merge |
| P1 | High | Should fix before merge |
| P2 | Medium | Fix or create follow-up |
| P3 | Low | Optional improvement |

## Structure

```
code-review-expert/
├── SKILL.md                 # Main skill definition
├── agents/
│   └── agent.yaml           # Agent interface config
└── references/
    ├── solid-checklist.md   # SOLID smell prompts
    ├── security-checklist.md    # Security & reliability
    ├── code-quality-checklist.md # Error, perf, boundaries
    └── removal-plan.md      # Deletion planning template
```

## References

Each checklist provides detailed prompts and anti-patterns:

- **solid-checklist.md** - SOLID violations + common code smells
- **security-checklist.md** - OWASP risks, race conditions, crypto, supply chain
- **code-quality-checklist.md** - Error handling, caching, N+1, null safety
- **removal-plan.md** - Safe vs deferred deletion with rollback plans

## License

MIT
