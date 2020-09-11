# Function definitions

## Dark v1 Problems and solutions:

### Function space

**Problem:** function definitions were in the "function space", which confused people.

**Solution:** the function space is not important, but keeping functions off of the main canvas is a key part of the [Infrastructure view](../../../editor/canvas.md) metaphor. I think we need to make it clearer whats happening here, possibly by making better animations as we transition from handler to caller.

I welcome other suggestions for how to improve this.

### Parameters are not fluid

**Problem:** Parameters use a non-fluid way to enter them. We want everything to be fluid.

**Solution:** Make function definitions fluid, including parameters and docstrings.

One thing that's nice about function parameters is that they're draggable - I think we could augment many fluid things by making them draggable \(eg `let` definitions, record entries, etc\).

### Docstrings in user functions

**Problem:** Dark v1 doesn't have docstrings. We had a \[PR for it\]\([https://github.com/darklang/dark/pull/2571](https://github.com/darklang/dark/pull/2571)\) but it had weird behaviour due to `blankOrs`.

**Solution:** docstrings should be part of the structured editor definition of a function, using a fluid mechanism.

### Docstrings aren't used properly in stdlib

**Problem:** Though we support docstrings

**Solution:** Go through the stdlib and use docstrings properly, according to the [guide](https://github.com/darklang/dark/blob/main/docs/writing-docstrings.md). 

**Problem**: we support docstrings for individual parameters \(as well as the parameters of lambda functions\) but we don't use them

**Solution:** go through the stdlib and add docstrings for individual parameters. Show those docstrings in the UI when your cursor in on a parameter.

### User Functions don't have continuous delivery built-in

**Problem:** there isn't a way to safely make a new version of an existing function that's used by other functions or handlers.

There is, _conceptually at least_, a good solution for continuous delivery of a handler:

* lock the handler when used
* only allow changes via feature flags

For functions, versioning is a better strategy, as it allows handlers to use feature flags to change which version they call.

**Solution:** We need to write down the exact UX of how this works, start to finish. How do the flags get set, when do functions lock and version, and what happens when we have a new version of a function that's down the callgraph?

### Methods

**Problem:** most people coming to dark are used to calling methods on "objects" and get confused when they type `"hello world".toUppercase` and discover not only that there's no function called `"uppercase"`, but also that they're not offered any functions. This is because Dark uses pipes, and doesn't do function dispatch.

**Non-Solution**: one solution would be like what Rust does solution: offer both functions and methods. If the function is implemented on that type, then it's available as a method, but you can also have methods. However, this is a little frustrating, as you can \(afaik\) only chain methods, you can't add a function call to that chain. Dark uses piping for chaining calls together nicely, so we should use that.

**Solution:** when a developer types '`.`' after an object, offer not just the fields of the struct in the autocomplete, but also the functions that the user would expect to find as methods. These would include at least anything that has the type as the first parameter.

### TODO:

```text
package manager from the start
can we implement built-in Dark functions via the package manager
what is the story with namespacing (types vs modules)
How should tests work? Should they be for a specific
TODO: partial application/currying
TODO: optional parameters
```

### Versioning:

* functions should be versioned, but we haven't got a good system
* idea: functions called by locked handlers are locked
* the challenge is that when you change a function, you change the entire call tree
* can you add a feature flag to a function?
* make it easy to clone another version

### Package manager

We want a package manager, so stdlibs need to fit into this. The namespace of stdlib is `dark/stdlib/`. Because functions  



#### Example

```text
def range_v0:
  start : Int => The lower end of the range
  end   : Int => The upper end of the range. This is not 
                 included in the output.
   
```

## Function calls



## BinOp calls

