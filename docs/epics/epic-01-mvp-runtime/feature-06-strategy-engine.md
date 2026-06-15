# Feature 6: Strategy Engine

## Feature Goal

Implement the shared strategy interface and the first momentum breakout strategy.

## Design Patterns / Engineering Concepts

- Strategy Pattern
- Template Method / Pipeline Orchestration
- Snapshot Model
- Pure Calculation Services

---

## PBI 6.1: Define Strategy Interface

### Requirement

Create a reusable strategy contract.

### Checklist

- [ ] Define `ITradingStrategy`.
- [ ] Define market context input.
- [ ] Define portfolio context input.
- [ ] Define strategy evaluation result.
- [ ] Support entry signal.
- [ ] Support exit signal.
- [ ] Support no-signal result.
- [ ] Prevent broker dependency in strategy layer.

### Acceptance Criteria

- [ ] Strategy receives market context.
- [ ] Strategy receives portfolio context.
- [ ] Strategy can return entry signal.
- [ ] Strategy can return exit signal.
- [ ] Strategy can return no-signal result.
- [ ] Strategy does not call broker directly.
- [ ] Strategy does not update lifecycle directly.

---

## PBI 6.2: Implement Indicator Calculator

### Requirement

Implement indicators needed by MomentumBreakoutStrategy.

### Indicators

```text
breakout_high_prev
breakout_threshold
trend_ma
vwap
avg_volume
atr
```

### Checklist

- [ ] Implement breakout high calculation.
- [ ] Implement breakout threshold calculation.
- [ ] Implement trend moving average.
- [ ] Implement VWAP.
- [ ] Implement average volume.
- [ ] Implement ATR.
- [ ] Handle insufficient lookback data.
- [ ] Store indicator values in snapshot.
- [ ] Add unit tests.

### Acceptance Criteria

- [ ] Each indicator has unit tests.
- [ ] Insufficient lookback data returns no signal.
- [ ] Indicator values can be stored in signal snapshot.
- [ ] Decimal precision is handled consistently.

---

## PBI 6.3: Implement MomentumBreakout Entry Logic

### Requirement

Implement current momentum breakout entry logic.

### Checklist

- [ ] Load strategy parameters from config.
- [ ] Evaluate breakout condition.
- [ ] Evaluate volume filter.
- [ ] Evaluate trend filter.
- [ ] Evaluate VWAP filter when enabled.
- [ ] Calculate planned stop loss.
- [ ] Calculate planned take profit.
- [ ] Generate entry reason.
- [ ] Generate indicator snapshot.
- [ ] Add tests for signal and no-signal cases.

### Acceptance Criteria

- [ ] Entry signal is generated only when breakout condition passes.
- [ ] Volume filter is applied.
- [ ] Trend filter is applied.
- [ ] VWAP filter is applied when enabled.
- [ ] Planned stop loss is calculated.
- [ ] Planned take profit is calculated.
- [ ] Entry reason is human-readable and includes key values.

---

## PBI 6.4: Implement Exit Logic

### Requirement

Implement basic exit conditions.

### Exit Reasons

```text
TREND_BREAKDOWN
STOP_LOSS
TAKE_PROFIT
```

### Checklist

- [ ] Detect trend breakdown.
- [ ] Detect stop loss.
- [ ] Detect take profit.
- [ ] Link exit signal to open lifecycle.
- [ ] Store exit reason.
- [ ] Store indicator snapshot.
- [ ] Add tests for each exit reason.

### Acceptance Criteria

- [ ] Exit signal links to open lifecycle.
- [ ] Exit signal stores exit reason.
- [ ] Exit logic uses latest market data.
- [ ] Exit signal includes indicator snapshot.
- [ ] Exit signal does not directly submit order.
