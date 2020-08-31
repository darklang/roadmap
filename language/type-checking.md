# Type checking

### Dark v1 problems

A big issue is that Dark v1 didn't support type checking directly. Instead, the execution engine highlighted and propagated type errors in many cases.

This particularly affected the automatic JSON parsing from HTTP requests and the result of HTTPClient calls, which essentially used dynamic typing. 

