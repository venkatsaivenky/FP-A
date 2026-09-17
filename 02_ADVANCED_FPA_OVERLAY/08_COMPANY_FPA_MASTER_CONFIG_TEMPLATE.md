# Company FP&A Master Configuration

> Replace every [CONFIGURE] item with the company's approved information. Do not invent values.

**Status: PARTIALLY CONFIGURED.** Fields marked `[DERIVED]` were read directly off the
structure of `QFM Management Accounts-working.xlsx` (P&L Raw Data / Twincube data / Budget
(AOP) / Store Master / Mapping tabs) — sheet names, GL-to-P&L-line mappings, entity lists, and
formula logic actually present in that file. They are facts about the file, not finance policy,
so they still need a named approver's sign-off before agents treat them as authoritative. Fields
marked `[CONFIGURE]` could not be derived from the file at all (no balance sheet, no policy
statements, no named individuals) and remain genuinely blank. **Until every `[CONFIGURE]` is
replaced, treat this file as unset per `CLAUDE.md` §6.**

## ⚠ Data-quality finding (read before using this config)

The source workbook's live P&L is currently **blank at the root**, not just unfilled:

- `Twincube data` (242,925 GL posting rows) has every dimension populated — period, brand,
  entity, GL account, cost-centre — **except the two amount columns, `Base value` and
  `Reporting amount`, which are 100% empty across all rows.**
- `P&L Raw Data` pulls every store/period cell via `SUMIFS(...'Twincube data'!$V:$V...)`
  (col V = Reporting amount). Since that column is empty, **every P&L line for every store,
  brand, and period sums to zero** — Store Sales, Gross Profit, EBITDA, Profit After Tax, all
  of it. This is a broken data extract, not a low-revenue period.
- `Budget (AOP)` is also 100% blank (0 of 9,153 checked cells populated) — no FY26 AOP has
  been loaded, so no actual-vs-budget variance is possible even once actuals are fixed.
- Secondary, smaller issue: 13 of 315 store/entity combinations referenced in `P&L Raw Data`
  don't exist in `Twincube data`'s keys, including one row where Company Name is hardcoded as
  the literal string `"Head Office"` (concat `A01Head Office`) instead of a real legal entity —
  that row can never match and silently drops whatever it was meant to carry.
- The `Mapping` tab's period calendar (see Calendar section below) dates FY26 as starting
  29-Dec-2026, which is inconsistent with `P&L Raw Data` already carrying periods P1_26–P10_26
  as of today. One of the two is mislabeled.

**Recommended fix path:** ask whoever owns the Twincube/GL export to re-pull with the
`Base value`/`Reporting amount` columns included (this looks like a column dropped in export,
not a formula break — every other field came through intact). Re-check the 13 orphaned
store/entity keys and the `A01Head Office` row against Store Master once real postings land.
Load the FY26 AOP before expecting variance output. This is exactly what the
`fpa-excel-auditor` overlay (`02_FPA_EXCEL_AUDITOR.md`) and the `reconciliation-reviewer` agent
are for — recommend running both once the export is repaired.

## Company
Company name: [CONFIGURE — group/trading name not stated in the file; e.g. holding company name]
Reporting entity: `[DERIVED]` Multi-entity UK group operating across the following legal
entities (from `Store Master` / `Twincube data`):
- Chicken Villas Limited
- Fieldrose Limited
- Intracave Limited
- Kuna Pension Scheme
- Mulcroft Limited
- Northgate Fast Food Limited
- Queenscourt Limited
- S.P.Q. Limited
- Brightside Foods Limited
- Tanaan Holdings Limited
- BM Kuna Property Developments Limited
- Icoffee Limited (+ Icoffee - Rhyl Limited, Icoffee - Selby Limited, Icoffee - Tunstall Limited)
- Revero Foods Limited
- G-CSDK Limited
- Consolidation Company (elimination/consolidation entity — not an operating entity)

Primary currency: [CONFIGURE — not stated explicitly; cost lines use UK-specific terms
(National Insurance, Apprenticeship Levy, Business Rates), so GBP is a reasonable working
assumption, but confirm before treating as policy]
Reporting units: `[DERIVED]` Store level → Brand level → Legal entity level → Consolidated
group, per `Store Master` (331 stores: 208 Active, 116 Closed, 7 Pending) and brand split of
active trading stores — KFC 41, Taco Bell 28, Dunkin' 12, JIM 1, plus 109 Property-only
entries and a closed/pending Costa (Icoffee) estate.

