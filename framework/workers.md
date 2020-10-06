# Workers

### Dark v1 problems

* Queues should be processed with QoS. If someone puts 100k items in the queue, the user with just 1 should still go immediately.
* V1 doesn't have the ability to fanout, or do any patterns except emit
* We dont have a good understanding of the currently implemented retry logic, or what the retry logic should be
* users dont have a good way to get warnings if their queues are failing
* no way to introspect queues using code, barely any way to introspect them without code
* sometimes queues take too long or fail, and items build up. should they be rerun? Should there be an expiry time?



