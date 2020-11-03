# Error Tracking

Every error TRACE should be stored in a special place, so that users can find them easily.

Categories:

* DError or DIncomplete - should not have happened
* DErrorRail - an error path reaches the user with Error/Nothing
* Non 200 results
* unit tests which aren't passing
* allow users assert that things can't happen
* uses of deprecated functions
* can users add bugs, TODOs, etc, in here.
* Can users add things in here dynamically?



Allow users to find them by:

* handler
* function

