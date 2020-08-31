# Fluid editor

### AstRefs first

TODO

### All definitions are use fluid

### Super-impose abilities

* dragging expressions or parameters or record fields or list entries, etc, to a different order can be done 

### Keyboard shortcuts for refactoring

### Text Wrapping

### Precedence

Operational transforms

Size of edits

Undo was broken

### History

* store who does changes, and when
* was the change due to a 



### Dark v1 issues

* Data is serialized using OCaml's bin\_prot, which is challenging
* Lack of debouncing for changes
* Ops are huge, making lots of things extremely slow

### Notes

* having different types for program storage, data storage, API generation, and runtime, makes migrating significantly easier. Migration for runtime is instant as they are not persisted; for APIs it's multi-step but not huge; for 

