# Strangler Pattern

The Strangler Pattern is a design pattern used to incrementally refactor and replace a legacy monolithic system with a new system, typically a microservices architecture. This pattern allows for a gradual transition, reducing the risks and complexities associated with a complete rewrite.

## Description

The Strangler Pattern involves incrementally creating a new system alongside the old system, eventually replacing the old system piece by piece. The name "Strangler" comes from the analogy of a strangler fig plant that grows around a tree, gradually taking over its structure.

![Strangler Facade](https://blog.mechanicalrock.io/img/strangler-pattern/strangler-pattern.png)

### Key Concepts

- **Incremental Refactoring:** Refactor the legacy system in small, manageable pieces rather than all at once.
- **Parallel Systems:** Run the new and old systems in parallel during the transition period.
- **Seamless Cutover:** Gradually switch user traffic from the old system to the new system as functionality is replicated.

## Implementation Steps

1. **Identify Components:**
   - Identify the parts of the legacy system that need to be replaced or refactored.
   - Determine the boundaries and responsibilities of each component.

2. **Create New Services:**
   - Develop new microservices that replicate the functionality of the identified components.
   - Ensure each new service is independently deployable and scalable.

3. **Implement Routing:**
   - Use an API gateway or a routing mechanism to direct user requests to either the legacy system or the new microservices.
   - Initially, route requests to the legacy system while the new services are being developed.

4. **Incremental Replacement:**
   - Gradually switch the routing of specific functionalities from the legacy system to the new microservices.
   - Monitor the performance and behavior of the new services to ensure they work correctly.

5. **Decommission Legacy Components:**
   - Once a new microservice fully replicates the functionality of a legacy component, decommission the corresponding part of the legacy system.
   - Continue this process until the entire legacy system is replaced.

## Benefits

- **Reduced Risk:** By transitioning incrementally, the risk of introducing errors and disruptions is minimized.
- **Continuous Improvement:** Allows for continuous delivery and integration, improving the system iteratively.
- **User Transparency:** Users experience minimal disruption during the transition, as the cutover is gradual and controlled.
- **Legacy System Operation:** The legacy system can continue to operate and provide value while the new system is being developed.

## Challenges

- **Complexity:** Managing two systems in parallel can be complex and requires careful planning.
- **Consistent Data:** Ensuring data consistency between the legacy system and the new microservices can be challenging.
- **Integration:** Integrating the new microservices with existing legacy components may require additional effort.

## Example

### Scenario: Migrating an E-commerce Platform

1. **Identify Components:**
   - Identify components of the legacy e-commerce platform such as User Management, Product Catalog, Order Processing, and Payment Gateway.

2. **Create New Services:**
   - Develop microservices for User Management, Product Catalog, Order Processing, and Payment Gateway.

3. **Implement Routing:**
   - Use an API gateway to route requests. Initially, all requests are directed to the legacy system.

4. **Incremental Replacement:**
   - Gradually route user-related requests to the new User Management service.
   - Monitor and ensure the new service is functioning correctly.
   - Continue with Product Catalog, Order Processing, and Payment Gateway services.

5. **Decommission Legacy Components:**
   - Once all functionalities are handled by the new microservices, decommission the legacy system.


