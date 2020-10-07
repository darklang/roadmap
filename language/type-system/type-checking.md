# Type checking

### Dark v1 problems

A big issue is that Dark v1 didn't support type checking directly. Instead, the execution engine sometimes produced error which highlighted and propagated type errors.

Because there was no type checking, programs were often broken, but this was hard to see if it was not triggered by a particular trace.



This particularly affected the automatic JSON parsing from HTTP requests and the result of HTTPClient calls, which essentially used dynamic typing. 

