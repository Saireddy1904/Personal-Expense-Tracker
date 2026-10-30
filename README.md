 # Personal Expense Tracker — SQL Mini Project 1

A beginner-friendly MySQL project for practicing data retrieval, filtering, sorting, and summary queries. The sample dataset contains 60 personal expenses across October and November 2026.

## Project goals
By completing this project, you will practice:

- Creating a table with appropriate data types and constraints
- Inserting rows into a table
- Selecting and filtering records with `SELECT` and `WHERE`
- Sorting results with `ORDER BY`
- Summarizing data with `COUNT`, `SUM`, `AVG`, `MIN`, and `MAX`
- Grouping results with `GROUP BY` and filtering groups with `HAVING`
- Categorizing values with `CASE`

## Requirements

- MySQL 8.0.16 or later (for enforced `CHECK` constraints)
- MySQL Workbench, the MySQL command-line client, or another MySQL-compatible SQL editor

## 1. Create the database and table

```sql
CREATE DATABASE expense_tracker;
USE expense_tracker;

CREATE TABLE expenses (
    expense_id    INT AUTO_INCREMENT PRIMARY KEY,
    expense_date  DATE NOT NULL,
    category      VARCHAR(20) NOT NULL,
    description   VARCHAR(40),
    amount        DECIMAL(10, 2) NOT NULL CHECK (amount > 0),
    payment_type  VARCHAR(30)
);
```

`expense_id` is generated automatically. `DECIMAL(10, 2)` stores money values precisely to two decimal places. The `CHECK` constraint rejects amounts that are zero or less.

## 2. Insert sample data

```sql
INSERT INTO expenses
    (expense_date, category, description, amount, payment_type)
VALUES
    ('2026-10-01', 'Food',          'Groceries',                42.50, 'Card'),
    ('2026-10-02', 'Transport',     'Metro recharge',           15.00, 'Card'),
    ('2026-10-03', 'Food',          'Lunch',                     8.75, 'Cash'),
    ('2026-10-04', 'Entertainment', 'Movie ticket',             12.00, 'Card'),
    ('2026-10-05', 'Bills',         'Mobile plan',               9.99, 'UPI'),
    ('2026-10-06', 'Food',          'Dinner',                    21.40, 'UPI'),
    ('2026-10-07', 'Transport',     'Taxi ride',                 18.25, 'Card'),
    ('2026-10-08', 'Shopping',      'Notebook and pens',           6.80, 'Cash'),
    ('2026-10-09', 'Food',          'Coffee',                     4.50, 'Card'),
    ('2026-10-10', 'Bills',         'Internet bill',             30.00, 'UPI'),
    ('2026-10-11', 'Health',        'Pharmacy',                  14.25, 'Card'),
    ('2026-10-12', 'Food',          'Bakery items',               7.60, 'Cash'),
    ('2026-10-13', 'Transport',     'Bus pass',                  22.00, 'UPI'),
    ('2026-10-14', 'Shopping',      'T-shirt',                   24.99, 'Card'),
    ('2026-10-15', 'Food',          'Groceries',                 36.80, 'UPI'),
    ('2026-10-16', 'Entertainment', 'Music subscription',         5.99, 'Card'),
    ('2026-10-17', 'Food',          'Lunch',                    11.50, 'Cash'),
    ('2026-10-18', 'Bills',         'Electricity bill',          48.75, 'UPI'),
    ('2026-10-19', 'Transport',     'Auto ride',                  9.50, 'Cash'),
    ('2026-10-20', 'Food',          'Dinner',                    18.90, 'Card'),
    ('2026-10-21', 'Health',        'Doctor visit',              35.00, 'Card'),
    ('2026-10-22', 'Shopping',      'Phone charger',             16.99, 'UPI'),
    ('2026-10-23', 'Food',          'Coffee and snack',            6.25, 'Cash'),
    ('2026-10-24', 'Transport',     'Metro recharge',            15.00, 'UPI'),
    ('2026-10-25', 'Entertainment', 'Concert ticket',            45.00, 'Card'),
    ('2026-10-26', 'Food',          'Groceries',                 53.20, 'Card'),
    ('2026-10-27', 'Bills',         'Water bill',                 8.50, 'UPI'),
    ('2026-10-28', 'Food',          'Lunch',                     10.75, 'Cash'),
    ('2026-10-29', 'Transport',     'Taxi ride',                 21.60, 'Card'),
    ('2026-10-30', 'Shopping',      'Household supplies',        27.40, 'UPI'),
    ('2026-11-01', 'Food',          'Groceries',                 39.80, 'Card'),
    ('2026-11-02', 'Transport',     'Bus fare',                   3.00, 'Cash'),
    ('2026-11-03', 'Food',          'Lunch',                      9.25, 'UPI'),
    ('2026-11-04', 'Bills',         'Mobile plan',                9.99, 'UPI'),
    ('2026-11-05', 'Health',        'Vitamins',                  12.80, 'Card'),
    ('2026-11-06', 'Entertainment', 'Movie ticket',              12.00, 'Card'),
    ('2026-11-07', 'Food',          'Dinner',                    23.50, 'Cash'),
    ('2026-11-08', 'Shopping',      'Water bottle',              11.99, 'UPI'),
    ('2026-11-09', 'Transport',     'Metro recharge',            15.00, 'Card'),
    ('2026-11-10', 'Food',          'Coffee',                     4.75, 'Cash'),
    ('2026-11-11', 'Bills',         'Internet bill',             30.00, 'UPI'),
    ('2026-11-12', 'Food',          'Groceries',                 47.60, 'Card'),
    ('2026-11-13', 'Transport',     'Taxi ride',                 19.80, 'UPI'),
    ('2026-11-14', 'Shopping',      'Headphones',                39.99, 'Card'),
    ('2026-11-15', 'Food',          'Lunch',                     12.40, 'Cash'),
    ('2026-11-16', 'Health',        'Pharmacy',                  18.35, 'UPI'),
    ('2026-11-17', 'Entertainment', 'Book purchase',             14.50, 'Card'),
    ('2026-11-18', 'Food',          'Dinner',                    20.25, 'UPI'),
    ('2026-11-19', 'Bills',         'Electricity bill',          51.20, 'UPI'),
    ('2026-11-20', 'Transport',     'Bus pass',                  22.00, 'Card'),
    ('2026-11-21', 'Food',          'Bakery items',               8.90, 'Cash'),
    ('2026-11-22', 'Shopping',      'Kitchen utensils',          31.75, 'Card'),
    ('2026-11-23', 'Food',          'Groceries',                 44.10, 'UPI'),
    ('2026-11-24', 'Transport',     'Auto ride',                 10.50, 'Cash'),
    ('2026-11-25', 'Entertainment', 'Game subscription',          7.99, 'Card'),
    ('2026-11-26', 'Food',          'Lunch',                     10.20, 'UPI'),
    ('2026-11-27', 'Health',        'Dental checkup',            40.00, 'Card'),
    ('2026-11-28', 'Bills',         'Water bill',                 8.50, 'UPI'),
    ('2026-11-29', 'Food',          'Dinner',                    19.60, 'Cash'),
    ('2026-11-30', 'Shopping',      'Cleaning supplies',         17.25, 'UPI');
```

