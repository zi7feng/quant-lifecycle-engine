# Feature 1: Kafka Local Infrastructure

## Feature Goal

Use Docker Compose to run local Kafka infrastructure.

## PBI E2.1.1: Add Docker Compose for Kafka

### Checklist

- [ ] Add Kafka service to `docker-compose.yml`.
- [ ] Add Kafka UI service to `docker-compose.yml`.
- [ ] Use Compose profile `kafka`.
- [ ] Document startup command.
- [ ] Document shutdown command.
- [ ] Confirm Kafka is reachable locally.
- [ ] Confirm Kafka UI is reachable locally.
- [ ] Confirm Kafka is not required for MVP mode.

### Acceptance Criteria

- [ ] `docker compose --profile kafka up -d` starts Kafka.
- [ ] Kafka is reachable at `localhost:9092`.
- [ ] Kafka UI is reachable at `localhost:8085`.
- [ ] README documents startup and shutdown commands.
- [ ] Kafka is not required for backtest, paper, or live MVP modes.
