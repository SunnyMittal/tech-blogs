---
title: "Software Architecture"
date: 2024-07-07
---

## Below are set of steps and considerations to be taken into account in order to implement a well architected software application/solution.

Its like a painting which looks pretty from a distance no matter which colors (technology, tools etc...) have been used to create it.
Below are broad steps to be followed to architect/design a solution that is fit for its purpose. (**Note: Might not be perfect in all aspects, <u>it should be fit for its purpose</u>**)

- Start from problem statement
- Document regulatory requirements
- Define functional requirements
- Define non-functional requirements
- Take other constraints into account
- Prepare first cut of design
- Seek peer review and refine it
- Seek stakeholder review and refine it
- Present refined architecture to all stakeholders for their approval

### Problem statement
This can be formed after discussion with business stakeholders (management, staff, customers). Selection of right pool of people depends on the problem statement itself. Most likely Management and Staff will be part of most business usecases. Customers must be considered when its customer facing application under design. Even for non customer facing applications confirm about the journey points where customer might interact with the application directly or indirectly.

### Document regulatory requirements
This is to take any regulatory standards or requirements into consideration while architecting/designing a solution.
e.g.

> GDPR (General Data Privacy Regulation)

> PCI-DSS (Payment Cards Industry - Data Security Standard)

> HIPPA (Health Insurance )

### Define functional requirements
These are based on business requirements.

### Define non-functional requirements
These help to make a solution secure, scalable, resilient and maintainable. e.g. use authentication, authorization flows and validation to keep it secure. Use scalable tech stack like Azure functions, AKS, Kafka based cloud solutions for scalability. Follow best practices to create a performant solution. Use polly policies to make call between components fault tolerant and resilient. Implement modular components (broken down by business domain), logging, monitoring and alerts to make troubleshooting issues easier and increase solution maintainability.

    Ingredients for building secure solutions

    - Implement authentication and authorisation - https://medium.com/@iamprovidence/oauth-2-0-and-openid-in-simple-terms-7196089a1b29
    - Use parameter validation - https://medium.com/@madu.sharadika/validation-in-net-8-a250c4d278d2

    Ingredients for building performant solutions

    - Efficient data access
    - Leverage async programming where feasible
    - Use caching when feasible
    - Idempotent APIs
    - Secure APIs using OAuth2, OIDC, stateless JWT tokens to enable security without affecting scalability.
    - Performance monitoring, alerts
    - Keep scalability in mind, use load balancers to distribute traffic to multiple instances of application.
    - Consider rate limiting or throttling

    References
    https://medium.com/@paulotorres/advanced-techniques-in-net-core-for-building-high-performance-apis-7e9a6e978106

### Take other constraints into account ([Ref](https://medium.com/@srinathperera/how-to-approach-software-architecture-a-first-principle-perspective-3b865d35bb9b))

Each instance of the system will have different scale requirements, timelines, and team skill levels. Hence, they will have different architectural considerations. Therefore, the following three factors (context) affect the right architecture, thus creating uncertainty.

- Time to market
- The skill level of the team
- What is the performance sensitivity of the system / how much load must it face?

The first two follow the project management triangle or triple constraints ( time, quality, cost), where cost is often a proxy for the team’s skill level.

**We need to think deeply about things that are hard to change but use an agile method with user feedback while considering the context factors also in the decisions.**

### Prepare first cut of design

### Seek peer review and refine it

### Seek stakeholder review and refine it

### Present refined architecture to all stakeholders for their approval
