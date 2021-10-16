# Error Tracking

Developers need to feel safe that Dark works. Right now, it is impossible (or at least extremely challenging) to know if your users are having issues, if all webhooks are being accepted, etc. Requests may hit Dark but hit an error of many kinds, and that error will create a trace that is hard to find.

Categories of error:

* runtime errors
  * coding error:
    * an incomplete value appears
  * unexpected function error
    * a DError (Dark built-in error)
  * unhandled exception
    * DErrorRail - an error path reaches the user with Error/Nothing
  * an expected unexpected value
    * Non-200 results
  * dev-defined assertion
* "compile time"
  * unit tests not passing
  * uses of deprecated functions
* other
  * can users add bugs, TODOs, etc, in here.
  * Can users add things in here dynamically?

### Problem: developers should be able to discover the error

**Solution:** Error traces should be put in a dead-letter queue, which have urls

**Solution:** Developers should be notified about errors. One implementation is that there would be a default error handler for the whole canvas, which would email the developer for each error (potentially every nth error). As an extension, this handler could be customized (if there is an error in the customization, the default handler would run again).

**Solution:** the canvas should have a list of TODO items, which should include errors in the error tracker

### Problem: developers should be able to solve the error

**Solution:** When an error is found, the notification should link to the trace. The trace should be replayable (either fully or partially) using existing trace features, which would allow the developer to ensure the intended action still happens for their user. The dev should then able to  to resolve it.

**Solution:** If there are a lot of errors, the user should be able to handle them all. For example, all of them could be pushed into a standard queue to be processed. If this is done, a button to run just one queue entry would be extremely valuable.
