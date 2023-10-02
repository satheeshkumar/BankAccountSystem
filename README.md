# Bank Account


- input banking transactions
- calculate interest
- printing account statement

All the example below assumes console input/output is used. 


When launching the application, it prompts user for actions:
```
Welcome to AwesomeGIC Bank! What would you like to do?
[T] Input transactions 
[I] Define interest rules
[P] Print statement
[Q] Quit
>

User is then able to enter something like the following:

20230929 AC001 D 100.00
20230929 AC001 W 100.00
20230929 AC001 D 200.00
20230929 AC001 W 300.00

```

```
Account: AC001
| Date     | Txn Id      | Type | Amount |
| 20230505 | 20230505-01 | D    | 100.00 |
| 20230601 | 20230601-01 | D    | 150.00 |
| 20230626 | 20230626-01 | W    |  20.00 |
| 20230626 | 20230626-02 | W    | 100.00 |


## Define interest rule
Please enter interest rules details in <Date> <RuleId> <Rate in %> format 
User is then able to enter something like the following:
```
20230615 RULE03 2.20
```
Some constraints to note:
* Date should be in YYYYMMdd format
* RuleId is string, free format
* Interest rate should be greater than 0 and less than 100
* If there's any existing rules on the same day, the latest one is kept

Then system responds by listing all interest rules orderd by date:
(assuming there are already RULE01 and RULE02 in the system) 
```
Interest rules:
| Date     | RuleId | Rate (%) |
| 20230101 | RULE01 |     1.95 |
| 20230520 | RULE02 |     1.90 |
| 20230615 | RULE03 |     2.20 |



## Print Statement
Upon selecting Print statement option, application prompts user to select which account to print the statement for:

```
Please enter account and month to generate the statement <Account> <Year><Month>

When user enters the account
```
AC001 202306
```

System then responds with the following account statement, which shows all the transactions and interest for that month (transaction type for interest is I):
```
Account: AC001
| Date     | Txn Id      | Type | Amount | Balance |
| 20230601 | 20230601-01 | D    | 150.00 |  250.00 |
| 20230626 | 20230626-01 | W    |  20.00 |  230.00 |
| 20230626 | 20230626-02 | W    | 100.00 |  130.00 |
| 20230630 |             | I    |   0.39 |  130.39 |
```

How to apply the interest rule:
* Interest is applied on end of day balance
```
| Period              | Num of days | EOD Balance | Rate Id | Rate | Annualized Interest      |
| 20230601 - 20230614 | 14          | 250         | RULE02  | 1.90 | 250 * 1.90% * 14 = 66.50 |
| 20230615 - 20230625 | 11          | 250         | RULE03  | 2.20 | 250 * 2.20% * 11 = 60.50 |
| 20230626 - 20230630 |  5          | 130         | RULE03  | 2.20 | 130 * 2.20% *  5 = 14.30 |
(this table is provided to help you get an idea how the calculation is done, it should not be displayed in the output)
```
* Therefore total interest is: (66.50 + 60.50 + 14.30) / 365 = 0.3871 => 0.39
* The interest is credited at the last day of the month

## Quit
When user chooses to quit, user enters:
```
q
```

System responds with:
```
Thank you for banking with AwesomeGIC Bank.
Have a nice day!
```
