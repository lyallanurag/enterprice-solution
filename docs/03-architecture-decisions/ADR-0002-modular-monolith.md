**Status:**

Accepted





**Context**

Building microservices initially introduces unnecessary complexity.





**Decision:**

The backend will be a Modular Monolith.



**Modules:**

Identity



Marketplace



Projects



Ticket



Payments



Notifications



Each module owns its own business rules.



**Future:**

Modules may later become independent ECS services.