## Calendar
Fiscal year start: [CONFIGURE — `Mapping` tab says FY26 starts 29-Dec-2026, but `P&L Raw Data`
already has periods P1_26 through P10_26 recorded, which can't both be true as of today
(2026-09-17). Confirm the real FY26 start date with the source-system owner before relying on
either.]
Fiscal year end: [CONFIGURE — same conflict as above]
Quarter definitions: `[DERIVED]` No explicit quarter grouping in the file; the year is built
from 13 sequential periods (P1–P13), so quarters would need to be defined as a periods-per-Q
convention (e.g. 4-4-5 vs. 5-4-4) — confirm which grouping finance actually uses for quarterly
reporting.
Month-end convention: `[DERIVED]` Not calendar-month based. Per the `Mapping` tab: "Each
Management period = 28 days" — a fixed 13 × 28-day period calendar (364 days/year), i.e. a UK
retail-style 13-period year, not a 12-month calendar.

## Accounting
Accounting framework: [CONFIGURE — not stated in file; UK private limited entity structure
suggests UK GAAP (FRS 102) but this is an inference, not a sourced fact]
Revenue recognition policy reference: [CONFIGURE]
EBITDA definition: `[DERIVED — house formula, taken verbatim from the live P&L Raw Data
formulas]`
`EBITDA = Operating Profit − Consultancy & Professional Fees − Audit & Accountancy − Other
Income & Expenses`
where `Operating Profit = Gross Profit − Total Operating Costs`, and `Total Operating Costs =
Total Labour Cost + Direct Costs-Brand + Property & Insurance + Smallwares & Staff Related +
Non-Brand Audits + Premises Cost + Financial + Utilities + Technology Costs + Maintenance
Charges + Repair Expenses + Variable Costs-Other`.
**Flag for review:** this EBITDA formula excludes Interest and *subtracts* Other Income &
Expenses, while the model's own PBDIT line (`Operating Profit − Consultancy & Professional
Fees − Audit & Accountancy + Other Income & Expenses + Interest Income and Expense`) *adds*
Other Income & Expenses back. Same line item, opposite sign treatment between the two
subtotals in the same workbook — worth a formula audit before either is quoted externally
(bank pack, board pack).
Adjusted EBITDA definition: [CONFIGURE — no add-back/exceptional-items schedule exists in the
file beyond a raw "Exceptional Costs" GL group; confirm which items finance actually adjusts
out]
Net debt definition: [CONFIGURE — file is P&L-only, no balance sheet/debt schedule present]
Working capital definition: [CONFIGURE — file is P&L-only, no balance sheet present]

## Planning
AOP definition: [CONFIGURE — `Budget (AOP)` tab exists with the right shape (Store × Brand ×
Period × COS%/Oil%/Labour%/EBITDA% × £ COS/Oil/Labour/EBITDA) but is currently 100% blank; no
AOP has been loaded for FY26]
Budget definition: [CONFIGURE]
Forecast definition: [CONFIGURE]
Latest Estimate definition: [CONFIGURE]
Actuals cut-off rule: [CONFIGURE]

## KPIs
Approved KPI list: [CONFIGURE — not stated as policy, but the Budget (AOP) tab's own column
headers imply these are the KPIs finance already tracks per store; confirm before adopting]
- Channel Sales vs. AOP (£ and %)
- Cost of Sales % (COS %)
- Oil % (a QSR-specific COS sub-metric — oil cost as % of sales)
- Labour %
- EBITDA % (AOP EBITDA % vs. actual)

## Materiality
Management materiality threshold: [CONFIGURE]
Board materiality threshold: [CONFIGURE]
Covenant materiality rules: [CONFIGURE]

## Source hierarchy
`[DERIVED]` Inferred from the workbook's own formula chain (this is how the model itself
already treats source precedence — confirm it matches finance's intended hierarchy):
1. `Twincube data` — GL posting extract (system of record for actuals; currently broken, see
   data-quality finding above)
2. `P&L Raw Data` — derived store/period P&L, built entirely from SUMIFS off Twincube data
   (never edit this directly; it recalculates from #1)
3. `Store Master` — entity/brand/status reference table used to key and validate #1 and #2
4. `Budget (AOP)` — FY26 plan, currently unloaded

## Management reporting
Required monthly pack structure: [CONFIGURE]
Required quarterly pack structure: [CONFIGURE]
Required commentary style: [CONFIGURE]

## Forecast methodology
Approved revenue methodology: [CONFIGURE]
Approved cost methodology: [CONFIGURE]
Approved NSO methodology: [CONFIGURE — "NSO" typically = New Store Opening in multi-unit
retail/QSR; confirm this is the intended meaning for this business before agents use it]
Approved growth methodology: [CONFIGURE]

## Governance
Model owner: [CONFIGURE]
Reviewer: [CONFIGURE]
Approver: [CONFIGURE]
Bank submission approver: [CONFIGURE]

## Important instruction
If an answer conflicts with this configuration, flag the conflict. Do not silently override
approved company policy.
