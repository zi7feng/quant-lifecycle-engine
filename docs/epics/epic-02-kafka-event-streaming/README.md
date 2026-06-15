# Epic 2: Kafka Event Streaming

## Epic Goal

Introduce Kafka after MVP event contracts are stable.

Kafka is not required for MVP. It is used for durable event streaming, replay, decoupled analytics, and scalable event processing.

## Feature Files

1. [Kafka Local Infrastructure](./feature-01-kafka-local-infrastructure.md)
2. [Kafka Event Bus](./feature-02-kafka-event-bus.md)
3. [Kafka Replay](./feature-03-kafka-replay.md)

## Epic Definition of Done

- [ ] Kafka can run locally through Docker Compose.
- [ ] Kafka UI can inspect topics.
- [ ] C# can publish events to Kafka.
- [ ] Python can consume selected events from Kafka.
- [ ] Runtime can switch between in-memory and Kafka event bus through config.
- [ ] Replay mode does not submit real orders.
