# Feature 2: Kafka Event Bus

## Feature Goal

Add Kafka implementation behind the existing event bus abstraction.

## Design Patterns / Engineering Concepts

- Adapter Pattern
- Publish-Subscribe
- Event Versioning
- Dependency Inversion

---

## PBI E2.2.1: Implement KafkaEventBus

### Checklist

- [ ] Add Kafka producer package to Infrastructure.
- [ ] Add Kafka consumer package to Infrastructure.
- [ ] Implement `KafkaEventBus`.
- [ ] Keep Application layer dependent only on `IEventBus`.
- [ ] Add config switch between in-memory and Kafka.
- [ ] Include event version in Kafka messages.
- [ ] Include correlation id in Kafka messages.
- [ ] Add local integration test if feasible.

### Acceptance Criteria

- [ ] Application layer still depends only on `IEventBus`.
- [ ] Kafka implementation lives in Infrastructure.
- [ ] Runtime can switch between `InMemoryEventBus` and `KafkaEventBus` by config.
- [ ] Kafka events include event version and correlation id.

---

## PBI E2.2.2: Define Kafka Topics

### Topics

```text
market.bars.1m
market.bars.5m
market.quotes.l1
strategy.signals
risk.decisions
orders.submitted
orders.filled
trade.lifecycles
portfolio.snapshots
```

### Checklist

- [ ] Define topic naming convention.
- [ ] Define topic event schema.
- [ ] Define event key strategy.
- [ ] Define partitioning strategy.
- [ ] Define retention policy.
- [ ] Document all topics in `docs/kafka-topics.md`.

### Acceptance Criteria

- [ ] Each topic has documented event schema.
- [ ] Topic naming is consistent.
- [ ] Event keys are defined.
- [ ] Partitioning strategy is documented.

---

## PBI E2.2.3: Add Python Kafka Consumer

### Checklist

- [ ] Add Python Kafka dependency.
- [ ] Implement lifecycle consumer.
- [ ] Implement fill consumer.
- [ ] Handle duplicate events safely.
- [ ] Generate near-real-time summary.
- [ ] Document local run command.

### Acceptance Criteria

- [ ] Python can consume `trade.lifecycles`.
- [ ] Python can consume `orders.filled`.
- [ ] Python can generate near-real-time summary.
- [ ] Consumer handles duplicate events safely.
