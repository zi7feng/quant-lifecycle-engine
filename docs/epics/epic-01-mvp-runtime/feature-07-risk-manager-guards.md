# Feature 7: Risk Manager and Guards

## Feature Goal

Separate signal generation from trading permission and enforce account, strategy, and position-group constraints.

## Design Patterns / Engineering Concepts

- Chain of Responsibility
- Specification Pattern
- Policy-Based Risk Checks
- Domain Service

---

## PBI 7.1: Implement Global Risk Checks

### Requirement

Validate account-level and strategy-level risk constraints.

### Rules

```text
max_open_positions
max_position_pct_per_trade
min_trade_notional
min_cash_buffer
no_new_entry_before_close_minutes
force_flatten_before_close
force_flatten_minutes_before_close
```

### Checklist

- [ ] Implement max open positions check.
- [ ] Implement position percentage check.
- [ ] Implement minimum notional check.
- [ ] Implement minimum cash buffer check.
- [ ] Implement no-new-entry-before-close check.
- [ ] Implement force-flatten-before-close config.
- [ ] Generate approved decision.
- [ ] Generate blocked decision.
- [ ] Persist decision.

### Acceptance Criteria

- [ ] Approved signal creates approved risk decision.
- [ ] Blocked signal creates blocked risk decision.
- [ ] Blocked decision has clear reason.
- [ ] Risk decision stores `signal_id`.
- [ ] Risk decision is persisted.

---

## PBI 7.2: Implement Position Group Guard

### Requirement

Support mutual exclusion and group-level position limits.

### Example

```text
Position group: NASDAQ_3X_PAIR
Symbols: US.TQQQ, US.SQQQ
group_max_open_positions: 1
conflict_symbol:
  US.TQQQ -> US.SQQQ
  US.SQQQ -> US.TQQQ
```

### Checklist

- [ ] Load position group config.
- [ ] Calculate group open count.
- [ ] Detect conflicting open position.
- [ ] Detect conflicting pending buy.
- [ ] Enforce group max open positions.
- [ ] Record `group_guard_passed`.
- [ ] Record `group_block_reason`.
- [ ] Add tests for TQQQ / SQQQ conflict.

### Acceptance Criteria

- [ ] Existing conflicting open position blocks new entry.
- [ ] Existing conflicting pending buy blocks new entry.
- [ ] `group_open_count` is calculated correctly.
- [ ] `group_guard_passed` is recorded.
- [ ] `group_block_reason` is recorded.

---

## PBI 7.3: Implement Pending Order Ledger

### Requirement

Track pending orders so risk checks can block duplicate or conflicting pending entries.

### Checklist

- [ ] Define pending order ledger interface.
- [ ] Add pending order on submit.
- [ ] Remove or update pending order on fill, cancel, or reject.
- [ ] Query pending buys by symbol.
- [ ] Query conflicting pending buys by position group.
- [ ] Add unit tests.

### Acceptance Criteria

- [ ] Duplicate pending buy can be detected.
- [ ] Conflicting pending buy can be detected.
- [ ] Pending state is updated after fill.
- [ ] Pending state is updated after rejection or cancellation.
