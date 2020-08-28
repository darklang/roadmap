# Infrastructure

* Queues should be processed with QoS. If someone puts 100k items in the queue, the user with just 1 should still go immediately.
* when loading a handler, we also load every function, etc, not just the necessary ones. We should store the dependencies with the code \(this could be done in the client\).
* * 
