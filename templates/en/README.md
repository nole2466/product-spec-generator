# English Templates

This folder contains English versions of the templates.

## Available Templates

| Template | Description | Role |
|----------|-------------|------|
| [spec.md](./spec.md) | Feature specification | PD |
| [contract.md](./contract.md) | API contract | Backend |
| [acceptance.md](./acceptance.md) | Acceptance criteria | QA |
| [delta.md](./delta.md) | Delta Spec for Sprint changes | PD |

## Usage

Use these templates when working in English-speaking teams or international projects.

## Status Symbols

All templates use consistent status symbols:

**Core Status**:
| Symbol | Status | Description |
|:------:|--------|-------------|
| ⚪ | Pending | Not started |
| 🔵 | In Progress | Currently working |
| ✅ | Done | Completed |

**Extended Status**:
| Symbol | Status |
|:------:|--------|
| 🟡 | Under Review |
| 🔴 | Blocked |

## Adding More Templates

To add an English version of a template:

1. Create the file in this folder with the same name as the Chinese version
2. Translate all content while keeping the same structure
3. Keep emoji symbols consistent with the Chinese version

## Directory Structure

```
templates/
├── spec.md               # Chinese (default)
├── contract.md           # Chinese (default)
├── acceptance.md         # Chinese (default)
├── delta.md              # Chinese (default)
├── ...
└── en/
    ├── README.md         # This file
    ├── spec.md           # English version
    ├── contract.md       # English version
    ├── acceptance.md     # English version
    └── delta.md          # English version
```
