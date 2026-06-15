# Kafka Local Infrastructure

Kafka is an enrichment dependency. It is not required for MVP backtest, paper, or live runtime.

Start Kafka:

```powershell
docker compose --profile kafka up -d
```

Stop Kafka:

```powershell
docker compose --profile kafka down
```

Stop and remove local data:

```powershell
docker compose --profile kafka down -v
```

Kafka:

```text
localhost:9092
```

Kafka UI:

```text
http://localhost:8085
```
