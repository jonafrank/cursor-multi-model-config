# Switch Model Profile

I want to switch my model profile.

## Available Profiles

| Profile | File | Use Case |
|---------|------|----------|
| **default** | `.cursor/model-profiles/default.json` | Balanced speed and completeness |
| **fallback** | `.cursor/model-profiles/fallback.json` | Low-cost for quota exhaustion |
| **completeness** | `.cursor/model-profiles/completeness.json` | Premium for deep planning |
| **cost_minimized** | `.cursor/model-profiles/cost_minimized.json` | Minimal cost for batch processing |

## Instructions

1. Read `.cursor/model-profiles/current-profile.json` to see which profile is currently active
2. Tell me the current profile name
3. Ask which profile I'd like to switch to
4. When I choose, copy the contents of that profile to `current-profile.json`

## Switch Commands

```bash
# To switch manually:
cp .cursor/model-profiles/default.json .cursor/model-profiles/current-profile.json
cp .cursor/model-profiles/fallback.json .cursor/model-profiles/current-profile.json
cp .cursor/model-profiles/completeness.json .cursor/model-profiles/current-profile.json
cp .cursor/model-profiles/cost_minimized.json .cursor/model-profiles/current-profile.json
```

