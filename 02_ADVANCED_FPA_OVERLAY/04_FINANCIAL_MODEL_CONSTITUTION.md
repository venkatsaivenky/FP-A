# Financial Model Constitution

## Fundamental rules
1. Actual historical data must not be changed unless explicitly authorized.
2. Forecast logic must be formula-driven.
3. Approved assumptions must have a clear source.
4. Avoid hardcoding calculated forecast outputs.
5. Avoid unnecessary external workbook dependencies.
6. Preserve auditability.
7. Maintain consistent units and signs.
8. Every material output should be traceable back to a source or assumption.

## Architecture
Preferred structure:
Assumptions → Supporting calculations → P&L / Balance Sheet / Cash Flow → Covenants / Outputs.

## Assumptions
Centralize assumptions where practical.
Each assumption should have:
- description;
- value;
- period;
- unit;
- source;
- status;
- applicable model line.

## Financial statements
P&L:
- Revenue lines should reconcile to total revenue.
- Gross profit and EBITDA should reconcile to underlying lines.
- Margin percentages must use the correct denominator.

Balance Sheet:
- Assets = Liabilities + Equity.
- Opening balances must tie to prior closing balances.

Cash Flow:
- Opening cash + net cash movement = closing cash.
- Closing cash must tie to the Balance Sheet cash figure where the model architecture requires it.

Debt:
- Opening debt + drawdowns - repayments + other approved movements = closing debt.
- Closing debt must reconcile to the Balance Sheet.

Covenants:
- Every covenant numerator and denominator must trace to the relevant statement or approved definition.
- Covenant definitions must not be inferred where contractual definitions are available.

## Bank submission standard
Before submission:
- eliminate unintended external links;
- validate formulas;
- validate statements;
- validate debt and covenants;
- review hidden sheets and rows;
- confirm assumptions;
- remove unnecessary working tabs;
- ensure the workbook is understandable to an independent reviewer.

## Change control
When modifying a model:
- identify the requested change;
- identify impacted formulas;
- preserve unrelated logic;
- test before and after;
- report material changes.
