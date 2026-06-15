# Feature 9: Trade Lifecycle Manager

## Feature Goal

Track every trade from entry signal to exit fill and generate analysis-ready lifecycle output.

## Design Patterns / Engineering Concepts

- State Pattern
- Repository Pattern
- Read Model / Projection
- Domain Service

---

## PBI 9.1: Open Lifecycle on Entry Fill

### Requirement

Create lifecycle after entry fill.

### Checklist

- [ ] Generate lifecycle id.
- [ ] Set status to open.
- [ ] Store entry signal id.
- [ ] Store entry order id.
- [ ] Store entry price.
- [ ] Store entry executed timestamp.
- [ ] Store entry strategy config snapshot.
- [ ] Store entry execution quality fields.

### Acceptance Criteria

- [ ] `lifecycle_id` is generated.
- [ ] `trade_status` is `OPEN`.
- [ ] `entry_signal_id` is stored.
- [ ] `entry_order_id` is stored.
- [ ] `entry_price` is stored.
- [ ] `entry_executed_at` is stored.
- [ ] Entry strategy config snapshot is stored.

---

## PBI 9.2: Update Path Metrics During Open Position

### Requirement

Update MFE / MAE while trade is open.

### Checklist

- [ ] Update max high since entry.
- [ ] Update min low since entry.
- [ ] Update MFE since entry.
- [ ] Update MAE since entry.
- [ ] Update MFE percentage.
- [ ] Update MAE percentage.
- [ ] Update last path metrics bar time.
- [ ] Add tests for long position path metrics.

### Acceptance Criteria

- [ ] `max_high_since_entry` is updated.
- [ ] `min_low_since_entry` is updated.
- [ ] `mfe_since_entry` is updated.
- [ ] `mae_since_entry` is updated.
- [ ] `mfe_pct_since_entry` is updated.
- [ ] `mae_pct_since_entry` is updated.
- [ ] `path_metrics_last_bar_time` is updated.

---

## PBI 9.3: Close Lifecycle on Exit Fill

### Requirement

Close lifecycle after exit fill.

### Checklist

- [ ] Set status to closed.
- [ ] Store exit signal id.
- [ ] Store exit order id.
- [ ] Store exit price.
- [ ] Store exit executed timestamp.
- [ ] Calculate holding minutes.
- [ ] Calculate gross PnL.
- [ ] Calculate net PnL.
- [ ] Calculate total estimated fee.
- [ ] Store exit reason.
- [ ] Add tests for closing lifecycle.

### Acceptance Criteria

- [ ] `trade_status` becomes `CLOSED`.
- [ ] `exit_signal_id` is stored.
- [ ] `exit_order_id` is stored.
- [ ] `exit_price` is stored.
- [ ] `exit_executed_at` is stored.
- [ ] `holding_minutes` is calculated.
- [ ] `gross_pnl` is calculated.
- [ ] `net_pnl` is calculated.
- [ ] `total_estimated_fee` is calculated.
- [ ] `exit_reason` is stored.

---

## PBI 9.4: Generate Flattened Lifecycle Record

### Requirement

Generate a wide lifecycle record compatible with Python analysis.

### Checklist

- [ ] Include identity fields.
- [ ] Include strategy version fields.
- [ ] Include risk and group guard fields.
- [ ] Include entry raw execution fields.
- [ ] Include exit raw execution fields.
- [ ] Include PnL fields.
- [ ] Include MFE / MAE fields.
- [ ] Include slippage fields.
- [ ] Include spread fields.
- [ ] Add export mapping test.

### Acceptance Criteria

- [ ] Identity fields are included.
- [ ] Strategy version fields are included.
- [ ] Risk and group guard fields are included.
- [ ] Entry raw execution fields are included.
- [ ] Exit raw execution fields are included.
- [ ] PnL fields are included.
- [ ] MFE / MAE fields are included.
- [ ] Slippage and spread fields are included.
