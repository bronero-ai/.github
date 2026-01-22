# GitHub Copilot Instructions for .github Repository

## Repository Overview

This is the `.github` repository for the bronero-ai organization. It contains organization-wide GitHub configurations and automation templates that are automatically applied to all repositories in the organization.

**Repository Type:** Meta/Configuration repository
**Primary Purpose:** Centralized GitHub configurations and workflow templates
**Size:** Small (4 files)
**Languages:** YAML, Markdown

## Repository Structure

```
.github/
├── copilot-instructions.md (this file)
├── PULL_REQUEST_TEMPLATE.md
└── workflows/
    └── pr-automation.yml
README.md
```

### Key Files

- **`.github/PULL_REQUEST_TEMPLATE.md`**: Default pull request template applied to all repositories in the organization. Contains sections for Summary, Tests, Risks, and Checklist.

- **`.github/workflows/pr-automation.yml`**: Automated PR validation workflow that:
  - Validates PR descriptions contain required sections (Summary, Tests, Risks)
  - Responds to `needs-comment` label by posting reminders about required sections
  - Responds to `/review-check` command in comments with a review checklist
  - Posts automated notifications when CI workflows fail

- **`README.md`**: Contains a personal philosophy and manifest (in Czech language)

## Working with This Repository

### No Build or Test Infrastructure

This repository contains only configuration files and does not require:
- Building or compilation steps
- Running tests
- Installing dependencies
- Linting (no linting configuration present)

### Validation Steps

When making changes:

1. **For workflow files** (`.github/workflows/*.yml`):
   - Validate YAML syntax with: `yamllint .github/workflows/*.yml` (if yamllint is available)
   - Review the workflow triggers and permissions carefully
   - Test changes by creating a PR and observing workflow execution

2. **For PR template** (`.github/PULL_REQUEST_TEMPLATE.md`):
   - Ensure all required sections are preserved: Summary, Tests, Risks, Checklist
   - Maintain consistency with the pr-automation.yml validation logic

3. **For Copilot instructions** (`.github/copilot-instructions.md`):
   - Keep instructions concise and actionable
   - Focus on repository-specific guidance

### Pull Request Requirements

All PRs should follow the template structure:
- **Summary**: Brief description of changes
- **Tests**: Description of validation performed
- **Risks**: Potential concerns or areas of impact
- **Checklist**: Complete the provided checklist items

The PR automation workflow will comment on PRs missing these sections.

## Copilot Guidance

When working on this repository:

1. **Preserve existing automation logic**: The pr-automation.yml workflow is carefully crafted to avoid duplicate comments and handle multiple event types. Be cautious when modifying it.

2. **Maintain template consistency**: Any changes to PULL_REQUEST_TEMPLATE.md should align with the validation logic in pr-automation.yml.

3. **Test workflow changes carefully**: Workflow changes affect all repositories in the organization. Consider the impact across multiple repositories.

4. **Respect the manifest**: The README.md contains personal values and philosophy. Only modify if explicitly requested.

5. **Organization-wide impact**: Remember that changes to this repository affect all repositories in the bronero-ai organization.

## Common Operations

### Adding a new workflow
```bash
# Create new workflow file
cd .github/workflows
# Edit new workflow file with appropriate triggers and steps
```

### Updating PR template
```bash
# Edit the template
vim .github/PULL_REQUEST_TEMPLATE.md
# Ensure consistency with pr-automation.yml validation
```

### Testing workflows locally
```bash
# Install act (GitHub Actions local runner) if needed
# Run workflows locally for testing
act pull_request -e event.json
```

## Tips for Contributors

- This repository has no code to build or test - focus on configuration correctness
- YAML syntax errors in workflows will cause CI failures across the organization
- Always validate YAML syntax before committing
- Test workflow changes in a fork or test repository first when possible
- The pr-automation workflow includes logic to prevent duplicate comments - preserve this behavior
