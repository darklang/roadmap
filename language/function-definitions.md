# Functions

## Functions Definitions

In Dark v1:

* function definitions were in the "function space", which confused people.
* you couldn't add docstrings
* parameters and docstrings used a non-fluid way to enter them
  * you could use the mouse to drag them \(good feature\)
* there wasn't a good way of doing continuous delivery on functions
  * How do I make a new version of a function safely?
    * Allow "make new version" operation/refactoring
    * Lock functions that are used by locked handlers

Solutions:

* "function space" addressed elsewhere
* Function definitions should be fluid \(use the fluid editor style\)
* parameters should have types
* parameters should have docs

TODO:

```text
package manager from the start
can we implement built-in Dark functions via the package manager
what is the story with namespacing
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

