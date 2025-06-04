# Git Workflow Guide

This document outlines our Git workflow for the top-down action game project, including branching strategies, commit conventions, and pull request processes.

## 🌳 Branching Strategy

```
main
│── feature/UE-123-player-movement
│── feature/UE-456-weapon-system
│── bugfix/UE-789-animation-crash
└── deliverable
```

### Branch Types

| Branch Type | Purpose | Naming Convention | Merge Target |
|-------------|---------|-------------------|--------------|
| `main` | Production-ready code | `main` | - |
| `feature/*` | New features | `feature/UE-123-description` | `develop` |
| `bugfix/*` | Bug fixes | `bugfix/UE-456-description` | `develop` |

### Branch Naming Rules

**Format:** `<type>/<ticket-id>-<short-description>`

**Examples:**
```bash
feature/UE-123-player-double-jump
bugfix/UE-456-inventory-ui-overlap
hotfix/UE-789-memory-leak-fix
content/UE-101-medieval-castle-assets
refactor/UE-202-weapon-system-cleanup
```

**Rules:**
- Use lowercase with hyphens
- Include ticket/issue ID (UE-XXX format)
- Keep description concise but descriptive
- No spaces or special characters

## 📝 Commit Message Standards

### Commit Types

| Type | Description | Example |
|------|-------------|---------|
| `feat` | New features | `feat(player): add double jump mechanic` |
| `fix` | Bug fixes | `fix(ui): resolve inventory slot overlap` |
| `docs` | Documentation | `docs(readme): update setup instructions` |
| `style` | Code formatting | `style(blueprints): organize node layout` |
| `refactor` | Code restructuring | `refactor(weapons): simplify projectile system` |

### Commit Examples

**Good commits:**
```bash
feat(combat): implement status effect system

- Added burn and slow effects
- Created StatusEffectComponent
- Integrated with weapon damage calculation

Closes UE-123

fix(ui): resolve health bar scaling on 4K displays

The health bar was incorrectly scaled on high-DPI displays
due to improper anchor settings in WBP_HealthBar.

Fixes UE-456

content(environment): add medieval castle tileset

- 24 unique wall pieces with 3 LOD levels
- 12 decorative props optimized for mobile
- Includes collision meshes and lightmap UVs

Assets created by: ArtistName
Reviewed by: LeadArtist
```

**Bad commits:**
```bash
# Too vague
fix: stuff

# Missing scope
add new feature

# No description
feat(player): 

# Not following convention
FIXED THE BUG!!!
```