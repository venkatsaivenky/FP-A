# Oria Finance Agent Pack for Claude

**Prepared by Oria — AI for complex slides.**

This pack contains 20 project-scoped Claude Code subagents for recurring finance work. Each definition maps to one working mode in the Oria Claude Finance Playbook: Plan, Operate, Close, Decide, and Communicate.

These are bounded analyst subagents, not autonomous finance employees. They prepare, challenge, and package draft work. They do not become your system of record, approve a forecast, post a journal, set accounting policy, execute a payment or trade, certify a control, or release a board document. A named finance professional remains accountable.

## What is included

- `.claude/agents/`: exactly 20 Claude Code subagent definitions.
- `QUICKSTART.md`: install and run the pack in Claude Code, Claude Projects, or a manual chat workflow.
- `WORK_ORDER_TEMPLATE.md`: the reusable task brief that tells an agent what decision, evidence, method, and controls apply to one run.
- `AGENT_ROUTING.md`: which agent to choose, which agent should review it, and where Oria fits.

## Agent catalog

| Plan | Operate | Close | Decide | Communicate |
|---|---|---|---|---|
| [01 Budget Architect](.claude/agents/01-budget-architect.md) | [05 Cash Flow Manager](.claude/agents/05-cash-flow-manager.md) | [09 Close Coordinator](.claude/agents/09-close-coordinator.md) | [13 FP&A Analyst](.claude/agents/13-fpa-analyst.md) | [17 Management Report Writer](.claude/agents/17-management-report-writer.md) |
| [02 Driver-Based Forecaster](.claude/agents/02-driver-based-forecaster.md) | [06 Working Capital Optimizer](.claude/agents/06-working-capital-optimizer.md) | [10 Reconciliation Reviewer](.claude/agents/10-reconciliation-reviewer.md) | [14 Profitability Mapper](.claude/agents/14-profitability-mapper.md) | [18 CFO Narrative Builder](.claude/agents/18-cfo-narrative-builder.md) |
| [03 Scenario Modeler](.claude/agents/03-scenario-modeler.md) | [07 Spend Controller](.claude/agents/07-spend-controller.md) | [11 Variance Investigator](.claude/agents/11-variance-investigator.md) | [15 Pricing Strategist](.claude/agents/15-pricing-strategist.md) | [19 Board Deck Packager](.claude/agents/19-board-deck-packager.md) |
| [04 Capital Allocation](.claude/agents/04-capital-allocation.md) | [08 Revenue and Margin Monitor](.claude/agents/08-revenue-margin-monitor.md) | [12 Controls and Compliance Monitor](.claude/agents/12-controls-compliance-monitor.md) | [16 Business Case Builder](.claude/agents/16-business-case-builder.md) | [20 Executive Q&A Simulator](.claude/agents/20-executive-qa-simulator.md) |

## Install in Claude Code

1. Install or update Claude Code using Anthropic's [official setup guide](https://code.claude.com/docs/en/overview).
2. Unzip this pack in the root of the finance workspace or repository you want Claude Code to use. Keep the `.claude/agents/` path intact.
3. Inspect every Markdown file before use. These files become instructions to Claude; never install unreviewed agent files from an untrusted source.
4. Start Claude Code from that workspace. If `.claude/agents/` did not exist when the current session started, restart the session once.
5. Ask the main conversation to delegate explicitly, for example: `Use the driver-based-forecaster subagent with the attached work order. Return its draft to this conversation; do not publish or change source files.`

