## Product choice
Product name: Yandex-Go
Link to the product website: https://go.yandex/
Short description of the product: Yandex's mobile app for transportation and delivery. It was built on the foundation of Yandex Taxi.
## Main components
![Yandex Go Component Diagram](diagrams/out/yandex-go/architecture-component/Component%20Diagram.svg)
[Yandex Go Component Diagram Code](diagrams/src/yandex-go/architecture-component.puml)
1) Mobile/Web Client — UI for passengers and couriers; handles ride/order creation, tracking, and payments.
2) Identity & Profile — authentication, user profiles, and device/account trust.
3) Marketplace & Matching — core business logic: pricing, ETA, driver/courier assignment, and order lifecycle.
4) Maps & Routing — geocoding, routing, real‑time navigation, and ETA updates.
5) Payments & Support — card payments, receipts, refunds, and customer support tooling.
## Data flow
![Yandex Go Sequence Diagram](diagrams/out/yandex-go/architecture-sequence/Sequence%20Diagram.svg)
[Yandex Go Sequence Diagram Code](diagrams/src/yandex-go/architecture-sequence.puml)
User opens the app, authenticates, and enters pickup/destination. The client sends the request to the Marketplace service, which queries Maps/Routing for ETA and price, then creates an order. Matching assigns a driver/courier and pushes the assignment back to the client. During the trip, the client and driver app send location updates; Maps/Routing recalculates ETA and the Marketplace updates status. After completion, Payments processes the charge and the receipt is shown to the user; Support can access the order details if needed.
## Deployment
![Yandex Go Deployment Diagram](diagrams/out/yandex-go/architecture-deployment/Deployment%20Diagram.svg)
[Yandex Go Deployment Diagram Code](diagrams/src/yandex-go/architecture-deployment.puml)
## Assumption
- *"I assume the app exposes both passenger and courier flows in a single client with role‑based UI."*
- *"I assume matching and pricing are handled by a centralized marketplace service, not on the client."*
- *"I assume routing and ETA are provided by a dedicated maps service integrated with Yandex Maps."*
## Open questions
- *"What is the exact pricing model (static vs. dynamic pricing factors) used for rides and deliveries?"*
- *"How is payment processed internally (in‑house processing vs. external payment provider)?"*
- *"What reliability/failover strategy is used for real‑time matching and location updates?"*
