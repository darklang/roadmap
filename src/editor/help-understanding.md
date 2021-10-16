# Help understanding

### Dark v1 problems

Users often have problems understanding what they're seeing, for a number of reasons:

* they are learning the language for the first time, and are unfamiliar with the constructs, frameworks, types, functions, etc
* the editor prints things in an ambiguous way

### Solution

We already partially solve this with traces, where we show actual values. However, we can show more information to help:

* show the type in the live value display
* show `(i)` info icon on framework elements, types. This will show a doc for this, perhaps with a link to more information
* an "AST view" where you can see the AST of this code, and when you mouse over particular code you see the AST you're selecting
