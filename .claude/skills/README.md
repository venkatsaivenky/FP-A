# Oria FP&A Skills — chat / Cowork / Projects layer

This folder packages the same 20 specialist FP&A roles from `.claude/agents/`
as **Skills** so they also work outside Claude Code — in claude.ai chat,
Claude Projects, and Cowork. `.claude/agents/` subagents only load inside a
Claude Code session that has this repo open; Skills load anywhere Claude
does, because the trigger is a description match on your request, not a
repo-scoped filesystem convention.

## The two layers, and why both exist

| | `.claude/agents/*.md` (subagents) | `.claude/skills/*/SKILL.md` (this folder) |
|---|---|---|
| Works in | Claude Code, this repo only | claude.ai chat, Claude Projects, Cowork, **and** Claude Code |
| Runs in | Its own isolated context window — only the work order goes in, only a condensed result comes back | The current conversation — its instructions load straight into the context you're already using |
| Token cost | Lower — isolation keeps the main conversation's history out of the specialist's context | Higher than a subagent, but far lower than not having the skill at all (you'd otherwise paste the whole role definition every time) |
| Trigger | You name it, or the orchestrating model infers it from the agent's `description` | The model matches your request against the skill's `description` |

**They are not competing systems — they're the same 20 roles, wired for
different surfaces.** Use whichever one is available where you're working.

## The single most important efficiency tip

Neither system is a literal keyword lookup table. Both work by an LLM
matching your phrasing against a `description` field — that's probabilistic,
not deterministic. **The fastest, cheapest, most accurate way to invoke any
of these 20 roles, whenever you're in Claude Code with this repo open, is to
name the subagent explicitly instead of hoping the right one triggers:**

> "Use the `driver-based-forecaster` subagent with this work order: …"

This skips the routing guesswork entirely. It's the most accurate path and
uses the fewest tokens, because you go straight to the isolated subagent
instead of the model first deciding whether to consult a skill or subagent
at all. Do this by default in Claude Code. Reach for the **keyword-triggered
skill** only on surfaces where explicit subagent naming isn't possible —
plain chat, a Project, or Cowork.

## What's in this folder

20 skill folders, one per FP&A role, each validated against the Skills spec
(kebab-case `name`, ≤1024-char `description`, no other frontmatter beyond
what's allowed). Each `SKILL.md` carries the same method, required inputs,
controls/boundaries, and output contract as its matching subagent, adapted
for a surface that may not have file access (chat) as well as one that does
(Cowork, a Project with sources, Claude Code).

| Skill | Matches subagent | Stage |
|---|---|---|
| `budget-architect` | `.claude/agents/01-budget-architect.md` | Plan |
| `driver-based-forecaster` | `02-driver-based-forecaster.md` | Plan |
| `scenario-modeler` | `03-scenario-modeler.md` | Plan |
| `capital-allocation` | `04-capital-allocation.md` | Plan |
| `cash-flow-manager` | `05-cash-flow-manager.md` | Operate |
| `working-capital-optimizer` | `06-working-capital-optimizer.md` | Operate |
| `spend-controller` | `07-spend-controller.md` | Operate |
| `revenue-margin-monitor` | `08-revenue-margin-monitor.md` | Operate |
| `close-coordinator` | `09-close-coordinator.md` | Close |
| `reconciliation-reviewer` | `10-reconciliation-reviewer.md` | Close |
| `variance-investigator` | `11-variance-investigator.md` | Close |
| `controls-compliance-monitor` | `12-controls-compliance-monitor.md` | Close |
| `fpa-analyst` | `13-fpa-analyst.md` | Decide |
| `profitability-mapper` | `14-profitability-mapper.md` | Decide |
| `pricing-strategist` | `15-pricing-strategist.md` | Decide |
| `business-case-builder` | `16-business-case-builder.md` | Decide |
| `management-report-writer` | `17-management-report-writer.md` | Communicate |
| `cfo-narrative-builder` | `18-cfo-narrative-builder.md` | Communicate |
| `board-deck-packager` | `19-board-deck-packager.md` | Communicate |
| `executive-qa-simulator` | `20-executive-qa-simulator.md` | Communicate |

Use `AGENT_ROUTING.md` (repo root) to pick the right one for a task — it
applies equally to the skill and the subagent version.

## How to install these on each surface

### 1. Claude Code (this repo, or any repo you copy `.claude/skills/` into)

Nothing to install. Claude Code auto-discovers project skills at
`.claude/skills/<name>/SKILL.md`, the same way it discovers
`.claude/agents/`. If this repo was already open when the skills were added,
start a new session (or restart) once so they're picked up — same rule as
for the subagents.

**But remember the efficiency tip above**: in Claude Code, prefer naming the
subagent directly over relying on the skill to trigger.

### 2. claude.ai chat (personal skills, not tied to any one repo)

1. Go to **claude.ai → Settings → Capabilities**.
2. Find the **Skills** section and make sure Skills are enabled for your
   account.
3. Upload each `.skill` file (a zipped skill folder — you were sent 20 of
   them, one per role) using the upload/**Save skill** option there. If you
   received the `.skill` files as file cards in a Claude conversation, each
   card shows a **Save skill** button directly — click it and the skill
   installs into your profile without a manual upload.
4. Once installed, any new chat can trigger the skill automatically when
   your message matches its description — e.g. "help me build a 13-week
   cash flow forecast" should bring in `cash-flow-manager`.

Exact menu wording can shift as Anthropic ships UI changes — if "Skills"
isn't under **Capabilities**, check **Settings** generally; the upload
mechanism is the part that's stable.

### 3. Claude Projects

Projects can carry their own skills in addition to (or instead of) your
account-wide ones:

1. Open the Project → **Project settings**.
2. Look for a **Skills** section scoped to that Project.
3. Attach the skills relevant to that Project — for an FP&A-only project,
   attaching all 20 makes sense; for a narrower project (e.g. just board
   reporting), attach `management-report-writer`, `cfo-narrative-builder`,
   `board-deck-packager`, and `executive-qa-simulator` to keep the
   Project's context lighter.
4. Skills attached at the account level (step 2 above) are usually also
   available inside Projects — attaching at the Project level is for
   scoping which ones are relevant to that Project's work, and for
   Project-only custom skills you don't want everywhere.

### 4. Cowork

Cowork uses the same underlying Skills mechanism as claude.ai. If you
received the `.skill` files as file cards in this conversation, each card's
**Save skill** button installs it into your profile the same way it does in
chat, provided your organization allows skill creation — if it doesn't,
your Cowork admin needs to enable that first, or install these on your
behalf.

## What still needs a human, regardless of surface

These skills carry the exact same controls as their subagent counterparts:
read-only analysis, `[OPEN]`-labeled gaps instead of invented numbers, no
ledger posting or external distribution, and a named human gate before
anything goes external. Installing them everywhere doesn't change who signs
off — it changes how many extra clicks it takes to get a draft in front of
that person.