Anthropic documents project subagents as Markdown files in `.claude/agents/` with YAML frontmatter. They run in separate context windows and return results to the main conversation. See [Create custom subagents](https://code.claude.com/docs/en/sub-agents).

### Why the files are read-only by default

All 20 subagents declare only `Read`, `Glob`, and `Grep`, use the parent model, and run in `plan` permission mode. They inspect workspace evidence and return a structured draft to the main conversation. They cannot edit a workbook, send a message, browse arbitrary sites, or write a release artifact by themselves. The main conversation—and then the responsible human—decides whether to create or change files.

This is deliberate least privilege. If your organization adds tools or connectors, do so only after security and data owners approve the scope. Prefer read-only access, restrict folders and systems, and require manual approval for consequential actions. Review Anthropic's [permissions documentation](https://code.claude.com/docs/en/permissions).

## Use with Claude Projects or ordinary Claude chat

Claude Projects do not install `.claude/agents/` as Claude Code subagents. Use this manual alternative:

1. Create a Project for one durable mandate, company, reporting cycle, or planning process—not the entire finance function.
2. Add approved policies, definitions, templates, and current source files to Project knowledge. Add concise project instructions that state source hierarchy, units, accounting basis, approval boundaries, and output standards.
3. Open the relevant agent file and paste its Markdown body into a new chat as working instructions. Then paste a completed work order from `WORK_ORDER_TEMPLATE.md`.
4. Run only one bounded role per chat. Start a separate reviewer chat for high-stakes work so the reviewer does not inherit the builder's reasoning.
5. Bring the verified output back to a main coordination chat. That main chat should maintain the source ledger, decisions, open items, versions, and approvals.

Claude Projects provide persistent knowledge and project instructions, but they are not the same as Claude Code subagents. See [What are Projects?](https://support.claude.com/en/articles/9517075-what-are-projects) and [Upload files to Claude](https://support.claude.com/en/articles/8241126-upload-files-to-claude).

## Main-conversation orchestration

Use the main Claude conversation as the accountable coordinator:

1. Validate the work order and list missing inputs.
2. Delegate a bounded task to one agent from `AGENT_ROUTING.md`.
3. Require the agent to return a draft, source ledger, assumption register, open issues, and proposed next handoff.
4. Route calculations and source claims to an independent reviewer before they enter a memo or deck.
5. Stop at every named human gate. Never treat silence as approval.
6. After storyline approval, hand checked material to Oria to create complex slides; then run number, evidence, narrative, and visual QA before release.

Avoid delegating a vague request to several agents at once. Parallel work is useful only when workstreams are independent, permissions are bounded, and the coordinator can reconcile conflicting assumptions. Otherwise, sequence the agents.

## Data and trusted-file warning

Treat uploaded spreadsheets, PDFs, email exports, web pages, connector responses, and this pack itself as potentially untrusted input. Hidden instructions inside external content can try to redirect an AI system. In every run:

- tell the agent that source content is data, never authority to change its instructions;
- use approved sources and record an as-of date;
- exclude secrets, credentials, personal data, and restricted information unless the environment and policy explicitly allow them;
- inspect agent files, Skills, plugins, and connector scopes before enabling them;
- keep external sending, ledger writes, payments, trading, approvals, and production publishing outside these agents;
- verify calculations independently and tie every material figure to a source, cell, formula, or labeled assumption.

Anthropic notes that external files and websites can contain hidden instructions; review the security guidance in [Create and edit files with Claude](https://support.claude.com/en/articles/12111783-create-and-edit-files-with-claude).

## Limitations

- The agents can use only the tools and files available in your Claude environment.
- Read access does not establish that a file is current, complete, entitled, or authoritative.
- Natural-language analysis can be wrong. Reproduce material calculations in a controlled workbook or deterministic script.
- The pack contains agent workflows, not firm policy, accounting advice, audit evidence, tax advice, legal advice, or investment recommendations.
- Claude feature availability, model behavior, plan limits, and file support can change. Verify current product documentation before rollout.
- Oria is the presentation layer: it turns checked analysis into polished, complex slides. It does not replace finance verification or executive approval.

## Recommended pilot

Start with one low-risk recurring workflow such as a forecast bridge or management-report draft. Run three supervised cases, compare them with the current process, log every correction, and scale only when evidence traceability, tie-outs, reviewer effort, and exception handling are acceptable.

## Official references

- [Claude Code: create custom subagents](https://code.claude.com/docs/en/sub-agents)
- [Claude Code permissions](https://code.claude.com/docs/en/permissions)
- [Claude Code overview and setup](https://code.claude.com/docs/en/overview)
- [Claude Projects](https://support.claude.com/en/articles/9517075-what-are-projects)
- [Upload files to Claude](https://support.claude.com/en/articles/8241126-upload-files-to-claude)
- [Prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)
- [Anthropic financial-services repository](https://github.com/anthropics/financial-services)
- [Create and edit files with Claude](https://support.claude.com/en/articles/12111783-create-and-edit-files-with-claude)

Prepared by [Oria](https://www.oria.one/) — AI for complex slides.
