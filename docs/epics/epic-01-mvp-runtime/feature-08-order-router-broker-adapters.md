# Feature 8: Order Router and Broker Adapters

## Feature Goal

Convert approved signals into order intents and support simulated, paper, and live execution paths.

## Design Patterns / Engineering Concepts

- Adapter Pattern
- Strategy Pattern
- Factory Pattern
- Ports and Adapters
- Safety Guard

---

## PBI 8.1: Implement Order Router

### Requirement

Convert approved signals into order intents.

### Checklist

- [ ] Convert entry signal to buy order intent.
- [ ] Convert exit signal to sell order intent.
- [ ] Calculate quantity.
- [ ] Calculate submitted notional.
- [ ] Link order intent to signal id.
- [ ] Persist order intent before execution.
- [ ] Add tests for buy and sell orders.

### Acceptance Criteria

- [ ] Entry signal becomes buy order intent.
- [ ] Exit signal becomes sell order intent.
- [ ] Order intent has side, quantity, order type, and notional.
- [ ] Order intent links to `signal_id`.
- [ ] Order intent is persisted before execution.

---

## PBI 8.2: Implement Broker Adapter Interface

### Requirement

Define broker-neutral execution interface.

### Checklist

- [ ] Define `IBrokerAdapter`.
- [ ] Add submit order method.
- [ ] Add query order status method if needed.
- [ ] Add cancel order method if needed.
- [ ] Keep broker SDK types out of Domain.
- [ ] Add fake broker implementation for tests.

### Acceptance Criteria

- [ ] Application layer depends on `IBrokerAdapter`.
- [ ] Simulated, paper, and live adapters implement the same interface.
- [ ] Broker adapter returns internal order and fill models.
- [ ] Broker-specific errors are mapped to internal errors.

---

## PBI 8.3: Implement SimulatedBrokerAdapter

### Requirement

Support backtest execution simulation.

### Checklist

- [ ] Fill market buy using ask price when quote exists.
- [ ] Fill market sell using bid price when quote exists.
- [ ] Define fallback fill price rule when quote is missing.
- [ ] Emit submitted event.
- [ ] Emit filled event.
- [ ] Include execution status.
- [ ] Add tests for buy, sell, and missing quote cases.

### Acceptance Criteria

- [ ] Market buy can fill using ask price when quote exists.
- [ ] Market sell can fill using bid price when quote exists.
- [ ] If quote is missing, fallback price rule is explicit.
- [ ] Fill event format matches paper/live fill event format.
- [ ] Fill includes execution status.
- [ ] Fill includes executed quantity and average price.

---

## PBI 8.4: Implement Moomoo Paper/Live Broker Adapter

### Requirement

Implement Moomoo broker adapter with environment switching through config.

### Checklist

- [ ] Implement Moomoo adapter behind `IBrokerAdapter`.
- [ ] Support `Broker.Environment = PAPER`.
- [ ] Support `Broker.Environment = LIVE`.
- [ ] Map submitted order response to internal model.
- [ ] Map fill response to internal model.
- [ ] Map rejection / cancellation to internal model.
- [ ] Block live order submission unless live safety config passes.
- [ ] Add adapter tests using fake responses.

### Acceptance Criteria

- [ ] Paper mode can submit paper orders.
- [ ] Live mode can submit live orders only when explicitly enabled.
- [ ] Switching paper/live does not change Strategy Engine or Risk Manager.
- [ ] Broker raw fields are captured for lifecycle export.
- [ ] Broker SDK types do not leak into Domain layer.

---

## PBI 8.5: Implement Fee Model

### Requirement

Support estimated fees.

### Checklist

- [ ] Define `IFeeModel`.
- [ ] Implement fixed commission model.
- [ ] Implement platform fee model.
- [ ] Calculate total estimated fee.
- [ ] Calculate fee percentage of notional.
- [ ] Support entry and exit fees.
- [ ] Add unit tests.

### Acceptance Criteria

- [ ] Fixed commission can be configured.
- [ ] Platform fee can be configured.
- [ ] `total_estimated_fee` is calculated.
- [ ] `fee_pct_of_notional` is calculated.
- [ ] Entry and exit fees are both supported.

---

## PBI 8.6: Implement Slippage Model

### Requirement

Support basic slippage calculation.

### Models

```text
NoneSlippageModel
FixedBpsSlippageModel
SpreadAwareSlippageModel
```

### Checklist

- [ ] Define `ISlippageModel`.
- [ ] Implement no-slippage model.
- [ ] Implement fixed basis points slippage model.
- [ ] Implement spread-aware slippage model.
- [ ] Ensure buy slippage direction is correct.
- [ ] Ensure sell slippage direction is correct.
- [ ] Calculate absolute slippage.
- [ ] Calculate slippage percentage.
- [ ] Calculate slippage versus mid.
- [ ] Calculate slippage versus bid / ask.
- [ ] Add unit tests.

### Acceptance Criteria

- [ ] Buy slippage direction is correct.
- [ ] Sell slippage direction is correct.
- [ ] `slippage_abs` is calculated.
- [ ] `slippage_pct` is calculated.
- [ ] `slippage_vs_mid` is calculated.
- [ ] `slippage_vs_bid_ask` is calculated.
