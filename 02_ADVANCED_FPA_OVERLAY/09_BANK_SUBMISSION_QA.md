# Bank Submission Financial Model QA

## Objective
Ensure a financial model is internally consistent, traceable and suitable for bank review before human approval.

## Required checks
### Structure
- Assumptions consolidated as required.
- P&L, Balance Sheet, Cash Flow, covenant and debt tabs present.
- Supporting tabs limited to necessary schedules.
- No unnecessary external workbook links.

### Historical data
- Historical actuals preserved.
- Forecast boundary clearly identified.

### Forecast
- Forecast methodology documented.
- Key assumptions traceable.
- Quarterly and annual totals reconcile.
- Material movements explainable.

### Statements
- P&L reconciles.
- Balance Sheet balances.
- Cash flow reconciles to cash.
- Debt schedule reconciles.
- Interest schedule reconciles where applicable.

### Covenants
- Definitions match approved/contractual definitions.
- Inputs trace to model statements.
- Calculations independently checked.
- Headroom correctly calculated.

### Submission hygiene
- No #REF!, #VALUE!, #DIV/0!, #N/A errors unless explicitly expected.
- No accidental hidden logic.
- No broken named ranges.
- No inconsistent formulas.
- No unexplained hardcodes.
- No obsolete external links.
- Formatting and units are consistent.

## Release rule
Do not describe the workbook as bank-ready merely because the model calculates. Report:
- PASS
- PASS WITH EXCEPTIONS
- FAIL

and list all material exceptions.

Final submission remains subject to human finance approval.
