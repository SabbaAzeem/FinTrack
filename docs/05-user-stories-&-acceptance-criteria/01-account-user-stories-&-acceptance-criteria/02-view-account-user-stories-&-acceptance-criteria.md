# Feature: View Accounts

## User Story

As a user, I want to view my all accounts and their current balances so that I can understand that where my money is held and how much money I have across my accounts.

## Display Information

For each account, the system should display:

- Account name
- Account type
- Current balance
- Currency
- Status: active or archived
- Total balance by currency

## Business Rules

- Only accounts belonging to the authenticated user must be displayed.
- The balance of each account must be displayed in that account's currency.
- Active and archived account must be clearly distinguishable.
- Archived accounts must not be included in the active account total by default.
- Accounts with different currencies must not be added together directly.
- Total balances must be grouped by currency.

## Acceptance Criteria

### Successful Case

**Given** the user is logged in and has one or more accounts,

**When** the user opens the Accounts section,

**then** the user's accounts should be displayed,

**And** each account should show its name, type, currency, current balance and status.