**Status:**

Accepted





**Context:**

The platform contains multiple deployable applications.

Web
API
Worker
Future Admin

Shared business logic should not be duplicated.





**Decision:**

Use a single Nx Monorepo.



**Consequences:-**



**Advantages**

Shared TypeScript types

Shared UI

Shared validation

Shared authentication

Atomic commits

One version history



**Disadvantages**

Slight learning curve

Requires dependency management

