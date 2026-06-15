# Epic 1: MVP Runtime, Backtesting, Execution, and Analytics

## Epic Goal

Build the core QuantLifecycleEngine system.

MVP includes:

- [ ] Backtest mode.
- [ ] Paper trading mode.
- [ ] Live trading mode controlled by explicit configuration.
- [ ] Shared strategy and risk pipeline.
- [ ] Shared order routing abstraction.
- [ ] Moomoo paper/live broker adapter support.
- [ ] Trade lifecycle tracking.
- [ ] Execution quality calculation.
- [ ] Python-based analysis reports.

MVP excludes:

- [ ] Kafka as a required runtime dependency.
- [ ] Full L2 order book.
- [ ] Multi-account portfolio.
- [ ] Complex margin model.
- [ ] Full option chain execution.
- [ ] Dynamic universe selection.

## Feature Files

1. [Project Bootstrap](./feature-01-project-bootstrap.md)
2. [Runtime Modes and Safety Configuration](./feature-02-runtime-modes-safety-config.md)
3. [Domain Models and Event Contracts](./feature-03-domain-models-events.md)
4. [Market Data and Historical Data](./feature-04-market-data-historical-data.md)
5. [Event Bus and Event Store](./feature-05-event-bus-event-store.md)
6. [Strategy Engine](./feature-06-strategy-engine.md)
7. [Risk Manager and Guards](./feature-07-risk-manager-guards.md)
8. [Order Router and Broker Adapters](./feature-08-order-router-broker-adapters.md)
9. [Trade Lifecycle Manager](./feature-09-trade-lifecycle-manager.md)
10. [Backtesting Engine](./feature-10-backtesting-engine.md)
11. [Python Analyzer](./feature-11-python-analyzer.md)
12. [Tests and Runbook](./feature-12-tests-runbook.md)

## Epic Definition of Done

- [ ] `dotnet build` succeeds.
- [ ] `dotnet test` succeeds.
- [ ] Backtest mode can process historical bar and quote data.
- [ ] Paper mode can use realtime Moomoo paper environment.
- [ ] Live mode can use the same Moomoo adapter path with explicit live config.
- [ ] Strategy can generate entry and exit signals.
- [ ] Risk Manager can approve or block signals.
- [ ] PositionGroupGuard can prevent conflicting TQQQ / SQQQ positions.
- [ ] Order Router can create order intents.
- [ ] Broker adapters can return submitted and filled events.
- [ ] TradeLifecycleManager can open, update, and close lifecycles.
- [ ] Lifecycle CSV can be exported.
- [ ] Python Analyzer can generate reports.
