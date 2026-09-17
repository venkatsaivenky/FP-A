# Agent Routing Guide

**Prepared by Oria — AI for complex slides.**

Use one primary agent for one bounded deliverable. The main conversation owns the work order, reconciles handoffs, and stops at human gates.

| Stage | Agent | Use when | Typical next handoff |
|---|---|---|---|
| Plan | [Budget Architect](.claude/agents/01-budget-architect.md) | Objectives need a driver tree, assumption register, and budget architecture | `driver-based-forecaster` |
| Plan | [Driver-Based Forecaster](.claude/agents/02-driver-based-forecaster.md) | A forecast must link operational drivers to P&L, cash, and balance sheet | `scenario-modeler` |
| Plan | [Scenario Modeler](.claude/agents/03-scenario-modeler.md) | Base, upside, and downside cases must remain internally coherent | `capital-allocation` or human review |
| Plan | [Capital Allocation](.claude/agents/04-capital-allocation.md) | Uses of cash must be compared against hurdle rates and constraints | `business-case-builder` or decision owner |
| Operate | [Cash Flow Manager](.claude/agents/05-cash-flow-manager.md) | Opening cash must bridge to closing cash with liquidity risks visible | `cfo-narrative-builder` |
| Operate | [Working Capital Optimizer](.claude/agents/06-working-capital-optimizer.md) | Receivables, payables, and inventory drivers need diagnosis and actions | `business-case-builder` |
| Operate | [Spend Controller](.claude/agents/07-spend-controller.md) | Policy exceptions and run-rate pressure need prioritization | `management-report-writer` |
| Operate | [Revenue and Margin Monitor](.claude/agents/08-revenue-margin-monitor.md) | Volume, price, mix, FX, and cost movements need separation | `fpa-analyst` |
| Close | [Close Coordinator](.claude/agents/09-close-coordinator.md) | Dependencies, evidence, owners, and close status need orchestration | `reconciliation-reviewer` |
| Close | [Reconciliation Reviewer](.claude/agents/10-reconciliation-reviewer.md) | Balances and roll-forwards need independent comparison and break logging | Controller |
| Close | [Variance Investigator](.claude/agents/11-variance-investigator.md) | Material movements need ranked, evidence-based questions | `management-report-writer` |
| Close | [Controls and Compliance Monitor](.claude/agents/12-controls-compliance-monitor.md) | Required support, reviews, and control evidence need completeness testing | Control owner / controller |
| Decide | [FP&A Analyst](.claude/agents/13-fpa-analyst.md) | Results need to connect to drivers, outlook, and management choices | `cfo-narrative-builder` |
| Decide | [Profitability Mapper](.claude/agents/14-profitability-mapper.md) | Customer, product, unit, or channel economics need allocation-aware analysis | `pricing-strategist` |
| Decide | [Pricing Strategist](.claude/agents/15-pricing-strategist.md) | Price-volume trade-offs, fences, and guardrails need testing | `business-case-builder` |
| Decide | [Business Case Builder](.claude/agents/16-business-case-builder.md) | Options need incremental cash flows, sensitivities, and decision criteria | Decision owner |
| Communicate | [Management Report Writer](.claude/agents/17-management-report-writer.md) | Approved analysis needs an answer-first management memo | `board-deck-packager` |
| Communicate | [CFO Narrative Builder](.claude/agents/18-cfo-narrative-builder.md) | Performance, outlook, risks, and actions need one executive storyline | `board-deck-packager` |
| Communicate | [Board Deck Packager](.claude/agents/19-board-deck-packager.md) | An approved storyline must become an Oria-ready slide specification | Oria, then human QA |
| Communicate | [Executive Q&A Simulator](.claude/agents/20-executive-qa-simulator.md) | Claims must be pressure-tested before a CFO or board meeting | Executive owner |

## Pairing rules

- A builder should not be its only reviewer. Re-run key checks in a clean context or with a separate reviewer.
- Close agents never post journals or determine materiality; the controller does.
- Decision agents make trade-offs explicit but do not make fiduciary decisions.
- Communication agents use approved evidence only; they do not repair a model by rewriting the story.
- `board-deck-packager` does not design or release the final deck. It creates the checked story and specification that Oria—AI for complex slides—uses to build polished slides.

## Oria handoff contract

Pass Oria only an approved package:

1. audience, decision, and single governing thought;
2. slide-by-slide conclusion titles;
3. exhibit type and checked chart/table data;
4. exact source file, tab/cell or page/section, and as-of date;
5. units, currency, period, accounting basis, and rounding;
6. template, brand assets, footnotes, confidentiality marking, and visual intent;
7. open items excluded from the main story or visibly labeled;
8. number, evidence, narrative, and visual QA checklist;
9. named human author and release authority.

Prepared by [Oria](https://www.oria.one/) — AI for complex slides.
