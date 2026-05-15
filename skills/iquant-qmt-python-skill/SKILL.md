---
name: iquant-qmt-python-skill
description: Complete QMT (迅投极速策略交易系统) Python strategy development skill. Use this skill whenever you work with QMT, iQuant, 迅投, quantitative trading strategy development, backtesting, live trading, passorder, get_market_data_ex, handlebar, subscribe, run_time, or any Python code targeting the QMT/iQuant platform. Covers system overview, three execution mechanisms, backtesting guide, live trading guide, market data API, trading API, best practices, and 4 fully runnable strategy examples.
metadata:
  author: iQuant QMT
  version: "1.0.0"
---

# QMT Python Strategy Development Skill

Complete skill for developing Python strategies on the QMT (迅投极速策略交易系统) platform. Read the reference files below based on what the user needs.

## When to use which reference

| User needs | Read this file |
|---|---|
| QMT basics, system architecture, trading modes | `../../iQuant SKILL/qmt-skill/overview.md` |
| Execution mechanisms (handlebar/subscribe/run_time) | `../../iQuant SKILL/qmt-skill/execution-mechanisms.md` |
| Backtesting a strategy | `../../iQuant SKILL/qmt-skill/backtesting-guide.md` |
| Live trading deployment | `../../iQuant SKILL/qmt-skill/live-trading-guide.md` |
| Market data API functions | `../../iQuant SKILL/qmt-skill/market-data-api.md` |
| Trading/order API functions | `../../iQuant SKILL/qmt-skill/trading-api.md` |
| Coding standards & best practices | `../../iQuant SKILL/qmt-skill/best-practices.md` |
| Full backtest code example | `../../iQuant SKILL/qmt-skill/examples/backtest.md` |
| Full live trading code example | `../../iQuant SKILL/qmt-skill/examples/live-trading.md` |
| Event-driven subscribe example | `../../iQuant SKILL/qmt-skill/examples/subscribe.md` |
| Timer run_time example | `../../iQuant SKILL/qmt-skill/examples/run-time.md` |
| Navigation index | `../../iQuant SKILL/qmt-skill/INDEX.md` |

## Critical QMT Rules

1. **Encoding**: All files MUST start with `#coding:gbk` on the first line
2. **Minimum unit**: 100 shares (1 lot)
3. **Three execution mechanisms**:
   - `handlebar` — K-bar driven (recommended for backtesting), also supports live
   - `subscribe` — Event-driven tick-by-tick (live only), for high-frequency
   - `run_time` — Timer-based (e.g. every minute), for monitoring
4. **quicktrade parameter**: 0 = K-bar mode (wait for bar close), 2 = immediate mode (execute now)
5. **Data access**: `subscribe=False` for backtesting (local data), `subscribe=True` for live (server subscription)

## Quick Code Patterns

### Strategy skeleton
```python
#coding:gbk

def init(C):
    C.stock = C.stockcode + '.' + C.market

def handlebar(C):
    data = C.get_market_data_ex(['close'], [C.stock], count=100, subscribe=False)
    # Strategy logic here
```

### Placing orders
```python
# Buy (order_type=23), immediate mode
passorder(23, 1101, account, '000001.SZ', 14, -1, 100, C)

# Sell (order_type=24), K-bar mode
passorder(24, 1101, account, '000001.SZ', 14, -1, 100, C)
```

### Querying account
```python
account = get_trade_detail_data(account, 'stock', 'account')
positions = get_trade_detail_data(account, 'stock', 'position')
orders = get_trade_detail_data(account, 'stock', 'order')
deals = get_trade_detail_data(account, 'stock', 'deal')
```

## Workflow

1. Determine user's need (backtesting vs live trading vs API query vs code example)
2. Read the appropriate reference file(s) listed above
3. Provide guidance or code based on the reference content
4. Always follow best practices from `best-practices.md` when generating code
5. For complete strategy code, reference the examples directory
