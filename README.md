# Cursor Multi-Model Configuration Template

A configuration template that makes Cursor automatically recommend the best AI model for your task—plan with GPT-5, debug with Claude, refactor with DeepSeek, or optimize costs on demand.
#### WHAT IT DOES:
* Task Detection: Identifies what you're doing (planning, debugging, refactoring, etc.)
* 4 Model Profiles: default (balanced), completeness (premium), cost_minimized (batch), fallback (quota-exhausted)
* 7 Slash Commands: /planning, /reasoning, /refactor, /summarize, /compliance, /creative, /draft
* 10 Task-Specific Rules: Guidelines and best practices for each mode
* Zero Configuration: Copy .cursor folder to any project, get instant model routing
  
#### WHY IT MATTERS:
Cursor supports 10+ AI models, each optimized for different work. Manual switching is friction. This removes that friction—you get the right tool automatically, or switch to a cost-optimized profile when quota runs low.

## Quick Start

### Copy to a New Project

```bash
# Copy the .cursor folder (contains rules, commands, and model profiles)
cp -r /path/to/cursor-config/.cursor /path/to/your-project/
```

Or clone this repo as a template:
```bash
git clone https://github.com/your-username/cursor-config.git my-project
```

## Structure

```
.cursor/
├── rules/
│   ├── 00-model-router.mdc      # Main router (always active)
│   ├── 01-planning.mdc          # Planning tasks
│   ├── 02-reasoning.mdc         # Debugging/analysis
│   ├── 03-refactor.mdc          # Code refactoring
│   ├── 04-summarize.mdc         # Explanations
│   ├── 05-compliance.mdc        # Code review
│   ├── 06-creative.mdc          # New features
│   └── 07-draft.mdc             # Quick prototypes
├── commands/
│   ├── planning.md              # /planning command
│   ├── reasoning.md             # /reasoning command
│   ├── refactor.md              # /refactor command
│   ├── summarize.md             # /summarize command
│   ├── compliance.md            # /compliance command
│   ├── creative.md              # /creative command
│   ├── draft.md                 # /draft command
│   └── switch-profile.md        # /switch-profile command
└── model-profiles/
    ├── default.json             # Balanced speed + quality
    ├── fallback.json            # Quota exhaustion mode
    ├── completeness.json        # Premium models
    ├── cost_minimized.json      # Batch processing
    └── current-profile.json     # Active profile
```

## Model Profiles

| Profile | Use Case | Philosophy |
|---------|----------|------------|
| **default** | Normal daily use | Balanced speed and completeness |
| **fallback** | Quota exhaustion | Low-cost, fast models only |
| **completeness** | Deep planning, multi-file | Premium reasoning models |
| **cost_minimized** | Batch processing | Minimal cost models |

### Profile Contents

Each profile defines models for different task types:

| Task | Description |
|------|-------------|
| `default` | General-purpose tasks |
| `autocomplete` | Code completion |
| `planning` | Architecture and design |
| `reasoning` | Debugging and analysis |
| `refactor` | Code cleanup |
| `summarize` | Explanations and overviews |
| `long_context` | Large file operations |
| `compliance` | Code review and security |
| `creative` | New feature implementation |
| `draft` | Quick prototypes |

## Usage

### Slash Commands

Use these commands in Cursor chat:

- `/planning` - Start a planning/architecture session
- `/reasoning` - Debug or analyze complex issues
- `/refactor` - Clean up and optimize code
- `/summarize` - Get code explanations
- `/compliance` - Code review and security check
- `/creative` - Build new features
- `/draft` - Quick prototype mode
- `/switch-profile` - Change model profile

### Switching Profiles

**Option 1: Use the slash command**
```
/switch-profile
```

**Option 2: Manual switch**
```bash
# Switch to completeness profile
cp .cursor/model-profiles/completeness.json .cursor/model-profiles/current-profile.json

# Switch to cost_minimized profile
cp .cursor/model-profiles/cost_minimized.json .cursor/model-profiles/current-profile.json

# Switch to fallback profile
cp .cursor/model-profiles/fallback.json .cursor/model-profiles/current-profile.json

# Switch back to default
cp .cursor/model-profiles/default.json .cursor/model-profiles/current-profile.json
```

### How It Works

1. The **00-model-router.mdc** rule is always active and detects task types from your queries
2. When a task type is detected, it reads `current-profile.json` and recommends the appropriate model
3. Task-specific rules provide additional guidance for each type of work
4. Slash commands explicitly activate a mode with model recommendations

## Customization

### Adding New Models

Edit any profile in `.cursor/model-profiles/` to change model assignments:

```json
{
  "name": "default",
  "description": "Balanced speed and completeness",
  "models": {
    "default": "your-preferred-model",
    "planning": "your-planning-model",
    ...
  }
}
```

### Creating a New Profile

1. Copy an existing profile:
   ```bash
   cp .cursor/model-profiles/default.json .cursor/model-profiles/my-custom.json
   ```

2. Edit the models to your preferences

3. Switch to it:
   ```bash
   cp .cursor/model-profiles/my-custom.json .cursor/model-profiles/current-profile.json
   ```

### Modifying Rules

Edit the `.mdc` files in `.cursor/rules/` to customize:
- Task detection keywords
- Response formats
- Guidelines and best practices

## Tips

- **Quota exhaustion?** Switch to `fallback` profile
- **Complex multi-file work?** Use `completeness` profile
- **Batch processing?** Use `cost_minimized` profile
- **Normal work?** Stick with `default` profile

## Model Reference

### Default Profile Models

| Task | Model |
|------|-------|
| default | gpt-5.1 |
| autocomplete | composer-1 |
| planning | gpt-5.1-codex-high |
| reasoning | claude-4.5-opus |
| refactor | deepseek-v3.1 |
| summarize | claude-4.5-haiku |
| long_context | kimi-k2-instruct |
| compliance | claude-4.5-opus |
| creative | grok-4-fast-reasoning |
| draft | composer-1 |

### Completeness Profile Models

| Task | Model |
|------|-------|
| default | gpt-5.1-codex-high |
| autocomplete | composer-1 |
| planning | gpt-5.1-codex-high |
| reasoning | claude-4.5-opus-high |
| refactor | deepseek-v3.1 |
| summarize | kimi-k2-instruct |
| long_context | kimi-k2-instruct |
| compliance | claude-4.5-opus-high |
| creative | grok-4-fast-reasoning |
| draft | gpt-5.1 |

### Cost Minimized Profile Models

| Task | Model |
|------|-------|
| default | composer-1 |
| autocomplete | composer-1 |
| planning | gpt-5.1-codex-low |
| reasoning | deepseek-r1-0528 |
| refactor | deepseek-r1-0528 |
| summarize | claude-4.5-haiku |
| long_context | claude-4.5-haiku |
| compliance | claude-4.5-haiku |
| creative | grok-4-fast-non-reasoning |
| draft | composer-1 |

### Fallback Profile Models

| Task | Model |
|------|-------|
| default | composer-1 |
| autocomplete | composer-1 |
| planning | composer-1 |
| reasoning | deepseek-r1-0528 |
| refactor | deepseek-r1-0528 |
| summarize | composer-1 |
| long_context | composer-1 |
| compliance | deepseek-r1-0528 |
| creative | composer-1 |
| draft | composer-1 |

