# Feature 12: Tests and Runbook

## Feature Goal

Make the system runnable, testable, and operationally clear.

## Design Patterns / Engineering Concepts

- Test Pyramid
- Deterministic Test Data
- Local Runbook
- Operational Workflow

---

## PBI 12.1: Add Unit Tests for Core Calculations

### Requirement

Test core business logic.

### Coverage Areas

```text
indicator calculation
risk checks
position group guard
fee calculation
slippage calculation
PnL calculation
MFE / MAE calculation
runtime safety config
```

### Checklist

- [ ] Add indicator calculation tests.
- [ ] Add risk check tests.
- [ ] Add position group guard tests.
- [ ] Add fee calculation tests.
- [ ] Add slippage calculation tests.
- [ ] Add PnL calculation tests.
- [ ] Add MFE / MAE calculation tests.
- [ ] Add runtime mode safety tests.
- [ ] Ensure tests do not require broker connection.

### Acceptance Criteria

- [ ] Each calculation has normal-case tests.
- [ ] Each calculation has edge-case tests.
- [ ] Tests can run locally with `dotnet test`.
- [ ] Tests do not require broker connection.

---

## PBI 12.2: Add Local Run Scripts

### Requirement

Create scripts for local execution.

### Scripts

```text
scripts/run-csharp.ps1
scripts/run-backtest.ps1
scripts/run-analyzer.ps1
```

### Checklist

- [ ] Add C# runtime script.
- [ ] Add backtest script.
- [ ] Add Python analyzer script.
- [ ] Validate required files before running.
- [ ] Print clear error messages.
- [ ] Document script usage in README.

### Acceptance Criteria

- [ ] C# runtime can be started from script.
- [ ] Backtest can be started from script.
- [ ] Python analyzer can be started from script.
- [ ] Scripts fail clearly when required files are missing.

---

## PBI 12.3: Add End-of-Day Workflow

### Requirement

Create a daily review workflow.

### Flow

```text
1. Export lifecycle CSV.
2. Export event log.
3. Run Python analyzer.
4. Generate reports.
5. Check open lifecycle records.
6. Print EOD summary.
```

### Checklist

- [ ] Export lifecycle CSV.
- [ ] Export event log.
- [ ] Run Python analyzer.
- [ ] Generate performance report.
- [ ] Generate execution quality report.
- [ ] Generate strategy review report.
- [ ] Check open lifecycle records.
- [ ] Print EOD summary.
- [ ] Store reports under `data/reports/`.

### Acceptance Criteria

- [ ] EOD summary is generated.
- [ ] Open lifecycle records are reported.
- [ ] Analyzer output is stored under `data/reports/`.
- [ ] Workflow can run after backtest, paper trading, or live trading.
