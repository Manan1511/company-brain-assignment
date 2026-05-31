# Component
Event Queue / Message Queue

# Proposed Technology
Apache Kafka

# What does this component do?
It acts as hub of all engg activity data of the project. It reliably receives incoming events from external sources, such as commits from github, discussions on slack or other notifications of development, and hold them in a durable organised log. Different services in our architecture , can subscribe to these events and process them when they are ready without crashing during high loads.

# Why did you choose this technology?
- Kafka functions as an immutable log, it stores events on disk allowing us to replay the past data whenever we want, it is useful in a situation, imagine when we need to reconstruct our enitre infra for a specific reason at a point of time.
- As Kafka serves as long term , durable memory log, it keeps data indefinitely based on our config. Upon browsing a few alternatives, such as Amazon SQS, RabbitMQ, they act as a transient message handlers, they delete messages as soon as they are consumed, it makes them unsuitable for our project. Amazon SQS is built for small tasks, it fire and forget task queue, on the other hand, RabbitMQ acts as a broker, it won't store data.
- Kafka is built for high volume event streaming, it handles millions of events /s , by partitioning data across clusters.


# Advantages
- Guaranteed ordering of events. - the order of events is non-negotiable. If an "Incident Reported on ACM-VIT assets" event arrives before the "Deployment" event that caused it, then our analysis will be wrong. Kafka guarantees that events within a specific partition are stored and delivered in the exact sequence they occurred before, ensuring the timeline logic stays accurate. 
- Highly fault-tolerant. - It replicates data across multiple servers, called brokers. If one server in the cluster crashes or experiences a hardware failure, the data is still safe and accessible from the other servers. This ensures that our project never suffers from data loss, even during infra outages too.

# Limitations
- Complex to set up compared to simple queues. - Kafka is more complex to configure and maintain than simple queues like amazon's sqs. It requires managing coordination of a cluster, partitioning logics, and retention policy. This means it requires more time to set up and monitor.
- Requires managing a cluster. - Kafka requires to manage a cluster of machines. We need to monitor disk usage, network throughput, and cpu load across the cluster to ensure it stays healthy.

# Would you use it in Company Brain?
Yes. Implementing Kafka is the best choice. The goal relies on preserving the complete history of an org rather than just clearing temporary tasks. By utilizing kafka’s log-based architecture, we ensure that our events are true.
