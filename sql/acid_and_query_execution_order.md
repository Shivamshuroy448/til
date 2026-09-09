# ACID Properties & SQL Query Execution Order

### 1. The ACID Principles (Transactional Integrity)
- **Atomicity:** All operations in a transaction succeed, or the entire transaction rolls back. No partial writes.
- **Consistency:** Data must satisfy all defined integrity constraints and schemas before and after the transaction.
- **Isolation:** Concurrent transactions execute without interfering with one another.
- **Durability:** Once committed, changes are permanently written to non-volatile storage and survive power outages or crashes.

---

### 2. SQL Logical Query Execution Order
SQL is written declaratively, but the engine evaluates clauses in this specific runtime order:

```
1. FROM / JOIN     --> Identify and join tables
2. WHERE           --> Filter individual rows before grouping
3. GROUP BY        --> Aggregate rows into buckets
4. HAVING          --> Filter grouped aggregates
5. SELECT          --> Compute expressions and column aliases
6. DISTINCT        --> Eliminate duplicate records
7. ORDER BY        --> Sort final results
8. LIMIT / OFFSET  --> Restrict row count
```

### Why It Matters (The Classic Alias Trap):
```sql
-- ❌ FAILS with "column new_salary does not exist"
SELECT salary * 1.1 AS new_salary
FROM employees
WHERE new_salary > 50000;
```
**Why:** `WHERE` runs at step 2, before `SELECT` creates the alias `new_salary` at step 5!

### When to use `WHERE` vs `HAVING`:
| Clause | Evaluated At | Operates On | Example |
| :--- | :--- | :--- | :--- |
| `WHERE` | Step 2 (Early) | Individual raw rows | `WHERE salary > 50000` |
| `HAVING` | Step 4 (Late) | Grouped aggregates | `HAVING COUNT(*) > 5` |
