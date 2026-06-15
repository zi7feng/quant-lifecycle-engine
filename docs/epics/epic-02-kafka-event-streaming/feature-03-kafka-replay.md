# Feature 3: Kafka Replay

## Feature Goal

Replay event streams for debugging and strategy comparison.

## PBI E2.3.1: Replay Stored Events from Kafka

### Checklist

- [ ] Add replay mode.
- [ ] Filter replay by date.
- [ ] Filter replay by symbol.
- [ ] Filter replay by strategy version.
- [ ] Prevent real order submission during replay.
- [ ] Export replay summary.

### Acceptance Criteria

- [ ] Replay can filter by date.
- [ ] Replay can filter by symbol.
- [ ] Replay can filter by strategy version.
- [ ] Replay mode does not submit real orders.
