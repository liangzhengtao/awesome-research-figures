# Contributing to Awesome Research Figures

Thank you for your interest in contributing! This project welcomes contributions from researchers, engineers, and designers who want to improve scientific figure quality.

## How to Contribute

### Adding a New Skill

1. Fork this repository
2. Create a new branch: `git checkout -b add-skill/my-new-skill`
3. Add your skill file in the appropriate `skills/` subdirectory
4. Ensure your skill file includes all required sections (see template below)
5. Submit a Pull Request

### Skill File Template

Every skill file must include these sections:

```markdown
# Skill Title

## When to Use
- Clear trigger conditions

## Tools and Libraries
- Exact install commands

## Step-by-step Instructions
1. Setup
2. Configuration
3. Usage

## Code Templates
- Complete, runnable examples
- Language-appropriate (Python/R/LaTeX)

## Style Specifications
| Parameter | Value |
|-----------|-------|

## Common Pitfalls
1. Issue → Solution format

## Journal-Specific Tips
- Per-journal guidance
```

### Improving Existing Skills

- Fix code bugs or outdated API usage
- Add new journal specifications
- Improve code templates with better defaults
- Add missing common pitfalls

### Reporting Issues

- Use the [Issue Tracker](https://github.com/ai-era/awesome-research-figures/issues)
- Include the skill file name, tool version, and expected vs actual behavior
- Attach screenshots for visual issues

## Code of Conduct

Please read our [Code of Conduct](CODE_OF_CONDUCT.md) before contributing.

## Style Guidelines

- **Markdown**: Use ATX-style headers (`#`, `##`, `###`)
- **Code blocks**: Always specify the language (` ```python `, ` ```r `, ` ```latex `)
- **Tables**: Use Markdown table syntax, align columns consistently
- **Colors**: Always provide hex codes (e.g., `#0072B2`)
- **Units**: Use metric (mm, cm) and inches together for figure sizes
- **Font names**: Use standard names (Times New Roman, Arial, Helvetica)

## Pull Request Process

1. Update the README.md if adding a new skill (add to the skills table)
2. Ensure all code templates are syntactically correct
3. Test code templates in the target environment
4. One skill per PR (keep changes focused)
5. PR title format: `Add [category]: skill-name` or `Fix [category]: skill-name`

## Questions?

Open a [Discussion](https://github.com/ai-era/awesome-research-figures/discussions) for questions about contributing.