Confirm the insert:

```sql
SELECT COUNT(*) AS total_expenses
FROM expenses;
```

Expected result: `60`.

## 3. Practice questions

### Level 1 — Select, filter, and sort

1. Display every expense.
2. Display only the date, category, description, and amount.
3. Find all expenses paid using `UPI`.
4. Find all expenses in the `Food` category.
5. Show expenses greater than 20, ordered from highest to lowest amount.
6. Find expenses from October 10 through October 20, 2026, including both dates.
7. Find expenses whose description contains the word `ride`.
8. Show the five most expensive expenses.

### Level 2 — Aggregate functions

9. Calculate the total amount spent.
10. Count the expense records.
11. Find the average, largest, and smallest expense amounts.
12. Calculate total spending for each category.
13. Count the expenses for each payment type.
14. Calculate the average expense amount for each category.
15. Calculate the total amount spent using each payment type.

### Level 3 — Grouping and business questions

16. Show categories where total spending is greater than 100.
17. Find categories with at least five expense records.
18. Calculate the number of expenses and total spending for each month.
19. Find the category with the highest total spending.
20. Find the payment type used for the most expenses.
21. Show expenses that are above the overall average expense amount.
22. Label each expense `Small` if below 10, `Medium` if from 10 through 30, and `Large` if above 30.

## 4. Starter queries

Use these as examples, then adapt them to answer the questions above.

```sql
-- View expenses, newest first
SELECT *
FROM expenses
ORDER BY expense_date DESC;

-- Total spending by category
SELECT category, SUM(amount) AS category_total
FROM expenses
GROUP BY category
ORDER BY category_total DESC;

-- Categories with total spending above 100
SELECT category, SUM(amount) AS category_total
FROM expenses
GROUP BY category
HAVING SUM(amount) > 100
ORDER BY category_total DESC;
```

## Notes

- The amounts are sample values with no currency specified. Choose one currency and state it if you use the results in a portfolio.
- The dates and records are fictional and intended for SQL practice.
- To rerun the insert, clear the table first with `TRUNCATE TABLE expenses;` or recreate the database. `TRUNCATE` removes all rows and resets the auto-increment counter.

## Suggested portfolio extension

After answering the questions, write a short summary of the three categories with the highest total spending and compare October with November. Include the SQL queries and explain what each result tells you.
