# User Stories

## Authentication

- Register
- Login
- Logout

## Accounts User Stories

### Create Account

**User Story**

As a user, I want to create a financial account so that I can track its balance and the transactions associated with it.

**Required Information**

- Account name
- Account type
- Opening balance
- Currency

**Business Rules**

- Account name is required.
- Account name must be unique for each user.
- Account type is required.
- Opening balance is required.
- Opening balance may be positive, zero, or negative.
- Currency is required.

### View Accounts

As a user, I want to view all my accounts and their current balances so that I can understand where my money is stored.

### View Total Balance

As a user, I want to view the combined balance of all active accounts so that I can understand how much money I currently have.

### Edit Account

As a user, I want to edit an account’s details so that I can correct or update its information.

### Archive Account

As a user, I want to archive an account that I no longer use so that it does not appear in my active accounts while its transaction history remains available.

### Delete Account

As a user, I want to delete an account that was created by mistake so that unnecessary accounts are removed from the system.

## Transactions

- Record income
- Record an expense
- Transfer money between accounts
- Record a loan given
- Record a loan repayment
- Edit a transaction
- Delete a transaction
- View transactions
- Filter by date
- Filter by account
- Filter by category
- Filter by transaction type

## Loans

- Record a loan given
- Record a partial or full repayment
- View a loan and its repayment history
- View pending loans
- View completed loans
- View total outstanding amount by counterparty

## Reports

- View daily summary
- View monthly summary
- View yearly summary
- View account balances
- View category-wise spending

## Categories

- Create a category
- Edit a category
- Archive a category
- View categories

## Counterparties

- Create a counterparty
- Edit a counterparty
- View transactions with a counterparty
