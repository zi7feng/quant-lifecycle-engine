# Feature 3: Order Book Feature Engine

## PBI E3.3.1: Calculate Microstructure Features

### Features

```text
spread
mid_price
top_1_imbalance
top_5_imbalance
bid_depth_top_n
ask_depth_top_n
microprice
liquidity_pressure
```

### Checklist

- [ ] Calculate spread.
- [ ] Calculate mid price.
- [ ] Calculate top 1 imbalance.
- [ ] Calculate top 5 imbalance.
- [ ] Calculate top N bid depth.
- [ ] Calculate top N ask depth.
- [ ] Calculate microprice.
- [ ] Calculate liquidity pressure.
- [ ] Add unit tests.
- [ ] Export features to analyzer.

### Acceptance Criteria

- [ ] Each feature has unit tests.
- [ ] Feature output can be consumed by Strategy Engine.
- [ ] Feature output can be consumed by Python Analyzer.
- [ ] Missing depth levels are handled safely.
