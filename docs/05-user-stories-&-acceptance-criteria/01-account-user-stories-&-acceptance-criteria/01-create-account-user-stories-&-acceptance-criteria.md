# Feature: Create Account

## User Story

As a user, I want to create a financial account so that I can track its balance and the transactions associated with it.

## Required Information

- Account name
- Account type
- Opening balance
- Currency

## Business Rules

- Account name is required.
- Account name must be unique for each user.
- Account-name uniqueness must be checked case-insensitively.
- Leading and trailing spaces in the account name must be ignored when checking uniqueness.
- Account type is required.
- Opening balance is required.
- Opening balance may be positive, zero, or negative.
- Currency is required.

## Acceptance Criteria

### Successful Account Creation

**Given** the user has entered:

- A unique account name
- An account type
- An opening balance
- A currency

**When** the user submits the account creation form,

**Then** the account should be created successfully,

**And** the account should be displayed in the user's accounts list.

### Duplicate Account Name

**Given** the user has entered an account name that already exists in their accounts,

**And** the difference is only capitalization or surrounding spaces,

**When** the user submits the account creation form,

**Then** the account must not be created,

**And** the user should see an error message explaining that the account name is already in use.

### Missing Required Information

**Given** the user has left one or more required fields empty,

**When** the user submits the account creation form,

**Then** the account must not be created,

**And** the user should see validation messages identifying the missing required fields.
