# ⚡ cq-trader
### Live Crypto Trading Engine with Exchange Integrations  
Part of the **CryptoQuantAI** Ecosystem

`cq-trader` is a robust, production-ready **live trading engine** designed for algorithmic crypto trading,  
AI trading agents, and automated execution systems.

It integrates perfectly with:
- cq-ohlcv (market data)
- cq-indicators (signals)
- cq-backtester (strategy validation)
- cq-aimodels (ML/AI predictions)
- cq-aiagent (ChatGPT-based trading agents)

---

## 🚀 Features

- ✅ Unified trading API for multiple exchanges  
- ✅ Binance · Bybit · MEXC · OKX · KuCoin (Spot + Futures)  
- ✅ Real-time WebSocket market data  
- ✅ Position tracking (long / short)  
- ✅ Risk management (SL/TP/TSL)  
- ✅ Order types: market, limit, stop, reduce-only  
- ✅ Leverage control  
- ✅ Full logging (JSON + TXT)  
- ✅ Session resume (restart-safe)  
- ✅ Paper trading mode  
- ✅ Plug-and-play Strategy API  

---

## 📦 Installation

```bash
pip install cq-trader
```

---

## 💡 Quick Start

### ✅ Initialize Trader

```python
from cq_trader import Trader

trader = Trader(
    exchange="binance",
    api_key="YOUR_API_KEY",
    api_secret="YOUR_SECRET",
    symbol="BTCUSDT",
    leverage=5
)
```

---

### ✅ Place Trades

```python
trader.buy_market(0.01)
trader.sell_limit(price=45000, amount=0.01)
```

---

### ✅ Manage Positions

```python
pos = trader.get_position()
print(pos)
```

---

### ✅ WebSocket Live Feed

```python
def on_tick(tick):
    print("New tick:", tick)

trader.subscribe_ticker("BTCUSDT", on_tick)
```

---

## ✅ Strategy Execution

```python
from cq_trader import StrategyTrader

class EMACrossTrader(StrategyTrader):
    def generate_signal(self, df):
        fast = df.close.ewm(span=9).mean()
        slow = df.close.ewm(span=21).mean()

        if fast.iloc[-1] > slow.iloc[-1]:
            return "buy"
        return "sell"

bot = EMACrossTrader("BTCUSDT", exchange="binance", leverage=5)
bot.run(interval="5m")
```

---

## 📁 Folder Structure

```
cq-trader/
│
├── cq_trader/
│   ├── __init__.py
│   ├── trader.py
│   ├── websocket.py
│   ├── exchange_router.py
│   ├── strategy_trader.py
│   │
│   ├── exchanges/
│   │   ├── base.py
│   │   ├── binance.py
│   │   ├── bybit.py
│   │   ├── mexc.py
│   │   ├── okx.py
│   │   ├── kucoin.py
│   │
│   └── utils/
│       ├── time.py
│       ├── logger.py
│       ├── formats.py
│
├── tests/
├── examples/
└── README.md
```

---

## 📊 Logging Output

- trade_logs/  
- execution_logs/  
- error_logs/  
- json_logs/  

Every execution and order is timestamped to ensure audit safety.

---

## 📅 Roadmap

- ✅ Cross-exchange portfolio trading  
- ✅ Strategy backtest-to-live continuity  
- ⏳ Smart routing (best price execution)  
- ⏳ Multi-symbol portfolio management  
- ⏳ Grid & DCA built-in strategies  
- ⏳ REST + Web UI Dashboard  

---

## 🤝 Contributing

Guidelines:
- PEP8 + type hints  
- Add tests for new exchanges  
- Keep exchange wrappers simple  
- Contributions welcome  

---

## ⚖️ License

MIT License

---

## 👨‍💻 Maintained By

CryptoQuantAI Development Team
