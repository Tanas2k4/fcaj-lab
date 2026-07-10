---
title: "Translated Blogs"
date: 2026-07-08
weight: 3
chapter: false
pre: " <b> 3. </b> "
---


This section lists and briefly introduces the technology blogs translated during the internship:

###  [Blog 1 - Scaling telco automation to millions of devices with Managed Red Hat AAP and ROSA on AWS](3.1-Blog1/)
This blog explores a highly elastic and scalable telco automation solution on AWS using Managed Red Hat AAP and ROSA. You will learn about the strict separation between the control plane and execution plane to manage millions of network edge gateways (home routers, modems) smoothly. It details real-time auto-scaling mechanisms to optimize AWS compute costs and the ingestion of logs into a distributed OLAP database to prepare for training operations AI/LLM models.

###  [Blog 2 - Introducing the AWS WAF traffic overview dashboard](3.2-Blog2/)
This blog introduces the out-of-the-box, default, and free traffic overview dashboard in AWS WAF. You will learn how network security operators can visualize metrics such as allowed/blocked requests, bot compared to non-bot traffic, device types, and top matched rules in near real-time. It covers practical use cases including tracking traffic spikes to tune security policies and utilizing Bot Control metrics to implement advanced token-based protections.

###  [Blog 3 - Comparing design approaches for building serverless microservices](3.3-Blog3/)
This blog compares the trade-offs of building serverless APIs with AWS Lambda using single-purpose functions vs. the monolithic Lambda-lith approach. It proposes a pragmatic middle ground: separating read and write operations into two dedicated functions per bounded context. This layout optimizes performance and cold starts, serving as an ideal precursor to evolving into a full CQRS (Command Query Responsibility Segregation) pattern with asynchronous SQS queue buffering and read replicas.
