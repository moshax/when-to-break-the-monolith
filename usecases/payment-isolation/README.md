# Payment Service Isolation

## 🧠 Context
In high-traffic systems, payment logic needs to be reliable, secure, and independently scalable. Coupling it with the main application can lead to latency issues and outages during traffic spikes (e.g. flash sales).

## 🎯 Goal
Isolate payment handling into its own service to:
- Scale independently based on load
- Add circuit breakers and retries without impacting user experience
- Contain failures (so a payment issue doesn’t crash the whole app)

## 🛠 Architecture Sketch
- Main app emits `PaymentRequested` events
- PaymentService consumes events, calls payment gateway, stores results
- Uses retry queue + dead letter queue for failed attempts
- Exposes internal health status and metrics

## ✅ Implementation Tips
- Use an event broker (RabbitMQ / Kafka)
- Add circuit breaker (Polly, Resilience4J)
- Store payment state in separate DB
- Mock external gateway in dev mode
