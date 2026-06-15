# Feature 3: Domain Models and Event Contracts

## Feature Goal

Define the core business models and event contracts before implementing runtime logic.

## Design Patterns / Engineering Concepts

- Domain Model
- Value Object
- Immutable Event
- Event Contract
- Schema Versioning

---

## PBI 3.1: Define Market Data Models

### Requirement

Create market data models for bars and quotes.

### Checklist

- [ ] Define `Symbol` value object.
- [ ] Define `BarType`.
- [ ] Define `MarketBar`.
- [ ] Define `QuoteSnapshot`.
- [ ] Use `decimal` for prices and quantities.
- [ ] Use `DateTimeOffset` for timestamps.
- [ ] Add quote validation helpers.

### Acceptance Criteria

- [ ] `MarketBar` contains symbol, timestamp, bar type, OHLCV.
- [ ] `QuoteSnapshot` contains symbol, timestamp, bid, ask, mid, spread, spread percentage.
- [ ] Invalid quote values can be rejected or flagged cleanly.
- [ ] Domain models do not reference broker SDK types.

---

## PBI 3.2: Define Strategy Signal Models

### Requirement

Create entry and exit signal models.

### Checklist

- [ ] Define base signal model.
- [ ] Define `EntrySignal`.
- [ ] Define `ExitSignal`.
- [ ] Define `StrategyParametersSnapshot`.
- [ ] Define `IndicatorSnapshot`.
- [ ] Include signal id and strategy version.
- [ ] Include human-readable reason.

### Acceptance Criteria

- [ ] Every signal has `signal_id`.
- [ ] Every signal has `strategy_name` and `strategy_version`.
- [ ] Entry signal stores planned stop loss and take profit.
- [ ] Exit signal stores exit reason.
- [ ] Signal includes indicator snapshot fields.

---

## PBI 3.3: Define Risk Models

### Requirement

Create models for risk evaluation and position group checks.

### Checklist

- [ ] Define risk decision status.
- [ ] Define risk block reason.
- [ ] Define `RiskDecision`.
- [ ] Define `PositionGroupConfig`.
- [ ] Define `PositionGroupState`.
- [ ] Support conflict symbol relationships.
- [ ] Support pending order conflict checks.

### Acceptance Criteria

- [ ] Risk decision can represent approved and blocked decisions.
- [ ] Risk decision stores `signal_id`.
- [ ] Risk decision stores `group_guard_passed`.
- [ ] Risk decision stores `group_block_reason` when blocked.
- [ ] Position group config supports conflict symbols.

---

## PBI 3.4: Define Order and Fill Models

### Requirement

Create order intent, order event, and fill models.

### Checklist

- [ ] Define order side.
- [ ] Define order type.
- [ ] Define execution status.
- [ ] Define `OrderIntent`.
- [ ] Define `OrderSubmitted`.
- [ ] Define `OrderFilled`.
- [ ] Define `OrderRejected`.
- [ ] Keep all models broker-neutral.

### Acceptance Criteria

- [ ] Order intent links back to `signal_id`.
- [ ] Order submitted event has `order_id` and submitted timestamp.
- [ ] Order filled event has executed quantity, average price, notional, and fill timestamp.
- [ ] Execution status supports `FILLED`, `PARTIAL`, `REJECTED`, and `CANCELLED`.

---

## PBI 3.5: Define Trade Lifecycle Model

### Requirement

Create the central trade lifecycle model.

### Checklist

- [ ] Define lifecycle identity fields.
- [ ] Define lifecycle status.
- [ ] Define entry fields.
- [ ] Define exit fields.
- [ ] Define PnL fields.
- [ ] Define fee fields.
- [ ] Define MFE / MAE fields.
- [ ] Define strategy snapshot fields.
- [ ] Define risk snapshot fields.

### Acceptance Criteria

- [ ] Lifecycle has `lifecycle_id`.
- [ ] Lifecycle supports `OPEN` and `CLOSED`.
- [ ] Lifecycle stores entry signal, order, price, and timestamp.
- [ ] Lifecycle stores exit signal, order, price, and timestamp after close.
- [ ] Lifecycle stores gross PnL, net PnL, total fee, and return percentage.
- [ ] Lifecycle stores MFE / MAE path metrics.

---

## PBI 3.6: Define Event Contracts

### Requirement

Define internal event contracts.

### Checklist

- [ ] Define base event metadata.
- [ ] Add `event_id`.
- [ ] Add event timestamp.
- [ ] Add `correlation_id`.
- [ ] Add schema version.
- [ ] Make events serializable to JSON.
- [ ] Add sample JSON files under `contracts/events/`.

### Acceptance Criteria

- [ ] Every event has `event_id`.
- [ ] Every event has timestamp.
- [ ] Every event has `correlation_id`.
- [ ] Every event has schema version.
- [ ] Events can be persisted in append-only format.
