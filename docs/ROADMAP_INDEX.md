# QuantLifecycleEngine Roadmap Index

## Project Goal

QuantLifecycleEngine is a C# trading system for strategy research, backtesting, paper trading, live trading, execution review, and lifecycle-based analytics.

The system focuses on a clear end-to-end workflow:

```text
Historical / realtime market data
  -> Market data normalization
  -> Strategy signal generation
  -> Risk and position-group checks
  -> Order intent generation
  -> Simulated / paper / live execution
  -> Trade lifecycle tracking
  -> Event and trade persistence
  -> Python analysis and reporting
```

## Runtime Modes

MVP includes all three runtime modes:

```text
BACKTEST
PAPER
LIVE
```

Runtime mode is selected by configuration. For the Moomoo-based runtime, paper and live trading should use the same high-level broker adapter contract and switch environment through config.

Recommended config shape:

```json
{
  "Runtime": {
    "Mode": "PAPER"
  },
  "Broker": {
    "Provider": "Moomoo",
    "Environment": "PAPER",
    "LiveTradingEnabled": false,
    "RequireLiveConfirmation": true
  }
}
```

Rules:

- `BACKTEST` uses `HistoricalDataProvider`, `ReplayClock`, `SimulatedBrokerAdapter`, and `PortfolioSimulator`.
- `PAPER` uses realtime data, `SystemClock`, and Moomoo paper environment.
- `LIVE` uses realtime data, `SystemClock`, and Moomoo live environment.
- Live mode must be explicit and protected by safety config.
- The same Strategy Engine, Risk Manager, Order Router interface, Trade Lifecycle Manager, Event Store, and Python output schema should be shared across modes.

## Repository Layout

```text
quant-lifecycle-engine/
  README.md
  docker-compose.yml
  .dockerignore
  .gitignore

  docs/
    ROADMAP_INDEX.md
    architecture.md
    e2e-behavior.md
    branching-policy.md
    setup-csharp.md
    docker-compose.md
    epics/
      epic-01-mvp-runtime/
      epic-02-kafka-event-streaming/
      epic-03-orderbook-market-microstructure/
      epic-04-advanced-research/

  src/
    QuantLifecycleEngine.sln
    QuantLifecycleEngine.Host/
    QuantLifecycleEngine.Domain/
    QuantLifecycleEngine.Application/
    QuantLifecycleEngine.Infrastructure/
    QuantLifecycleEngine.Backtesting/

  tests/
    QuantLifecycleEngine.Domain.Tests/
    QuantLifecycleEngine.Application.Tests/
    QuantLifecycleEngine.Infrastructure.Tests/
    QuantLifecycleEngine.Backtesting.Tests/

  python/
    analyzer/
    notebooks/
    requirements.txt

  contracts/
    events/

  data/
    raw/
    normalized/
    exports/
    reports/
    backtest/

  infra/
    docker/
      kafka/

  scripts/
```

## Epic Structure

- [Epic 1: MVP Runtime, Backtesting, Execution, and Analytics](./epics/epic-01-mvp-runtime/README.md)
- [Epic 2: Kafka Event Streaming](./epics/epic-02-kafka-event-streaming/README.md)
- [Epic 3: Order Book and Market Microstructure](./epics/epic-03-orderbook-market-microstructure/README.md)
- [Epic 4: Advanced Research](./epics/epic-04-advanced-research/README.md)

## Design Patterns

The project should intentionally use these patterns:

| Pattern | Where Used | Purpose |
|---|---|---|
| Ports and Adapters | Market data, broker, storage, event bus | Keep application logic independent from external systems |
| Strategy Pattern | Trading strategy, fee model, slippage model, fill model | Swap behavior without changing orchestration |
| Factory Pattern | Runtime adapter creation | Select backtest, paper, or live implementations from config |
| Observer / Pub-Sub | `IEventBus` | Decouple event producers and consumers |
| Repository Pattern | Event store, lifecycle store, backtest run store | Hide persistence details |
| State Pattern | Trade lifecycle | Control valid lifecycle transitions |
| Specification / Chain of Responsibility | Risk checks | Compose risk rules cleanly |
| Template Method / Pipeline | Runtime loop and backtest runner | Keep a consistent trading pipeline across modes |

## Recommended Implementation Order

1. Project bootstrap and solution structure.
2. Runtime mode and safety configuration.
3. Domain models and event contracts.
4. Market data and historical data providers.
5. Event bus and persistence.
6. Strategy engine.
7. Risk manager and guards.
8. Order router and broker adapters.
9. Trade lifecycle manager.
10. Backtesting engine.
11. Python analyzer.
12. Tests and runbook.
13. Kafka enrichment.
14. Order book enrichment.
15. Advanced research enrichment.
