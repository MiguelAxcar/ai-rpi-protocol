# ai-rpi-protocol

Stop AI coding assistants from going rogue. Drop this governance framework into any repo to enforce Research, Plan, Implement, challenge weak requirements, and ship safer code with repeatable checkpoints.

## What is RPI?

RPI (Research → Plan → Implement) is a structured methodology that prevents AI coding assistants from making hasty changes by enforcing three mandatory phases:

1. **Research**: Understand the problem and constraints
2. **Plan**: Create a detailed implementation strategy
3. **Implement**: Execute with built-in quality checkpoints

## Quick Start

1. Copy `rpi-config.yaml` to your repository root
2. Copy the `templates/` directory to your project
3. Configure your AI assistant to follow the RPI workflow

See [USAGE.md](USAGE.md) for detailed instructions.

## Features

- ✅ Enforces thoughtful analysis before coding
- ✅ Prevents scope creep with clear planning
- ✅ Built-in quality and security checkpoints
- ✅ Customizable enforcement levels
- ✅ Template-driven workflow
- ✅ Integrates with existing CI/CD

## Why RPI?

AI coding assistants are powerful but can:
- Rush to implementation without understanding
- Make broad changes based on vague requirements
- Skip important validation steps
- Introduce security vulnerabilities unknowingly

RPI addresses these risks with a governance framework that keeps AI on track.

## Example Workflow

```bash
# Start with research
cp templates/research.md .rpi/task-research.md
# Fill in research questions and findings

# Create a plan
cp templates/plan.md .rpi/task-plan.md
# Define tasks and success criteria

# Implement with checkpoints
cp templates/implement.md .rpi/task-implementation.md
# Follow the checklist to completion
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT License - see [LICENSE](LICENSE) for details.
