# Dark v1 problems

The roadmap is mostly organized around Dark features, for example, the Strings page discusses v1 problems, solutions, detailed implementation, etc, all in one page/section.

Any things that can't be classified well there will go here.



### Safety

Dark feels unsafe to users. They feel reluctant to make changes because they don't know if they will work, or if they'll break things. We need ways to make this safer:

* unit tests on functions and handlers will make users feel safe
* type checking:
  * by having type checking on functions and handlers, users can feel confident that their code will work
* error tracking
  * highlight \(and email users about\) errors in their apps
  * highlight data being sent that isn't being used by the app \(eg form fields\)
    * is this the same as warn/error log messages?
* application understanding
  * email users about their traffic so that they understand that their code works
  * allow people search their traces for 
* feature flags:
  * make feature flags global and easier to use and understand
* fix size of traces
* fix editor layout
  * the layout of the canvas
* education so that users can understand

