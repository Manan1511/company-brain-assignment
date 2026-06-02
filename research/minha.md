# Component

Async Workers

# Proposed Technology

Taskiq and RabbitMQ 

# What does this component do?

Asynchronous workers allow  to run tasks simultaneously by using multiple threads. Workers cannot directly access the variables of the main code, in order to prevent data synchronization issues. This means that they cannot directly access the **DOM** neither all the **API's** that the main application can. 

The different types of workers are:
- Dedicated Workers- They share a single script instance.
- Shared Workers- They can use different scripts running in different windows.
- Service Workers- They cache resources so that web apps can work even when the user is offline. 

# Why did you choose this technology?

- RabbitMQ is the best at reducing latency since it uses the highly efficient AMQP ( Advanced Message Queuing Protocol )
- Taskiq can be implemented easily with **Fast API** to simultaneously handle tasks in a single event loop. 
- Another alternative is Celery and Redis but they are process based blocks, meaning whenever a LLM API is called or a query on the graph database, that process sits completely idle, waiting for a network response.  

# Advantages

- Advanced Message Routing is supported as RabbitMQ allows to simultaneously broadcast to the vector and graph queue without duplicate tasks.
- True Dependency Injection as Taskiq is similar to Fast API's dependency injection system. 
- Modern and currently booming technology

# Limitations

- Smaller Community as Taskiq is much newer.
- Handles CPU bound tasks poorly. 

# Would you use it in Company Brain?

Yes, Taskiq and RabbitMQ can be used in Company Brain as the engine running the data ingestion and processing pipelines. When external data from Github or Slack enters the system, the backend pushes it directly to RabbitMQ which acts as a broker and routes into respective queues.

Taskiq coordinates the execution of background worker processes that pull these tasks from RabbitMQ. Since Taskiq is built natively on pythons asynchronous event loop, a single worker process can handle thousands of concurrent tasks simultaneously.

Even though the system handles CPU bound tasks poorly, this project comprises mostly of I/O based tasks, making the Taskiq and RabbitMQ setup optimal. 

# References

- https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Async_JS/Introducing_workers
- https://taskiq-python.github.io/guide/architecture-overview.html#context
- https://www.cloudamqp.com/blog/part1-rabbitmq-for-beginners-what-is-rabbitmq.html

