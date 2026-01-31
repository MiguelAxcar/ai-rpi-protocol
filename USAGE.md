# AI RPI Protocol - Usage Guide

## Overview

The AI RPI Protocol is a governance framework that helps AI coding assistants work more effectively by enforcing a structured Research → Plan → Implement workflow.

## Quick Start

1. Copy the `rpi-config.yaml` file to your repository
2. Copy the `templates/` directory to your project
3. Configure your AI assistant to follow the RPI phases

## Workflow

### Phase 1: Research
Start by understanding the problem:
```bash
cp templates/research.md .rpi/current-research.md
```
Answer all questions before proceeding.

### Phase 2: Plan
Create a detailed plan:
```bash
cp templates/plan.md .rpi/current-plan.md
```
Get approval before implementing.

### Phase 3: Implement
Execute the plan:
```bash
cp templates/implement.md .rpi/current-implementation.md
```
Follow the checklist to completion.

## Benefits

- **Prevents rushed implementations**: Forces thoughtful analysis
- **Reduces rework**: Better planning means fewer mistakes
- **Improves code quality**: Built-in checkpoints ensure standards
- **Better documentation**: Each phase produces useful artifacts
- **Safer AI**: Governance prevents AI from "going rogue"

## Configuration

Edit `rpi-config.yaml` to customize:
- Enforcement level (strict/advisory/disabled)
- Required checkpoints
- Custom rules and thresholds

## Integration

The framework can be integrated with:
- GitHub Actions (automated enforcement)
- Pre-commit hooks (local validation)
- CI/CD pipelines (deployment gates)
- AI assistant prompts (built-in guidance)
