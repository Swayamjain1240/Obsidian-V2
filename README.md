# Obsidian

**A review-first, human-gated enhancer for GitHub repositories.**

Obsidian reads your public GitHub repository, reports bugs, security issues and enhancement opportunities, proposes an enhancement plan, applies only what you approve on a separate branch, and opens a pull request only after your explicit permission.

> Obsidian is an **enhancer**, not an automatic bug fixer. Bugs and errors are reported to you, never silently fixed.

## Core principles

- **Human approval first.** Nothing is changed without your approval, and nothing is merged without you.
- **Your code is never executed.** Obsidian only reads your repository. It does not run install, build, test, lint, scripts or git hooks.
- **Your `main` branch is never touched.** All work is committed to a separate branch `obsidian/enhance-<repo>`. No force-push. No auto-merge.
- **AI only suggests.** Login, approval, workflow state and security checks are normal code. AI output is validated before it is used.
- **Honest results.** Obsidian does not claim a project is tested, secure or production-ready.

## How it works

1. Log in with GitHub OAuth.
2. Pick one of your own personal public repositories (ownership and visibility are verified on the server).
3. Obsidian pins the exact commit and creates a work branch.
4. It analyzes the project from file content (languages, frameworks, package managers), not from folder names.
5. It reports findings with file and line evidence.
6. You choose what to enhance. Each operation lists files, risk and expected change.
7. You approve the plan. High-risk operations need extra confirmation.
8. Approved edits are committed to the work branch.
9. Static checks run (syntax parse, diff matches manifest). Code is not run.
10. You review the exact diff, the change manifest and the check results.
11. With your permission, Obsidian opens a pull request into `main`. You decide whether to merge.

## Safety model

| Area | Control |
|---|---|
| Ownership | Server verifies owner, public visibility and personal account |
| Approval | Bound to user, repo, commit SHA and selected operations. Stale approvals are rejected |
| Execution | Only approved operations, only on files inside the snapshot |
| Repository safety | Git hooks disabled, symlinks not followed, size and file-count limits |
| AI | Treated as untrusted input and output. No secrets, no authority over state |
| Delivery | Never targets `main`, never force-pushes, never merges |
| Data | Per-user isolation, rate limits, per-user AI limits, verified data deletion |

## Tech stack

| Layer | Technology |
|---|---|
| Frontend | React, Vite (JavaScript) |
| Backend | Node.js, Express (JavaScript) |
| Database | MongoDB |
| Job queue | BullMQ, Redis |
| AI service | Python (FastAPI) |
| Auth | GitHub OAuth |

## Repository layout

```
Obsidian-V2/
├── frontend/      React + Vite client
├── backend/       Express API, worker, workflow engine
├── aiServices/    Python AI service
├── docs/          Design documents
└── README.md
```

## Documentation

All design decisions are documented in [`docs/`](./docs):

| Document | Purpose |
|---|---|
| [PRODUCT_SPEC](./docs/PRODUCT_SPEC.md) | Product scope, flow and acceptance criteria |
| [SYSTEM_ARCHITECTURE](./docs/SYSTEM_ARCHITECTURE.md) | Components, trust boundaries, failure modes |
| [DATA_MODEL](./docs/DATA_MODEL.md) | Collections, indexes, consistency rules |
| [WORKFLOW_STATE_MACHINE](./docs/WORKFLOW_STATE_MACHINE.md) | States, transitions, guards, recovery |
| [THREAT_MODEL](./docs/THREAT_MODEL.md) | Threats, controls and tests |
| [API_CONTRACTS](./docs/API_CONTRACTS.md) | Endpoints and error codes |
| [TEST_STRATEGY](./docs/TEST_STRATEGY.md) | Test layers and security test list |
| [DEFINITION_OF_DONE](./docs/DEFINITION_OF_DONE.md) | Release criteria |

## Status

The design documents in `docs/` are the source of truth for the implementation.

## License

To be decided by the repository owner.
