# Feature 2: Runtime Modes and Safety Configuration

## Feature Goal

Support `BACKTEST`, `PAPER`, and `LIVE` modes in MVP through explicit configuration.

Paper and live trading should share the same high-level execution pipeline. The Moomoo environment is switched by config, but live mode must require explicit safety confirmation.

## Design Patterns / Engineering Concepts

- Factory Pattern
- Options Pattern
- Ports and Adapters
- Runtime safety guard

---

## PBI 2.1: Define Runtime Mode Configuration

### Requirement

Define runtime mode and broker environment configuration.

### Checklist

- [ ] Define `RuntimeMode`: `BACKTEST`, `PAPER`, `LIVE`.
- [ ] Define `BrokerProvider`: `Moomoo`.
- [ ] Define `BrokerEnvironment`: `PAPER`, `LIVE`.
- [ ] Add `LiveTradingEnabled`.
- [ ] Add `RequireLiveConfirmation`.
- [ ] Add runtime config validation.
- [ ] Add startup summary logging.

### Acceptance Criteria

- [ ] Host can load runtime mode from config.
- [ ] Host can load broker environment from config.
- [ ] `BACKTEST` mode does not require broker connection.
- [ ] `PAPER` mode uses Moomoo paper environment.
- [ ] `LIVE` mode uses Moomoo live environment only when explicitly enabled.
- [ ] Invalid mode/environment combinations fail fast.

---

## PBI 2.2: Implement Runtime Factory

### Requirement

Create runtime-specific dependency wiring.

### Checklist

- [ ] Add `RuntimeFactory`.
- [ ] Wire backtest dependencies.
- [ ] Wire paper dependencies.
- [ ] Wire live dependencies.
- [ ] Keep Strategy Engine shared.
- [ ] Keep Risk Manager shared.
- [ ] Keep Trade Lifecycle Manager shared.
- [ ] Add tests for mode selection.

### Acceptance Criteria

- [ ] `BACKTEST` creates `HistoricalDataProvider`, `ReplayClock`, and `SimulatedBrokerAdapter`.
- [ ] `PAPER` creates realtime provider, `SystemClock`, and Moomoo paper adapter.
- [ ] `LIVE` creates realtime provider, `SystemClock`, and Moomoo live adapter.
- [ ] Strategy and risk modules are not duplicated across modes.

---

## PBI 2.3: Add Live Trading Safety Guard

### Requirement

Prevent accidental live trading.

### Checklist

- [ ] Require `Runtime.Mode = LIVE`.
- [ ] Require `Broker.Environment = LIVE`.
- [ ] Require `LiveTradingEnabled = true`.
- [ ] Require live confirmation flag.
- [ ] Log clear warning at startup.
- [ ] Block live order submission if any safety flag is missing.
- [ ] Add tests for blocked live startup.

### Acceptance Criteria

- [ ] Live mode cannot start accidentally.
- [ ] Paper mode cannot submit live orders.
- [ ] Backtest mode cannot submit broker orders.
- [ ] Live startup prints broker provider, environment, symbols, and risk limits.
- [ ] Failed safety validation produces a clear error.

---

## PBI 2.4: Add Runtime Startup Summary

### Requirement

Print a concise startup summary for debugging and auditability.

### Checklist

- [ ] Print runtime mode.
- [ ] Print broker provider and environment.
- [ ] Print trading market and currency if configured.
- [ ] Print active symbols.
- [ ] Print strategy name and version.
- [ ] Print max open positions.
- [ ] Print max position percentage per trade.
- [ ] Print minimum trade notional.
- [ ] Print minimum cash buffer.
- [ ] Print no-new-entry-before-close minutes.
- [ ] Print force-flatten settings if configured.

### Acceptance Criteria

- [ ] Startup summary is visible in logs.
- [ ] Startup summary contains enough context to diagnose wrong mode.
- [ ] Sensitive credentials are never printed.
