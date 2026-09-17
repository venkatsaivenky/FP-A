# FP&A Model QA Checklist

## A. File integrity
- [ ] Workbook opens successfully.
- [ ] Expected worksheets exist.
- [ ] No accidental duplicate sheets.
- [ ] No unexpected hidden sheets.
- [ ] No unexpected hidden rows/columns.
- [ ] Units are consistent.
- [ ] Currency is consistent.

## B. Actuals / forecast
- [ ] Actual periods identified correctly.
- [ ] Actual values unchanged.
- [ ] Forecast start date correct.
- [ ] Forecast formulas populate all intended periods.
- [ ] No accidental hardcodes in forecast ranges.

## C. Assumptions
- [ ] Assumptions are centralized as required.
- [ ] Each key assumption has a source.
- [ ] No duplicated contradictory assumptions.
- [ ] Assumptions flow into calculations.

## D. P&L
- [ ] Revenue lines reconcile.
- [ ] Cost lines reconcile.
- [ ] Gross profit correct.
- [ ] EBITDA correct.
- [ ] Margins correct.
- [ ] Quarterly totals reconcile to annual totals.

## E. Balance Sheet
- [ ] Balance Sheet balances.
- [ ] Opening balances tie to prior closing.
- [ ] Working capital is coherent.
- [ ] Equity movements are coherent.

## F. Cash Flow
- [ ] Opening cash is correct.
- [ ] Operating cash flow reconciles.
- [ ] Investing cash flow reconciles.
- [ ] Financing cash flow reconciles.
- [ ] Closing cash reconciles.

## G. Debt / covenant
- [ ] Debt schedule reconciles.
- [ ] Interest calculations are coherent.
- [ ] Covenant definitions are correct.
- [ ] Covenant inputs trace to statements.
- [ ] Headroom calculations are correct.

## H. Formula integrity
- [ ] No #REF!
- [ ] No #DIV/0!
- [ ] No #VALUE!
- [ ] No #N/A where unintended.
- [ ] No inconsistent formula patterns.
- [ ] No broken external links.
- [ ] No accidental circular references.

## I. Forecast methodology
- [ ] Approved growth rules applied.
- [ ] Same-quarter comparisons correct.
- [ ] YTD comparisons correct.
- [ ] NSO logic correct.
- [ ] No double counting.
- [ ] FY totals reconcile.

## J. Final release
- [ ] Material exceptions documented.
- [ ] Independent QA completed.
- [ ] Reviewer knows what changed.
- [ ] Final file is submission-ready only after human approval.
