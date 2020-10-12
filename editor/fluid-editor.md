# Fluid editor

### Dark v1 problems

### Different editing schemes

**Problem:** Dark has two different ways of editing text. The "blankOr" method where something is blank or has a value, and the fluid method of editing code. The fact that there are two is confusing, as they have different interaction models \(they also intersect badly\).

**Solution:** The Fluid method is far superior, so make it so we can edit databases, handlers, functions, using Fluid editing

* note that some places have the ability to do cool shit now \(eg, dragging function parameters to a different order\); we should super-impose nice editing tooling like this on fluid tokens

### Unclear how to change text

**Problem:** while it's relatively nice to create text, changing existing code is a bit of an ordeal.

**Solution:** We need to identify a \(large\) list of specific areas where changing code is annoying, and find ways to make them nice, whether using refactoring tools, overlays, keyboard shortcuts, copy/paste, or just typing

List of known problems:

* TODO

### Text Wrapping

**Problem**: We wrap text in a number of places \(strings at 40 characters\), function calls at 120 characters. We need to wrap more things.

**Solution:** Write down how wrapping should work for various constructs.

### Precedence

**Problem**: It's difficult for users to set \(or to see\) the precedence of code in Dark. For example: `i % 15 == 0` , if typed out left-to-right in the way you'd expect, is actually `i % (15 == 0).` 

**Solution \(seeing precedence\):** the code is actually in the repo for displaying parens around expressions when they need them. It just needs:

* to be enabled
* to be trimmed so that we only show them at useful times \(eg `1 + 1` doesn't need it, but `i % 15 == 0` does\)

The major issue that made this challenging is that when you add an expression which needs parens, it adds a parenthesis behind you, which moves your cursor. When we had a caret which uses an integer offset as position, this would keep it in the same place and that would be really annoying. We switched to `AstRefs` instead \(the caret is now determined relative to a particular AST element\), but we probably still have some bugs that will come from this.

**Solution \(automatically setting precedence\):** when typing infix, there is a known set of precedence rules that humans expect \(most languages define them in the parser\). As a result, we should use them to automatically set precedence as users type.

**Solution \(allowing users change precedence\):** once you've got a particular precedence, how do you change it? We don't allow you to type parens randomly, or to delete them. Instead, we should add refactoring commands to shift what's covered in the parens. Paredit \(one of the inspirations for Dark's editor\) does this really well.

### Undo is slow

**Problem:**  when undoing something in Dark, it can take a long time and you can't see that.

**Solution:** make it faster. Dark opcodes are often huge and pulling them all from the DB, then writing them back, does indeed take time.

* We can shrink the opcodes significantly \(most opcode in the DB are SetHandlers, which contain the entire handler. Switching to much smaller opcodes such as `SetExpr` and `InsertIntoStringAt` would result in much much smaller ops.
* We can also send fewer opcodes when a user is typing \(eg a long string\) by debouncing.  
* We can cache previous states in the client or server
* We can make the opcodes so that we can go both ways

**Solution:** make it clear that something is happening. There should be an indicator to let you know that Dark is actually undoing your code for you.

### Undo is broken for function/DB renames

**Problem**: if you rename a function, it will rename all users of that function. If you then undo a handler with a use in it, it will go back to the old name \(which breaks it\). If you undo a function name change, none of the uses are updated.

**Solution:** we could store the TLIDs of functions being called and the DBs being referenced, instead of their names. Then renames wouldn't be needed, and wouldn't be part of the undo stack

