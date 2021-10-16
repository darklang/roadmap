# Higher-order functions

## Dark v1 problems

Dark's higher order functions could only take lambdas. For example:

```
List::map [1,2,3] (Int::add 1) // not possible

List::map [1,2,3] (\i -> Int:add i 1) // workaround
```

However, this was allowed in pipes:

```
[1,2,3]
|> Int::add 1
```

But this came with problems of it's own:

```
[1,2,3]
|> Int::sub 1 // [0,1,2] or [0,-1,-2]?
```
