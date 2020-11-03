# Traces / analysis / tests

* Dark feels unsafe to users. We need to add ways 
* record and places where the 
* size of traces is out of control
* when moving around the editor, we don't stay in the same trace

### Storage of traces

**Problem:** the storage of traces is poor. Each trace is currently stored and then GCed - the performance of the GC is poor, despite multiple incremental fixes, and causes operational issues.

**Solution:** The trace feature should be redesigned with performance taken into account. The access patterns are:

* traces are created on each request. They are created in several parts and written to the DB each time. The inputs are written on input \(they are stored with the path, module, and modifier instead of a tlid, to allow searching for 404s. It also means that 404s are created dynamically. The intent was for 404s to be automatically repopulated when changing the name of a canvas: this feature is alsp confusing to users\)
* traces are updated via:

So

* store 404s individually
* new handler and function executions get new traces
* store traces so that they can be accessed by

