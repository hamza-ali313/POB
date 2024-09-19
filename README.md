Create Loan
Flow of the Loops

Outer Loop: {% for row in doc.loans %}

This loop iterates over each record in the doc.loans list.
For each row in doc.loans, 
the following operations are performed:

Initialization of loan_amount: {%- set loan_amount = 0 -%}.

This initializes the variable loan_amount to 0 for each row in doc.loans.

Inner Loop: {% for loan in loans %}

Inside the outer loop, this loop iterates over each record in the loans list fetched from the Loan DocType.

For each loan in loans, the following operations are performed:
Condition Check: {%- if row.account == loan.name -%}

Compares row.account (from doc.loans) with loan.name (from the loans list).

If the account matches the name of a loan, it sets loan_amount to loan.loan_amount.
This means that if there's a match, loan_amount is updated with the loan_amount value of the matching loan.
After the Inner Loop Completes

After the inner loop has finished checking all loans, the outer loop continues.
At this point, loan_amount should hold the value from the matching loan (or 0 if no match was found).
Creating Table Rows

Row Creation: <tr> creates a table row for each row in doc.loans.
Displaying Data:
<td>{{ row.loan_account }}</td>: Displays the loan_account from the current row.
<td>{{ row.total_payment }}</td>: Displays the total_payment from the current row.
<td>{{ loan_amount - row.total_payment }}</td>: Calculates and displays the balance by subtracting row.total_payment from loan_amount.
Example Scenario
Suppose doc.loans contains:

json
Copy code
[
  { "account": "LOAN-001", "loan_account": "Personal Loan", "total_payment": 1000 },
  { "account": "LOAN-002", "loan_account": "Car Loan", "total_payment": 500 }
]

And loans contains:

json
[
  { "name": "LOAN-001", "loan_amount": 5000 },
  { "name": "LOAN-002", "loan_amount": 2000 }
]

Detailed Flow:

First Iteration of Outer Loop (row = { "account": "LOAN-001", "loan_account": "Personal Loan", "total_payment": 1000 }):

Inner Loop:
First Iteration (loan = { "name": "LOAN-001", "loan_amount": 5000 }):
Match found (row.account == loan.name), so loan_amount is set to 5000.
Second Iteration (loan = { "name": "LOAN-002", "loan_amount": 2000 }):
No match (continue checking, but loan_amount remains 5000).
Row Creation:
<td>Personal Loan</td>
<td>1000</td>
<td>5000 - 1000 = 4000</td>
Second Iteration of Outer Loop (row = { "account": "LOAN-002", "loan_account": "Car Loan", "total_payment": 500 }):

Inner Loop:
First Iteration (loan = { "name": "LOAN-001", "loan_amount": 5000 }):

No match (continue checking).
Second Iteration (loan = { "name": "LOAN-002", "loan_amount": 2000 }):
Match found (row.account == loan.name), so loan_amount is set to 2000.
Row Creation:
<td>Car Loan</td>
<td>500</td>
<td>2000 - 500 = 1500</td>
Summary:
The outer loop iterates through doc.loans, and for each row, it looks up the corresponding loan_amount from the loans list using the inner loop.
It then calculates the balance and constructs a table row with the loan_account, total_payment, and the calculated balance for each record.
