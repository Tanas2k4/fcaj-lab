---
title: "Blog 3"
date: 2024-07-04
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Comparing design approaches for building serverless microservices

Designing a workload with AWS Lambda creates questions for developers due to the modularity that can be expressed either at the code or infrastructure level. Using serverless for running code requires additional planning to extract the business logic from the underlying functional components. This deliberate separation of concerns ensures a robust modularity, paving the way for evolutionary architectures.

This post focuses on synchronous workloads, but similar considerations are applicable in other workload types. After identifying the bounded context of your API and agreeing on API contracts with consumers, it’s time to structure the architecture of your bounded context and the associated infrastructure.

The two most common ways to structure an API using Lambda functions are single responsibility and Lambda-lith. However, this blog post explores an alternative to these approaches, which can provide the best of both.

---

## Single responsibility Lambda functions

Single responsibility Lambda functions are designed to run a specific task or handle a particular event-triggered operation within a serverless architecture.

This approach provides a strong separation of concerns between business logic and capabilities. You can test in isolation specific capabilities, deploy a Lambda function independently, reduce the surface to introduce bugs, and enable easier debugging for issues in Amazon CloudWatch.

Additionally, single purpose functions enable efficient resource allocation as Lambda automatically scales based on demand, optimizing resource consumption, and minimizing costs. This means you can modify the memory size, architecture, and any other configuration available per function. Moreover, requesting an update of concurrent function execution via a support ticket becomes easier because you are not aggregating the traffic to a single Lambda function that handles every request but you can request specific increase based on the traffic of a single task.

Another advantage is rapid execution time. Considering the business logic for a single-purpose Lambda function designed for a single task, you can optimize the size of a function more easily, without the need of additional libraries required in other approaches. This helps reduce the cold start time due to a smaller bundle size.

Despite these benefits, some issues exist when solely relying on single-purpose Lambda functions. While the cold start time is mitigated, you might experience a higher number of cold starts, particularly for functions with sporadic or infrequent invocations. For example, a function that deletes users in an Amazon DynamoDB table likely won’t be triggered as often as one that reads user data. Also, relying heavily on single-purpose Lambda functions can lead to increased system complexity, especially as the number of functions grows.

A good separation of concerns helps maintain your code base, at the cost of a lack of cohesion. In functions with similar tasks, such as write operations of an API (POST, PUT, DELETE), you might duplicate code and behaviors across multiple functions. Moreover, updating common libraries shared via Lambda Layers, or other dependency management systems, requires multiple changes across every function instead of an atomic change on a single file. This is also true for any other change across multiple functions, for instance, updating the runtime version.

---

## Lambda-lith: Using one single Lambda function

When many workloads use single purpose Lambda functions, developers end up with a proliferation of Lambda functions across an AWS account. One of the main challenges developers face is updating common dependencies or function configurations. Unless there is a clear governance strategy implemented for addressing this problem (such as using Dependabot for enforcing the update of dependencies, or parameterized parameters that are retrieved at provisioning time), developers may opt for a different strategy.

As a result, many development teams move in the opposite direction, aggregating all code related to an API inside the same Lambda function.

This approach is often referred to as a Lambda-lith, because it gathers all the HTTP verbs that compose an API and sometimes multiple APIs in the same function.

This allows you to have a higher code cohesion and colocation across the different parts of the application. Modularity in this case is expressed at the code level, where patterns like single responsibility, dependency injection, and façade are applied to structure your code. The discipline and code best practices applied by the development teams is crucial for maintaining large code bases.

However, considering the reduced number of Lambda functions, updating a configuration or implementing a new standard across multiple APIs can be achieved more easily compared with the single responsibility approach.

Moreover, since every request invokes the same Lambda function for every HTTP verb, it’s more likely that little-used parts of your code have a better response time because an execution environment is more likely to be available to fulfill the request.

Another factor to consider is the function size. This increases when collocating verbs in the same function with all the dependencies and business logic of an API. This may affect the cold start of your Lambda functions with spiky workloads. Customers should evaluate the benefits of this approach, especially when applications have restrictive SLAs, which would be impacted by cold starts. Developers can mitigate this problem by paying attention to the dependencies used and implementing techniques like tree-shaking, minification, and dead code elimination, where the programming language allows.

This coarse grain approach won’t allow you to tune your function configurations individually. But you must find a configuration that matches all the code capabilities with a possibly higher memory size and looser security permissions that might clash with the requirements defined by the security team.

---

## Read and write functions

These two approaches both have trade-offs, but there is a third option that can combine their benefits.

Often, API traffic leans towards more reads or writes and that forces developers to optimize code and configurations more on one side over the other.

For example, consider building a user API that allows consumers to create, update, and delete a user but also to find a user or a list of users. In this scenario, you can change one user at a time with no bulk operations available, but you can get one or more users per API request. Dividing the design of the API into read and write operations results in this architecture:

### Separating read and write operations in serverless APIs

![Separating read and write operations in serverless APIs](/images/blogs/blog3-Picture1.png)
*Figure 1: Separating read and write operations in serverless APIs*

The cohesion of code for write operations (create, update, and delete) is beneficial for many reasons. For instance, you may need to validate the request body, ensuring it contains all the mandatory parameters. If the workload is heavy on writes, the less-used operations (for instance, Delete) benefit from warm execution environments. The code colocation enables reusability of code on similar actions, reducing the cognitive load to structure your projects with shared libraries or Lambda layers, for instance.

When looking at the read operations side, you can reduce the code bundled with this function, having a faster cold start, and heavily optimize the performance compared to a write operation. You can also store partial or full query results in-memory of an execution environment to improve the execution time of a Lambda function.

This approach helps you further with its evolutionary nature. Imagine if this platform becomes much more popular. Now, you must optimize the API even further by improving reads and adding a cache aside pattern with ElastiCache and Redis. Moreover, you have decided to optimize the read queries with a second database that is optimized for the read capability when the cache is missed.

On the write side, you have agreed with the API consumers that receiving and acknowledging user creation or deletion is adequate, considering they fully embraced the eventual consistency nature of distributed systems.

Now, you can improve the response time of write operations by adding an SQS queue before the Lambda function. You can update the write database in batches to reduce the number of invocations needed for handling write operations, instead of dealing with every request individually.

### Evolved CQRS pattern with SQS, Lambda, and Replica Databases

![Evolved CQRS pattern with SQS, Lambda, and Replica Databases](/images/blogs/blog3-Picture2.png)
*Figure 2: Evolved CQRS pattern with SQS, Lambda, and Replica Databases*

Command query responsibility segregation (CQRS) is a well-established pattern that separates the data mutation, or the command part of a system, from the query part. You can use the CQRS pattern to separate updates and queries if they have different requirements for throughput, latency, or consistency.

While it’s not mandatory to start with a full CQRS pattern, you can evolve from the infrastructure highlighted more easily in the initial read and write implementation, without massive refactoring of your API.

---

## Conclusion

All three approaches are viable for designing serverless APIs, and understanding what you are optimizing for is the key for making the best decision. Remember, understanding your context and business requirements to express in your applications leads you towards the acceptable trade-offs to specify inside a specific workload. Keep an open mind and find the solution that solves the problem and balances security, developer experience, cost, and maintainability.

**Source:** [AWS Compute Blog](https://aws.amazon.com/blogs/compute/comparing-design-approaches-for-building-serverless-microservices/)

**Post on AWS Study group:** [AWS Compute Blog](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2203819477049679/?rdid=3sEML8B3PXziCwcs#)