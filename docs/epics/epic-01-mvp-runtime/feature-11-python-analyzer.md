# Feature 11: Python Analyzer

## Feature Goal

Analyze lifecycle output from backtest, paper trading, and live trading.

## Design Patterns / Engineering Concepts

- Read Model Analysis
- Functional Data Pipeline
- Report Generator Separation

---

## PBI 11.1: Load Lifecycle CSV

### Requirement

Read flattened lifecycle CSV into pandas.

### Checklist

- [ ] Load lifecycle CSV.
- [ ] Validate required columns.
- [ ] Parse timestamp columns.
- [ ] Parse numeric columns.
- [ ] Handle empty values.
- [ ] Return clean DataFrame.
- [ ] Add sample test CSV.

### Acceptance Criteria

- [ ] CSV loads without crash.
- [ ] Timestamp columns are parsed.
- [ ] Numeric columns are parsed.
- [ ] Empty values are handled.
- [ ] Required columns are validated.

---

## PBI 11.2: Generate Performance Report

### Requirement

Generate basic strategy performance summary.

### Checklist

- [ ] Calculate trade count.
- [ ] Calculate win rate.
- [ ] Calculate gross PnL.
- [ ] Calculate net PnL.
- [ ] Calculate average net PnL.
- [ ] Calculate return percentages.
- [ ] Calculate average holding minutes.
- [ ] Group by runtime mode.
- [ ] Group by strategy version.
- [ ] Group by symbol.
- [ ] Group by date.
- [ ] Export markdown report.
- [ ] Export summary CSV.

### Acceptance Criteria

- [ ] Markdown report is generated.
- [ ] Summary CSV is generated.
- [ ] Results can be grouped by runtime mode.
- [ ] Results can be grouped by strategy version.
- [ ] Results can be grouped by symbol.
- [ ] Results can be grouped by date.

---

## PBI 11.3: Generate Execution Quality Report

### Requirement

Analyze spread, slippage, and fee impact.

### Checklist

- [ ] Calculate average entry spread percentage.
- [ ] Calculate average exit spread percentage.
- [ ] Calculate average entry slippage.
- [ ] Calculate average exit slippage.
- [ ] Calculate slippage versus mid.
- [ ] Calculate fee percentage of notional.
- [ ] Compare gross PnL and net PnL.
- [ ] Highlight high-spread trades.
- [ ] Highlight abnormal slippage.
- [ ] Export markdown report.

### Acceptance Criteria

- [ ] Report highlights high-spread trades.
- [ ] Report highlights abnormal slippage.
- [ ] Report compares gross PnL and net PnL.
- [ ] Report shows fee impact.
- [ ] Report can be grouped by symbol and strategy version.

---

## PBI 11.4: Generate Strategy Review Report

### Requirement

Review strategy quality using lifecycle and path metrics.

### Checklist

- [ ] Group trades by entry reason.
- [ ] Group trades by exit reason.
- [ ] Analyze MFE.
- [ ] Analyze MAE.
- [ ] Compare exit price with planned stop loss.
- [ ] Compare exit price with planned take profit.
- [ ] Analyze holding minutes.
- [ ] Identify trades with large MFE but poor exit.
- [ ] Export markdown report.

### Acceptance Criteria

- [ ] Report groups by entry reason.
- [ ] Report groups by exit reason.
- [ ] Report shows average MFE / MAE.
- [ ] Report identifies trades that hit large MFE but exited poorly.
- [ ] Report produces notes useful for next parameter iteration.
