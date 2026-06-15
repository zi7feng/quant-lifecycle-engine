# Feature 10: Backtesting Engine

## Feature Goal

Run historical backtests using the same strategy, risk, order, and lifecycle pipeline as paper/live trading.

## Design Patterns / Engineering Concepts

- Template Method
- Adapter Pattern
- Strategy Pattern
- Factory Pattern
- Deterministic Clock Abstraction

---

## PBI 10.1: Define BacktestConfig

### Requirement

Create backtest configuration model.

### Checklist

- [ ] Define backtest config model.
- [ ] Load config from JSON.
- [ ] Generate run id if missing.
- [ ] Save config snapshot into run output directory.
- [ ] Validate date range.
- [ ] Validate symbols.
- [ ] Validate strategy config.
- [ ] Validate output directory.

### Acceptance Criteria

- [ ] Backtest config can be loaded from JSON.
- [ ] `run_id` is generated if missing.
- [ ] Strategy parameters are saved with run output.
- [ ] Backtest output directory is created automatically.

---

## PBI 10.2: Implement ReplayClock

### Requirement

Backtest must use replay time, not system time.

### Checklist

- [ ] Define `IClock`.
- [ ] Implement `SystemClock`.
- [ ] Implement `ReplayClock`.
- [ ] Ensure strategy receives replay time.
- [ ] Ensure risk logic receives replay time.
- [ ] Add tests for time advancement.

### Acceptance Criteria

- [ ] Current time comes from `ReplayClock`.
- [ ] `ReplayClock` advances with historical market events.
- [ ] Strategy and risk logic use replay time.
- [ ] `no_new_entry_before_close_minutes` works in backtest.

---

## PBI 10.3: Implement PortfolioSimulator

### Requirement

Maintain cash and positions in backtest mode.

### Checklist

- [ ] Load initial cash.
- [ ] Update cash after buy fill.
- [ ] Update cash after sell fill.
- [ ] Update position quantity.
- [ ] Update average cost.
- [ ] Expose positions to Risk Manager.
- [ ] Block insufficient cash.
- [ ] Add tests for cash and position updates.

### Acceptance Criteria

- [ ] Initial cash is loaded.
- [ ] Buy fill reduces cash.
- [ ] Sell fill increases cash.
- [ ] Position quantity is updated.
- [ ] Average cost is updated.
- [ ] Risk Manager can query current positions.
- [ ] Insufficient cash blocks new entries unless margin is explicitly enabled.

---

## PBI 10.4: Implement BacktestRunner

### Requirement

Create the main historical event loop.

### Checklist

- [ ] Load historical data.
- [ ] Merge market events by timestamp.
- [ ] Publish market data events.
- [ ] Run strategy evaluation.
- [ ] Run risk evaluation.
- [ ] Generate order intents.
- [ ] Simulate fills.
- [ ] Update portfolio.
- [ ] Update lifecycle.
- [ ] Persist events.
- [ ] Export lifecycle CSV.
- [ ] Export summary JSON.
- [ ] Add integration test with small sample data.

### Acceptance Criteria

- [ ] Backtest runner loads historical data.
- [ ] Events are processed in timestamp order.
- [ ] Market data events trigger strategy evaluation.
- [ ] Approved signals trigger simulated orders.
- [ ] Simulated fills update portfolio and lifecycle.
- [ ] Backtest outputs lifecycle CSV and summary JSON.

---

## PBI 10.5: Backtest Summary Export

### Requirement

Generate summary output for each backtest run.

### Metrics

```text
trade_count
win_rate
gross_pnl
net_pnl
total_fee
avg_slippage
avg_holding_minutes
max_drawdown_simple
```

### Checklist

- [ ] Calculate trade count.
- [ ] Calculate win rate.
- [ ] Calculate gross PnL.
- [ ] Calculate net PnL.
- [ ] Calculate total fee.
- [ ] Calculate average slippage.
- [ ] Calculate average holding minutes.
- [ ] Calculate simple max drawdown.
- [ ] Export `summary.json`.
- [ ] Export `summary.csv`.

### Acceptance Criteria

- [ ] `summary.json` is generated.
- [ ] `summary.csv` is generated.
- [ ] Summary includes strategy version.
- [ ] Summary includes date range.
- [ ] Summary includes initial and final portfolio value.
