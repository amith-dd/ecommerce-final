# ecommerce-final
This project is a practical demonstration of building a resilient and scalable backend for an e-commerce platform using a microservices architecture with Spring Boot. It simulates the core functionalities of order placement, inventory management, payment processing, and customer notifications.


The system emphasizes modern cloud-native development practices by integrating several key Spring Cloud components and architectural patterns:

Microservices: The application is decomposed into independent, loosely coupled services (Order-Service, Inventory-Service, Payment-Service, Notification-Service), each responsible for a specific business capability. This design promotes modularity, independent deployment, and easier maintenance.


Centralized Configuration (Spring Cloud Config): All microservices retrieve their configuration (e.g., database connection details, service endpoints) from a centralized Spring Cloud Config Server backed by a Git repository. This allows for dynamic updates to properties without requiring service redeployments, facilitating easy environment management (e.g., dev vs. prod profiles).


Secure Secret Management (HashiCorp Vault): Sensitive data, such as database credentials and external API keys, is securely stored and retrieved from HashiCorp Vault via Spring Cloud Vault Config. This enhances security by preventing hardcoding of secrets within application code or configuration files.

Service Discovery (Eureka): Microservices register themselves with a Eureka Server, enabling them to discover and communicate with each other dynamically by service name rather than hardcoded IP addresses or ports.

Inter-Service Communication (FeignClient): Synchronous HTTP-based communication between services (e.g., Order-Service calling Inventory-Service and Payment-Service) is efficiently managed using Spring Cloud OpenFeign, which simplifies REST client declarations.

Distributed Transactions & Compensation: While each microservice manages its own local database transactions, the Order-Service implements a manual compensation mechanism (akin to a simplified Saga pattern) to handle distributed transactions. If a downstream operation (like payment processing) fails, the Order-Service triggers compensating actions (e.g., restoring inventory) to maintain data consistency across services.


Asynchronous Processing (Spring @Async): The system leverages Spring's @Async annotation to perform non-blocking operations, such as triggering customer notifications, on separate threads. This improves the responsiveness of critical API endpoints by offloading non-essential tasks.

Distributed Tracing (Spring Cloud Sleuth & Zipkin): Spring Cloud Sleuth automatically injects trace and span IDs into requests as they flow across different microservices. All trace data is sent to a Zipkin server, providing end-to-end visibility into request paths, latency, and dependencies, which is invaluable for debugging and performance monitoring in a distributed environment.
