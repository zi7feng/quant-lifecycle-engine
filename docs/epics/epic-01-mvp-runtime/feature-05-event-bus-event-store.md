# Feature 5: Event Bus and Event Store

## Feature Goal

Provide the internal event-driven pipeline and durable event records.

## Design Patterns / Engineering Concepts

- Observer / Publish-Subscribe
- Repository Pattern
- Event Contracts
- Append-Only Logging

---

## PBI 5.1: Define IEventBus

### Requirement

Create event bus abstraction.

### Checklist

- [ ] Define `IEventBus`.
- [ ] Add `PublishAsync`.
- [ ] Add subscription method.
- [ ] Add event handler delegate.
- [ ] Keep interface independent from Kafka.
- [ ] Add unit tests using fake event handlers.

### Acceptance Criteria

- [ ] `PublishAsync` is supported.
- [ ] Subscription is supported.
- [ ] Event handlers can be registered by event type.
- [ ] Business modules depend on `IEventBus` only.

---

## PBI 5.2: Implement InMemoryEventBus

### Requirement

Implement in-process event dispatching for MVP.

### Checklist

- [ ] Implement event handler registration.
- [ ] Implement event publishing.
- [ ] Support multiple handlers per event.
- [ ] Log handler exceptions.
- [ ] Avoid crashing the entire runtime on one handler failure unless configured.
- [ ] Add unit tests.

### Acceptance Criteria

- [ ] Events can be published inside the same process.
- [ ] Multiple handlers can subscribe to the same event.
- [ ] Exceptions are logged with event context.
- [ ] Event processing order is deterministic enough for local debugging.

---

## PBI 5.3: Implement Event Store

### Requirement

Persist key runtime events.

### Storage Options for MVP

```text
SQLite for structured records
JSONL for append-only event log
CSV export for Python
```

### Checklist

- [ ] Define `IEventStore`.
- [ ] Implement append-only JSONL event log.
- [ ] Add structured lifecycle persistence.
- [ ] Persist market events.
- [ ] Persist signal events.
- [ ] Persist risk decisions.
- [ ] Persist order and fill events.
- [ ] Persist lifecycle events.
- [ ] Add correlation id to persisted events.

### Acceptance Criteria

- [ ] Market events can be stored.
- [ ] Signal events can be stored.
- [ ] Risk decisions can be stored.
- [ ] Order and fill events can be stored.
- [ ] Lifecycle events can be stored.
- [ ] Events include `correlation_id`.

---

## PBI 5.4: Implement Lifecycle CSV Export

### Requirement

Export flattened lifecycle records for Python analysis.

### Checklist

- [ ] Define lifecycle export model.
- [ ] Map lifecycle domain model to flattened row.
- [ ] Preserve entry raw execution fields.
- [ ] Preserve exit raw execution fields.
- [ ] Preserve strategy version.
- [ ] Preserve risk and group guard fields.
- [ ] Export ISO timestamps.
- [ ] Add sample export test.

### Acceptance Criteria

- [ ] CSV can be loaded by pandas.
- [ ] Column names are stable.
- [ ] Numeric fields are exported consistently.
- [ ] Timestamp fields are ISO formatted.
- [ ] Entry and exit raw execution fields are preserved.
- [ ] Strategy version is preserved.
