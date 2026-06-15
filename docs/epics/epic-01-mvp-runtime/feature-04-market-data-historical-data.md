# Feature 4: Market Data and Historical Data

## Feature Goal

Support realtime market input and historical data replay.

## Design Patterns / Engineering Concepts

- Adapter Pattern
- Ports and Adapters
- Validation Pipeline
- Data Normalization

---

## PBI 4.1: Implement Market Data Provider Interface

### Requirement

Define a broker-neutral market data provider interface.

### Checklist

- [ ] Define `IMarketDataProvider`.
- [ ] Add method for loading bars.
- [ ] Add method for loading quote snapshots.
- [ ] Keep interface independent from broker SDK.
- [ ] Add fake provider for tests.

### Acceptance Criteria

- [ ] Interface supports loading recent bars.
- [ ] Interface supports loading quote snapshots.
- [ ] Interface is independent from concrete broker SDK.
- [ ] Application layer depends on interface, not implementation.

---

## PBI 4.2: Implement Historical Data Provider

### Requirement

Read historical bar and quote data from local files or SQLite.

### Checklist

- [ ] Load bars by symbol and date range.
- [ ] Load quotes by symbol and date range.
- [ ] Sort data by timestamp.
- [ ] Detect missing data.
- [ ] Detect invalid data.
- [ ] Add test fixture files.

### Acceptance Criteria

- [ ] Can load bars by symbol and date range.
- [ ] Can load quote snapshots by symbol and date range.
- [ ] Data is sorted by timestamp.
- [ ] Missing data is logged as warning.
- [ ] Invalid quotes are excluded or flagged.

---

## PBI 4.3: Implement Realtime Moomoo Market Data Adapter

### Requirement

Create a Moomoo realtime market data adapter for paper and live modes.

### Checklist

- [ ] Implement adapter behind `IMarketDataProvider`.
- [ ] Load bars for active symbols.
- [ ] Load quote snapshots for active symbols.
- [ ] Map broker raw fields to internal domain models.
- [ ] Keep broker SDK types out of Domain and Application models.
- [ ] Add adapter-level logging.

### Acceptance Criteria

- [ ] Paper mode can receive realtime bar / quote data.
- [ ] Live mode can receive realtime bar / quote data.
- [ ] Adapter output uses internal models only.
- [ ] Adapter errors contain symbol and timestamp context.

---

## PBI 4.4: Implement Market Data Validation

### Requirement

Add data quality checks.

### Validation Rules

```text
bid > 0
ask > 0
ask >= bid
bar high >= low
bar volume >= 0
timestamp is not default
```

### Checklist

- [ ] Validate quote bid.
- [ ] Validate quote ask.
- [ ] Validate bid / ask relationship.
- [ ] Validate bar high / low relationship.
- [ ] Validate bar volume.
- [ ] Validate timestamp.
- [ ] Persist validation warnings.

### Acceptance Criteria

- [ ] Invalid quote does not enter strategy calculation.
- [ ] Invalid bar does not enter strategy calculation.
- [ ] Validation errors include symbol and timestamp.
- [ ] Warnings are persisted for later debugging.

---

## PBI 4.5: Implement Quote Feature Calculation

### Requirement

Calculate quote-level features.

### Checklist

- [ ] Calculate mid price.
- [ ] Calculate spread.
- [ ] Calculate spread percentage.
- [ ] Handle division by zero.
- [ ] Add normal-case tests.
- [ ] Add invalid-case tests.

### Acceptance Criteria

- [ ] `mid_price = (bid + ask) / 2`.
- [ ] `spread = ask - bid`.
- [ ] `spread_pct = spread / mid_price`.
- [ ] Division by zero is handled.
- [ ] Unit tests cover normal and invalid cases.
