# Claude Code GitHub Actions Setup

This repository uses Claude Code GitHub Actions to provide AI-powered automation for pull requests, issues, and code reviews.

## Setup Instructions

### 1. Install Claude GitHub App

Visit [Claude Code GitHub App](https://github.com/apps/claude-code) and install it for this repository.

### 2. Configure API Key

Add your Anthropic API key to repository secrets:

1. Go to repository **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret**
3. Name: `ANTHROPIC_API_KEY`
4. Value: Your Anthropic API key from [console.anthropic.com](https://console.anthropic.com/)
5. Click **Add secret**

### 3. Workflow File

The workflow file is already configured at `.github/workflows/claude-code.yml`

## Usage

### On Issues and Pull Requests

Comment `/claude <your request>` on any issue or PR to trigger Claude Code:

```
/claude Review this PR and suggest improvements
/claude Fix the failing tests
/claude Implement the feature described in this issue
```

### Automatic PR Analysis

Claude Code automatically analyzes new PRs and synchronized changes.

## Features

- **AI Code Review**: Automated analysis of pull requests
- **Issue Resolution**: Generate code to fix reported issues
- **Feature Implementation**: Create implementations from issue descriptions
- **BAML Context**: Automatically reads project CLAUDE.md and BAML skill documentation

## Permissions

The workflow has been configured with minimal required permissions:
- `contents: write` - To create commits and branches
- `pull-requests: write` - To create and update PRs
- `issues: write` - To comment on issues

## Troubleshooting

### Claude Code doesn't respond
- Verify the GitHub App is installed for this repository
- Check that `ANTHROPIC_API_KEY` is configured in repository secrets
- Ensure comments start with `/claude`

### API Key Issues
- Confirm your API key is valid at [console.anthropic.com](https://console.anthropic.com/)
- Verify the secret name is exactly `ANTHROPIC_API_KEY`

## Advanced Configuration

You can customize Claude Code behavior by modifying `.github/workflows/claude-code.yml`:

```yaml
claude_args: |
  --read custom-instructions.md
  --model claude-sonnet-4
```

## Documentation

- [Claude Code GitHub Actions Docs](https://docs.claude.com/en/docs/claude-code/github-actions)
- [Claude Code Documentation](https://docs.claude.com/en/docs/claude-code)

---

**Note**: This GitHub Action uses the Anthropic API and will consume API credits. Monitor usage at [console.anthropic.com](https://console.anthropic.com/).
