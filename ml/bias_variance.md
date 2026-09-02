# Bias-Variance Tradeoff

- **High Bias** = model is too simple → underfitting (misses patterns)
- **High Variance** = model is too complex → overfitting (memorizes noise)
- **Goal** = find the sweet spot in between

```
Simple model ←————————————→ Complex model
(High bias,                   (Low bias,
 Low variance)                 High variance)
 e.g., Linear Regression       e.g., Deep Neural Net
```

### How to fix:
| Problem | Signs | Fix |
| :--- | :--- | :--- |
| **Underfitting** | Train accuracy low, test accuracy low | Use a more complex model, add features |
| **Overfitting** | Train accuracy high, test accuracy low | Add regularization, get more data, simplify model |
