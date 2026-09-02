# Window Functions

- `ROW_NUMBER()` — gives a unique sequential number to each row
- `RANK()` — skips numbers on ties (1, 2, 2, 4)
- `DENSE_RANK()` — does NOT skip on ties (1, 2, 2, 3)
- Always needs `OVER(PARTITION BY ... ORDER BY ...)`

```sql
-- Get the top earner in each department
SELECT name, department, salary,
  RANK() OVER (PARTITION BY department ORDER BY salary DESC) as salary_rank
FROM employees;
```

### When to use what:
| Function | Use When |
| :--- | :--- |
| `ROW_NUMBER()` | You need exactly 1 result per group (e.g., "latest order per customer") |
| `RANK()` | You want to find "top N" but allow ties to share the same rank |
| `DENSE_RANK()` | Same as RANK but you don't want gaps in ranking numbers |
