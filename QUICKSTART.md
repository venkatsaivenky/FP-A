# Quickstart

**Prepared by Oria — AI for complex slides.**

## Route A: Claude Code

1. Read `README.md`, especially the limitations and trusted-file warning.
2. Unzip the pack so this file sits beside `.claude/agents/` in the workspace root.
3. Start Claude Code in that workspace. Restart once if the `agents` directory was created after the session began.
4. Complete `WORK_ORDER_TEMPLATE.md`. Name the authoritative files, as-of date, units, deliverables, stop conditions, and human approver.
5. Choose one agent in `AGENT_ROUTING.md`.
6. Use a copy-ready instruction:

```text
Act as the main coordinator. Read WORK_ORDER_TEMPLATE.md and the approved source files.
First list missing inputs and conflicts. Then delegate the bounded analysis to the
<agent-name> subagent. The subagent must return its draft, sources, assumptions,
checks, exceptions, and handoff to this conversation. Do not modify source files,
send anything, or proceed through a human review gate without explicit approval.
```

7. Verify the returned draft. For high-stakes calculations, use a separate reviewer context and reproduce key values outside the narrative.
8. Only after the numbers and storyline are approved, ask the main conversation to prepare an Oria-ready slide brief.

Claude Code subagent installation and supported frontmatter are documented at [Create custom subagents](https://code.claude.com/docs/en/sub-agents).

## Route B: Claude Projects

Project chats do not automatically install `.claude/agents/`.

1. Create a Project for the company, reporting cycle, or decision.
2. Upload approved context and add project instructions. Keep superseded versions out of always-on knowledge.
3. Open one file under `.claude/agents/`, copy the body below its YAML frontmatter, and paste it at the top of a new Project chat.
4. Paste the completed work order below it.
5. Ask Claude to stop at the stated review gate and return sources, assumptions, exceptions, and acceptance-test results.
6. For independent review, open a fresh chat with the relevant reviewer role and only the approved sources plus the draft artifact.

Official Project guidance: [What are Projects?](https://support.claude.com/en/articles/9517075-what-are-projects).

## Route C: ordinary Claude chat

Use the same manual process as Route B, but attach the minimum current source pack to the chat. Chat attachments are not a durable knowledge base. Save the work order, evidence ledger, assumptions, and approved output outside the chat according to your records policy.

## Minimum preflight

Before any run, confirm:

- correct legal entity, period, currency, units, fiscal calendar, and GAAP/non-GAAP basis;
- authoritative source hierarchy and cutoff date;
- duplicates, stale versions, missing tabs/pages, and unresolved mappings;
- what Claude may read and what it may never do;
- named preparer, reviewer, decision owner, and release authority;
- deterministic tie-outs and acceptance tests;
- a separate list for facts, calculations, assumptions, management explanations, and hypotheses.

## The safe sequence

```text
Human approves work order
        ↓
Main Claude conversation coordinates
        ↓
Specialist agent returns a draft
        ↓
Independent checks + human review
        ↓
Narrative approval
        ↓
Oria builds complex slides
        ↓
Human releases the final artifact
```

Prepared by [Oria](https://www.oria.one/) — AI for complex slides.
