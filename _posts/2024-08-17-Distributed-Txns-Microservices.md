---
title: "Distributed transactions in microservices"
date: 2024-08-17
---

A common challenge for distributed systems like microservices is to ensure data consistency across multiple microservices (their databases).

[There are two main approaches to solve this challenge.](https://www.baeldung.com/cs/two-phase-commit-vs-saga-pattern#:~:text=3.,context%20of%20a%20distributed%20transaction.)

- Two phase commit (2PC)
- Saga pattern

## 2PC
One microservice acts as a coordinator or transaction (txn) manager to initiate a 2PC transaction.
- Preparation phase
    - Request sent to dependency services to check if txn can be committed or not.
    - Each service must ensure the durability of their decision by e.g. using a write ahead log pattern.
- Commit phase
    - Executes based on response from dependency services from the preparation phase above.
    - Either a commit or abort request is sent to dependency services.
    - Each dependency service performs required action and releasees any locks acquired in the process.
    - Each dependency serivce responds back with success or failure to the coordinator service.

## Saga pattern
This pattern decomposes a txn into a series of smaller, independent sub-txns, also called local txns.
Each sub-txn is managed by a separate service & together they form a saga.

There are 3 different **types of txns** in Saga pattern
- Compensable - Txn that can be reversed by processing another txn with the opposite effect.
- Pivot - The go/no-go point in a saga. If the pivot txn commits, the saga runs until completion. A Pivot txn can be a txn that is neither compensable nor retryable. Also, it can be the last compensable or the first retryable txn in the saga.
- Retryable - Txn which can be retried multiple times.

There are two approaches for saga pattern
- Choreography
    > Each local txn publishes events that trigger local txns in other services. If any step fails, each service must execute a compensating txn to revert its changes.

    Decentralised approach, comms happen via service bus, different microservices can be easily upgraded separately [Ref](https://www.architect.io/blog/2022-06-30/microservices-orchestration-primer/).
- Orchestration
    > Central orchestrator manages the entire txn. The orchestrator sends commands to each service to perform their local txns. It also handles any failures by sending commands to execute compensating txns as necessary.

    Single point of failure - orchestrator. Can be useful for complex workflows. Can be difficult to update frequently [Ref](https://www.architect.io/blog/2022-06-30/microservices-orchestration-primer/).

## Differences

| Point of difference | 2PC | Saga pattern |
| - | - | - |
| Consistency                        | strong | eventual |
| Suitable for which lifespan of txn | short  | long     |
| Ease of implementation             | simple | complex  |
| Scalability                        | no     | yes      |

## Summary
Based on above input it becomes obvious that best way to handle is by using a combination of Orchestration and Choreography patterns. Top level transaction where it all begins need to use Orchestration pattern, dependency services need to use Choreography pattern as they can be calling further more dependency services.