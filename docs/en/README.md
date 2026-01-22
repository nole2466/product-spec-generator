# Product Spec Generator

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](../../CONTRIBUTING.md)

> From Requirements to Code, Together with AI

An enterprise-grade specification standard for product teams collaborating with AI.

[繁體中文](../../README.md) | **English**

---

## Features

- **Role-Oriented**: Clear responsibilities for PM, PD, Backend, Web, App, QA, Scrum Master
- **Human-AI Hybrid**: Readable and producible by both humans and AI
- **Centralized Knowledge**: Unified management of business logic, domain knowledge, and integrations
- **Review Workflow**: Built-in multi-role review mechanism

---

## Quick Start

### Option 1: Claude Code Plugin (Recommended)

Install the plugin in Claude Code to access all role skills:

```bash
# 1. Add Marketplace
/plugin marketplace add nole2466/product-spec-generator

# 2. Install Plugin
/plugin install product-spec-generator@product-spec-marketplace

# 3. Use Skills
/pm generate shopping cart feature    # PM generates PRD
/pd generate [PRD content]            # PD generates Spec
/backend generate [Spec content]      # Backend generates API Contract
/qa generate [Spec content]           # QA generates Acceptance Criteria
/scrum-master status                  # Track project progress
/review [Spec content]                # Multi-role review
```

**Available Skills:**

| Skill | Description | Usage |
|-------|-------------|-------|
| `/pm` | Product Manager | Generate PRD or review requirements |
| `/pd` | Product Designer | Generate Spec + Design specifications |
| `/backend` | Backend Developer | Generate API Contract |
| `/data-schema` | Data Schema Architect | Design entity definitions and data structures |
| `/chatbot` | Chatbot Specialist | Design AI/LLM chatbot specifications |
| `/web` | Web Developer | Review Web implementation feasibility |
| `/app` | App Developer | Review App implementation feasibility |
| `/qa` | QA Engineer | Generate Acceptance Criteria |
| `/scrum-master` | Scrum Master | Coordinate development phases, track progress |
| `/review` | Multi-role Review | Comprehensive specification review |

### Option 2: Clone to Project

```bash
# Using degit
npx degit nole2466/product-spec-generator my-project/specs

# Or direct clone
git clone https://github.com/nole2466/product-spec-generator.git
```

### Create Your First Feature Spec

```
my-project/
├── specs/
│   ├── _map.md                 # Feature map
│   └── user-login/             # Your first feature
│       ├── prd.md              # PM writes requirements
│       ├── spec.md             # PD writes specifications
│       ├── contract.md         # Backend defines API
│       └── acceptance.md       # QA writes acceptance criteria
└── knowledge/
    ├── business/               # Business logic
    ├── domain/                 # Domain knowledge
    └── integrations/           # Third-party integrations
```

### Choose Your Role

| Role | Start Here |
|------|------------|
| PM | Copy `templates/prd.md` to write requirements |
| PD | Read PRD, use `templates/spec.md` for specifications |
| Backend | Read Spec, use `templates/contract.md` for API |
| QA | Read all, use `templates/acceptance.md` for acceptance |
| Scrum Master | Read `agents/scrum-master.md` to coordinate phases |
| AI Agent | Read `SKILL.md` to understand how to assist |

---

## Project Structure

```
product-spec-generator/
│
├── .claude-plugin/           # Claude Code Plugin settings
│   ├── plugin.json           # Plugin info
│   └── marketplace.json      # Marketplace settings
│
├── skills/                   # Claude Code Skills
│   ├── pm/SKILL.md           # PM skill
│   ├── pd/SKILL.md           # PD skill
│   ├── backend/SKILL.md      # Backend skill
│   ├── data-schema/SKILL.md  # Data Schema Architect skill
│   ├── chatbot/SKILL.md      # Chatbot Specialist skill
│   ├── web/SKILL.md          # Web skill
│   ├── app/SKILL.md          # App skill
│   ├── qa/SKILL.md           # QA skill
│   ├── scrum-master/SKILL.md # Scrum Master skill
│   └── review/SKILL.md       # Multi-role review skill
│
├── core/                     # Core definitions
│   ├── principles.md         # Core principles (must read)
│   ├── glossary.md           # Glossary
│   └── review-workflow.md    # Review workflow
│
├── agents/                   # Role definitions (detailed)
│   ├── pm.md
│   ├── pd.md
│   ├── backend.md
│   ├── web.md
│   ├── app.md
│   ├── qa.md
│   └── scrum-master.md
│
├── templates/                # Document templates
│   ├── _map.md               # Feature map
│   ├── prd.md                # PRD template
│   ├── spec.md               # Spec template
│   ├── contract.md           # API Contract template
│   └── acceptance.md         # Acceptance Criteria template
│
├── examples/                 # Complete examples
│   └── product-search/       # Product search feature
│
└── references/               # Reference guides
    ├── business-logic.md
    ├── domain-knowledge.md
    └── integrations.md
```

---

## Roles and Outputs

```
                    ┌─────────────────┐
                    │  Scrum Master   │ ◄── Coordinates phase progression
                    │  (Coordinator)  │
                    └────────┬────────┘
                             │ Coordinates
         ┌───────────────────┼───────────────────┐
         ▼                   ▼                   ▼
PM ─────► prd.md        PD ─────► spec.md    QA ─────► acceptance.md
(Requirements)          (Spec + Design)       (Acceptance Criteria)
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
         Backend         Web/App        Testing
         contract.md     Code impl
         (API Contract)
```

---

## Working with AI

### Generation Mode

Let AI play a role to generate specifications:

```
Please act as a PD and generate spec.md based on the following PRD:

{PRD content}

Please first read agents/pd.md and templates/spec.md
```

### Review Mode

Let AI play a downstream role to review specifications:

```
Please review the following spec.md as a Backend developer:

{Spec content}

Check if the API is feasible and provide review results.
```

See [SKILL.md](../../SKILL.md) for details.

---

## Documentation

- [Best Practice Quick Start](../../BEST_PRACTICE.md) - **Start here**
- [Core Principles](../../core/principles.md) - Must read for everyone
- [Complete Example](../../examples/product-search/) - See a filled-out example
- [AI Collaboration Guide](../../SKILL.md) - How to work with AI

---

## Contributing

Contributions welcome! Please read [CONTRIBUTING.md](../../CONTRIBUTING.md) to learn how to participate.

### Ways to Contribute

- [Report Bugs](https://github.com/nole2466/product-spec-generator/issues)
- [Suggest Features](https://github.com/nole2466/product-spec-generator/issues)
- [Improve Documentation](../../CONTRIBUTING.md)
- [Translations](../../docs/)

---

## License

This project is licensed under the [MIT License](../../LICENSE).

---

## Acknowledgments

Thanks to all contributors and users for your support.

---

## Contact

- GitHub Issues: [Questions or Suggestions](https://github.com/nole2466/product-spec-generator/issues)
- Discussions: [Discussion Forum](https://github.com/nole2466/product-spec-generator/discussions)
