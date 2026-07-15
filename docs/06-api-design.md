Now every user action becomes an API.

For example

Authentication
```
POST /register

POST /login

POST /logout
```
Expense
```
GET /expenses

POST /expenses

GET /expenses/:id

PATCH /expenses/:id

DELETE /expenses/:id
```
Category
```
GET /categories

POST /categories
```
Notice you don't invent APIs—you derive them from user actions.
```
Include:

Request body
Response
Authentication requirements
Error cases
```