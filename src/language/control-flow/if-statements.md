# If

An if statement in Dark is a conditional, 

## Dark v1



```
type Expr = 
  | If { cond : Expr, thenbody : Expr, elsebody : Expr }
  | ...
  
// No pattern, dval, or dtype
```

### Problem

In Dark v1, the interpreter allows an non-false, non-fake value to return true.

#### Solution





## Dark v2
