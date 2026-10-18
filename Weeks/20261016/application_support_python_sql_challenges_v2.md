# Enterprise Application Support Engineer
## Python & SQL Interview Challenges

These exercises are intended to be short technical checks rather than full coding interviews.

Target approximately:

- **5 minutes for Python**
- **5 minutes for SQL**

The goal is to determine whether the candidate can read and reason about basic Python and work with relational data using basic SQL.

---

# Challenge 1: Python Code Reading & Debugging

## Candidate Prompt

Review the following Python code.

```python
def process_records(records):
    processed = []
    failed = []

    for record in records:
        if record["status"] == "failed":
            failed.append(record["id"])
        else:
            processed.append(record["id"])

    return {
        "processed_count": len(processed),
        "failed_count": len(processed),
        "failed_ids": failed
    }


records = [
    {"id": 101, "status": "success"},
    {"id": 102, "status": "failed"},
    {"id": 103, "status": "success"},
    {"id": 104, "status": "failed"}
]

print(process_records(records))
```

### Question 1

Walk me through what this code does.

### Question 2

There is a bug in the code.

Can you find it and explain what the correct behavior should be?

---

## Interviewer Notes

The bug is:

```python
"failed_count": len(processed)
```

It should be:

```python
"failed_count": len(failed)
```

For the supplied input, the expected result is:

```python
{
    "processed_count": 2,
    "failed_count": 2,
    "failed_ids": [102, 104]
}
```

### What to Look For

This is not intended to test obscure Python syntax.

Look for whether the candidate can:

- Read basic Python.
- Understand lists, dictionaries, loops, and conditionals.
- Trace data through the function.
- Explain what the code is doing.
- Identify the incorrect count.
- Explain how they would validate the fix.

### Optional Production Follow-up

Support reports that production is returning incorrect failure counts.

You do not know whether the problem is this function, the input records, or something upstream.

How would you investigate?

Strong answers may include:

- Obtain concrete examples.
- Compare expected vs. actual results.
- Inspect the actual input.
- Reproduce the behavior.
- Check logs.
- Trace records through upstream/downstream systems.
- Determine whether the problem is code, data, or configuration.
- Document findings before escalating.

---

# Challenge 2: SQL Data Investigation

## Candidate Prompt

You have two relational database tables.

### `customers`

| customer_id | name | active |
|---|---|---|
| 1 | Acme | 1 |
| 2 | Globex | 1 |
| 3 | Initech | 1 |
| 4 | Umbrella | 0 |
| 5 | Soylent | 1 |

### `transactions`

| transaction_id | customer_id | status | created_at |
|---|---|---|---|
| 1001 | 1 | SUCCESS | 2026-10-01 |
| 1002 | 1 | FAILED | 2026-10-02 |
| 1003 | 1 | FAILED | 2026-10-03 |
| 1004 | 2 | SUCCESS | 2026-10-01 |
| 1005 | 3 | FAILED | 2026-10-02 |
| 1006 | 3 | FAILED | 2026-10-03 |
| 1007 | 3 | FAILED | 2026-10-04 |

---

## Question 1: Join and Filter

Write a query that returns the **customer name and transaction status** for all **active customers that have transactions**.

### Interviewer Reference Answer

```sql
SELECT
    c.name,
    t.status
FROM customers c
INNER JOIN transactions t
    ON c.customer_id = t.customer_id
WHERE c.active = 1;
```

Equivalent valid SQL is fine.

### What to Look For

The candidate should be able to:

- Identify how the two tables relate.
- Join on `customer_id`.
- Understand that an `INNER JOIN` returns customers with matching transactions.
- Apply a simple filter using `WHERE`.

---

## Question 2: Aggregate Failures

Write a query that returns **all active customers**, including customers who have no transactions.

Return:

- Customer name
- Number of failed transactions

### Expected Result

| name | failed_count |
|---|---:|
| Acme | 2 |
| Globex | 0 |
| Initech | 3 |
| Soylent | 0 |

### Interviewer Reference Answer

```sql
SELECT
    c.name,
    SUM(CASE WHEN t.status = 'FAILED' THEN 1 ELSE 0 END) AS failed_count
FROM customers c
LEFT JOIN transactions t
    ON c.customer_id = t.customer_id
WHERE c.active = 1
GROUP BY c.name;
```

Equivalent valid approaches are fine.

### What to Look For

This question adds a little more complexity. The candidate should demonstrate an understanding of:

- `LEFT JOIN`.
- Preserving customers that have no matching transactions.
- `GROUP BY`.
- Aggregating related records.
- Conditional counting or an equivalent approach.
- How `NULL` or missing related records affect the result.

Minor syntax mistakes are not necessarily a concern if the candidate clearly understands the concepts and can reason through the query.

---

## Follow-up: Repeated Failures

Support reports that some active customers have had repeated transaction failures.

Modify the query to show only customers with **more than two failed transactions**.

### Interviewer Reference Answer

```sql
SELECT
    c.name,
    SUM(CASE WHEN t.status = 'FAILED' THEN 1 ELSE 0 END) AS failed_count
FROM customers c
LEFT JOIN transactions t
    ON c.customer_id = t.customer_id
WHERE c.active = 1
GROUP BY c.name
HAVING SUM(CASE WHEN t.status = 'FAILED' THEN 1 ELSE 0 END) > 2;
```

### Expected Result

| name | failed_count |
|---|---:|
| Initech | 3 |

### What to Look For

The follow-up is intended to see whether the candidate understands the difference between:

- Filtering individual rows with `WHERE`.
- Grouping records using `GROUP BY`.
- Filtering aggregated results using `HAVING`.

Knowing the exact `HAVING` syntax should not necessarily be treated as a hard pass/fail requirement. If the candidate understands what needs to happen but needs minor syntax help, that can still demonstrate sufficient SQL fundamentals for the role.

---

# Scoring Guidance

These challenges are intended as lightweight technical signals.

## Strong Signal

The candidate:

- Reads the Python without significant difficulty.
- Can explain the flow rather than only identify syntax.
- Finds the bug through reasoning or execution.
- Understands how the two SQL tables relate.
- Can construct the join and filtering query with minimal assistance.
- Understands how to preserve customers with no transactions.
- Can reason about grouping and counting failures.
- Understands the conceptual difference between `WHERE` and `HAVING`.

## Acceptable / Coachable

The candidate:

- Understands the concepts but needs minor syntax help.
- Has to think through Python syntax but can correctly reason about the code.
- Understands joins and aggregation but makes a small SQL syntax mistake.
- Understands what `HAVING` needs to accomplish even if they do not remember the exact syntax.
- Demonstrates enough technical foundation that the gaps appear teachable.

## Concern

The candidate:

- Cannot explain the basic Python control flow.
- Cannot reason about what the function returns.
- Cannot identify how the two database tables relate.
- Does not understand the conceptual difference between inner and outer joins.
- Cannot reason about grouping records or counting related records.
- Immediately gives up rather than attempting to reason through unfamiliar syntax.

The broader hiring question should remain:

> **Does this person have enough technical foundation and problem-solving ability that we can work with them on the things they do not already know?**
