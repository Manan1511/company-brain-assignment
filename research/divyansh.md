
# Component

Event queue / Message broker

# Proposed Technology

Apache Kafka

# What does this component do?

A message broker/event queue decouples producers (webhook rec in our case) from consumers (async workers). It enables reliable message delivery and asynchronous communication. It also handles buffering during traffic spikes, load balancing, event driven architectures  
# Why did you choose this technology?

- Kafka is designed to be have high throughput and handle growing systems well.
- Reliable message logs.
- Alternatives like Pulsar and NATS Jetstream can be considered as they have incorporated many of Kafka's unique features but Kafka still has a more mature ecosystem.

# Advantages

- Strong support for exactly-once semantics, partitioning, replication, and consumer groups for parallel processing.
- Extremely high throughput and low latency at scale.

# Limitations

- Higher operational complexity compared to simpler brokers.
- Not ideal for complex routing patterns.

# Would you use it in Company Brain?

I would use this in Company Brain because it is very mature and very widely supported. I am still understanding how message broker systems work and the design philosophies and performance implications of different systems. This is my first time working on a web development project of this scale so I am not sure about the scale, performance, routing, integration and maintenance requirements. Hybrid alternatives like Kafka + NATS Jetstream can be considered where Kafka handles durable, high-volume events & pipelines and NATS handles low-latency real-time communication but I feel like NATS's ultra low latency is not something we require.
There are multiple single broker alternatives to Kafka that claim to offer better performance but I would like to go with a system that is thoroughly tested and reliable.

# References

https://hasithas.medium.com/introduction-to-message-brokers-c4177d2a9fe3 - brief introduction to message brokers.

https://youtu.be/C4BnJ5QLeTY?si=exzJkw0GQ-_Ktr8q = NATS vs Kafka compared (offers insight into design philosophies)

https://quix.io/blog/kafka-vs-pulsar-comparison

https://docs.nats.io/ - Official NATS documentation

https://kafka.apache.org/43/getting-started/introduction/ - Official Kafka documentation

https://medium.com/@sylvain.tiset/beyond-the-queue-the-rise-of-rabbitmq-kafka-and-modern-messaging-ecdc124efd9e - Explains briefly how Kafka and RabbitMQ work and a comparison.