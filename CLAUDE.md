# FP&A Workspace — Instruction Hierarchy

This workspace is configured for FP&A work with a specialist agent layer
(`.claude/agents/`) and a governance/control overlay (`02_ADVANCED_FPA_OVERLAY/`).

Read and apply, in this order, before doing any FP&A work in this repo:

1. Claude's own applicable system/platform instructions.
2. `02_ADVANCED_FPA_OVERLAY/10_CLAUDE_PROJECT_INSTRUCTIONS.md`
3. `02_ADVANCED_FPA_OVERLAY/01_SENIOR_FPA_CONTROLLER.md`
4. `02_ADVANCED_FPA_OVERLAY/04_FINANCIAL_MODEL_CONSTITUTION.md`
5. `02_ADVANCED_FPA_OVERLAY/03_FORECASTING_METHODOLOGY.md`
6. `02_ADVANCED_FPA_OVERLAY/08_COMPANY_FPA_MASTER_CONFIG_TEMPLATE.md`
   — **only once completed with approved, company-specific definitions.**
   Treat it as unset/blocking until a human has filled it in.
7. Specialist agents in `.claude/agents/` — routed per `AGENT_ROUTING.md`.
8. `02_ADVANCED_FPA_OVERLAY/06_MODEL_QA_CHECKLIST.md` and
   `02_ADVANCED_FPA_OVERLAY/09_BANK_SUBMISSION_QA.md` before any final release.

## Operating rules

- Before starting any bounded deliverable, require a completed work order
  (`WORK_ORDER_TEMPLATE.md` / `02_ADVANCED_FPA_OVERLAY/07_FPA_WORK_ORDER.md`):
  authoritative source files, as-of date, units/currency/basis, deliverable,
  stop conditions, and named human approver.
- Delegate one bounded deliverable to one primary agent at a time, per
  `AGENT_ROUTING.md`. The main conversation coordinates and reconciles
  handoffs; it does not skip the human review gates listed there.
- A builder is never its own sole reviewer — re-run key checks in a clean
  context or hand off to the paired reviewer role.
- Close agents (`09`–`12`) never post journal entries or determine
  materiality — that stays with the controller.
- Decision agents (`13`–`16`) make trade-offs explicit; they do not make
  fiduciary decisions.
- Communication agents (`17`–`20`) use only approved evidence; they do not
  fix a shaky model by rewriting the narrative around it.
- Material forecasts, bank submissions, covenant conclusions, and board
  reporting remain subject to human finance review before release —
  this package improves consistency and auditability, it does not
  guarantee correctness.

See `QUICKSTART.md` for the full setup and safe-sequence walkthrough, and
`AGENT_ROUTING.md` for the agent table and Oria handoff contract.
