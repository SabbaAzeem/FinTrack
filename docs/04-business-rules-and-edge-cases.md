# Business Rules

## Transaction Type: Income

Required:

- Date
- Type: Income
- Category
- Amount
- Destination Account
- Counter Party

Optional:

- Notes (Description)

## Transaction Type: Expense

Required:

- Date
- Type: Expense
- Category
- Amount
- Source Account
- Counter Party

Optional:

- Notes

## Transaction Type: Transfer

Required:

- Date
- Type: Transfer
- Amount
- Source Account
- Destination Account

Optional:

- Category
- Notes

## Transaction Type: Loan Given

Required:

- Date
- Type: Loan Given
- Amount
- Counterparty
- Source Account

Optional:

- Notes

## Transaction Type: Loan Repayment Received

Required:

- Date
- Type: Loan Repayment Received
- Amount
- Counterparty
- Destination Account
- Related Loan

Optional:

- Notes

# Validation Rules

## Transaction Type: Transfer

- Source & Destination account can't be the same.
- Amount must be greater than zero.
- Source account must have enough balance.

## Transaction Type: Loan Given

- Amount must be greater than zero.
- Source account must have enough balance.

## Transaction Type: Loan Repayment Received

- Amount must be greater than zero.
- A related loan must exist.
- The related loan must not already be fully repaid.
- Repayment amount cannot be greater than the remaining loan amount.

## Transaction Type: Income

- Amount must be greater than zero.

## Transaction Type: Expense

- Amount must be greater than zero.
- Source account must have enough balance.

# Edit/delete behavior

## What happens if a transaction is edited or deleted?

- Account balances must be recalculated using the updated transaction history.
- If a transfer is edited or deleted, both source and destination account balances must be recalculated.
- If a loan repayment is edited or deleted, the remaining loan amount must also be recalculated.

## Deleting a Transaction

- A deleted transaction is marked as deleted instead of being permanently removed.
- Deleted transactions must not affect account balances, reports, or loan balances.
- The original transaction data remains available for history.

## Editing a Transaction

- The existing transaction is updated with the new values.
- Account balances, reports, and related loan balances are recalculated using the latest active, non-deleted transactions.
- Complete transaction edit history may be added later for audit purposes.

# Edge-Cases

## Can an account balance become negative?

- Each account has an `allowNegativeBalance` rule.
- By default, Cash, Bank, Savings, and JazzCash cannot become negative.
- Accounts such as Credit Card or Overdraft may allow negative balances.

## Should negative-balance behavior be fixed by account type, or configurable for each account?

- Negative balance behavior will be fixed by account type.
- Cash, Bank, Savings, and JazzCash accounts cannot have a negative balance.
- Credit Card or Overdraft account types may allow a negative balance in the future.

## Can a transaction be added with a past or future date?

- A transaction may be recorded with today’s date or a past date.
- A transaction cannot be recorded with a future date.

## What should happen if a user edits an old transaction and the recalculated balance becomes negative?

- Past transactions may be added or edited even if recalculation produces a negative account balance.
- FinTrack should warn the user that the account balance becomes negative.
- The user may continue after confirming the warning.
- The negative balance indicates that earlier records may be incomplete or incorrect.

## What should happen if the user changes an existing transaction from one type to another, such as Expense → Transfer?

- A transaction type may be changed.
- The transaction must provide all fields required by the new type.
- Fields that no longer apply should be removed or ignored.
- All affected account balances, reports, and loan balances must be recalculated.
- The change must be rejected if it creates an invalid transaction.

Example: When changing an Expense into a Transfer, a destination account must be selected.

## Deleting an Account

- An account with existing transactions cannot be permanently deleted.
- The account may be marked as archived.
- Archived accounts remain visible in old transaction history and reports.
- New transactions cannot use an archived account.
- Its balance continues to be calculated from its existing active transactions.

## What should happen if the user wants to archive an account that still has a balance?

- An account should not be archived while its balance is not zero.
- The user must first transfer or adjust the remaining balance.
- FinTrack should show the current balance and explain why the account cannot be archived.
- Once the balance becomes zero, the account may be archived.

## What should happen if a category is deleted but old transactions still use it?

- A category used by existing transactions is archived instead of permanently deleted.
- Existing transactions continue to show the archived category.
- Archived categories cannot be selected for new transactions.
- No replacement category is required.

## What should happen if a loan repayment is deleted or edited after the loan was marked as completed?

- The related loan’s remaining amount must be recalculated.
- If the remaining amount becomes greater than zero, the loan status changes from **Completed** back to **Pending**.
- If the recalculated remaining amount is zero, the loan remains **Completed**.
- Account balances and reports must also be recalculated.

## What should happen if a user gives another loan to the same person while an earlier loan is still pending?

- Each new loan given creates a separate loan record, even when the same counterparty already has a pending loan.
- Each loan keeps its own amount, date, repayments, remaining balance, and status.
- FinTrack may show the combined outstanding amount for that counterparty as a calculated summary.
- The combined total must not replace or merge the individual loan records.

## What should happen if a repayment is received from someone who has multiple pending loans?

- The user must select which pending loan the repayment belongs to.
- The repayment reduces the remaining balance of that selected loan.
- If its remaining balance becomes zero, that loan is marked as completed.
- Other pending loans remain unchanged.
- The counterparty’s total outstanding amount is recalculated automatically.

## What should happen if the received repayment amount is greater than the selected loan’s remaining balance?

- A repayment cannot be directly recorded for more than the selected loan’s remaining amount.
- FinTrack should show the excess amount to the user.
- The user must decide how to record the excess amount, such as income, a gift, or repayment toward another loan.
- The selected loan is completed after its full remaining amount is repaid.

## What should happen when the user creates their first account with money already inside it?

- When creating an account that already contains money, the existing amount is recorded as its opening balance.
- Opening balance affects the account’s current balance.
- Opening balance is not treated as income.
- Opening balance must not appear in income or monthly earning reports.
- The account creation date may be used as the opening-balance date.
