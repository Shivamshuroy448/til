# List Comprehension vs Generator Expression

### List Comprehension — creates the full list in memory
```python
squares = [x**2 for x in range(1000000)]  # uses ~8MB of RAM
```

### Generator Expression — generates values one at a time (lazy)
```python
squares = (x**2 for x in range(1000000))  # uses almost no RAM
```

### When to use what:
- **List comprehension** → when you need to access items multiple times or need `len()`
- **Generator** → when you're iterating once (e.g., passing to `sum()`, `max()`, `for` loop)

```python
# Pro tip: pass a generator directly to sum() — no brackets needed
total = sum(x**2 for x in range(100))
```
