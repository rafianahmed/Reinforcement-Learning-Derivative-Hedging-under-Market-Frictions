# Reinforcement Learning Derivative Hedging

A quantitative finance project that applies reinforcement learning to dynamic option hedging. The project trains an RL agent to hedge a short option position while minimizing both hedging error and transaction costs.

The RL hedge is compared against a classical Black-Scholes delta hedge across multiple volatility regimes.

---

# Overview

Traditional delta hedging assumes continuous trading, frictionless markets, and perfect model assumptions. In reality:

- Markets are discrete
- Transaction costs matter
- Volatility changes over time
- Continuous rebalancing is impossible

This project explores whether reinforcement learning can learn more efficient hedging strategies under realistic market conditions.

---

# Objective

Train a reinforcement learning agent to dynamically hedge a short option position.

The agent learns to:

- Reduce portfolio risk
- Minimize hedging variance
- Reduce transaction costs
- Adapt to changing volatility regimes

---

# Core Workflow

```text
Simulated Stock Paths
        ↓
Short Option Portfolio
        ↓
RL Agent Observes Market State
        ↓
Agent Chooses Hedge Ratio
        ↓
Portfolio P&L Computed
        ↓
Reward Function Applied
        ↓
Agent Learns Optimal Hedging Policy
```

---

# Financial Setup

Initial portfolio:

```text
Short 1 European Call Option
```

Hedging instrument:

```text
Underlying Stock
```

The agent dynamically adjusts stock hedge ratios over time.

---

# Reinforcement Learning Framework

The project uses reinforcement learning to solve a sequential hedging problem.

## State Space

The RL agent observes:

```text
Current stock price
Option delta
Time to maturity
Current volatility
Current hedge position
Portfolio P&L
```

---

## Action Space

The agent chooses:

```text
How many shares to hold
```

Examples:

```text
-1.0   → fully short stock
 0.0   → neutral
+0.5   → partial hedge
+1.0   → fully long stock
```

---

## Reward Function

The reward penalizes:

- Large hedging losses
- High portfolio variance
- Excessive transaction costs

Example reward:

```python
reward = (
    - pnl_variance
    - transaction_cost_penalty
)
```

This encourages smoother and cheaper hedging strategies.

---

# Baseline Comparison

The RL hedge is compared against:

```text
Black-Scholes Delta Hedging
```

Metrics compared:

- Hedging error
- P&L variance
- Tail risk
- Transaction costs
- Sharpe ratio
- Maximum drawdown

---

# Volatility Regimes

The project evaluates hedging performance under multiple environments:

| Regime | Volatility |
|---|---|
| Low Volatility | 10% |
| Medium Volatility | 20% |
| High Volatility | 40% |
| Stochastic Volatility | Dynamic |

This tests whether RL adapts better than static delta hedging.

---

# Technologies Used

```text
Python
PyTorch
Stable-Baselines3
Gymnasium
NumPy
Pandas
Matplotlib
SciPy
```

---

# RL Algorithms

The project supports:

```text
DQN
PPO
SAC
```

Recommended starting point:

```text
PPO (Proximal Policy Optimization)
```

because it is stable and performs well in continuous-control problems.

---

# Project Structure

```text
rl-derivative-hedging/
│
├── README.md
├── requirements.txt
├── train.py
├── evaluate.py
│
├── src/
│   └── rl_hedging/
│       ├── __init__.py
│       ├── environment.py
│       ├── black_scholes.py
│       ├── portfolio.py
│       ├── rewards.py
│       ├── agent.py
│       ├── simulation.py
│       ├── backtest.py
│       └── plotting.py
│
├── notebooks/
│   └── experiments.ipynb
│
├── reports/
│   ├── figures/
│   └── results/
│
└── tests/
    ├── test_environment.py
    ├── test_rewards.py
    └── test_black_scholes.py
```

---

# Installation

Clone repository:

```bash
git clone https://github.com/YOUR_USERNAME/rl-derivative-hedging.git
cd rl-derivative-hedging
```

Create virtual environment:

```bash
python -m venv venv
```

Activate environment:

## Windows

```bash
venv\Scripts\activate
```

## Mac/Linux

```bash
source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# Running the Project

Train RL agent:

```bash
python train.py
```

Evaluate hedging performance:

```bash
python evaluate.py
```

Run notebook experiments:

```bash
jupyter notebook
```

---

# Example Environment

Example Gym-style environment:

```python
state = [
    stock_price,
    option_delta,
    volatility,
    time_to_maturity,
    current_position
]
```

Action:

```python
action = hedge_ratio
```

Reward:

```python
reward = (
    - portfolio_variance
    - transaction_costs
)
```

---

# Example Results

| Strategy | Hedging Error | Transaction Costs |
|---|---|---|
| Delta Hedge | 0.024 | High |
| PPO RL Hedge | 0.018 | Medium |
| SAC RL Hedge | 0.016 | Low |

---

# Research Foundation

This project is based on major research in reinforcement learning and quantitative finance.

---

## 1. Deep Hedging

Buehler, Hans, Lukas Gonon, Josef Teichmann, and Ben Wood.

**Deep Hedging**  
Quantitative Finance, 2019

Paper:  
https://arxiv.org/abs/1802.03042

This paper introduced the deep hedging framework for learning hedging strategies with neural networks under realistic market frictions.

---

## 2. Dynamic Replication and Hedging

Kolm, Petter N., and Gordon Ritter.

**Dynamic Replication and Hedging: A Reinforcement Learning Approach**  
Journal of Financial Data Science, 2019

Paper:  
https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3281235

This paper provides one of the clearest practical formulations of RL-based hedging problems.

---

## 3. Deep Hedging Reference Implementation

GitHub:  
https://github.com/hansbuehler/deephedging

Reference implementation from the authors of the Deep Hedging paper.

---

## 4. FinRL

GitHub:  
https://github.com/AI4Finance-Foundation/FinRL

Used as inspiration for RL environment structure and finance-oriented reinforcement learning workflows.

---

# Skills Demonstrated

This project demonstrates:

- Reinforcement Learning
- Quantitative Finance
- Dynamic Hedging
- Option Pricing
- Deep Learning
- Sequential Decision Making
- Financial Simulation
- Risk Management
- Backtesting
- Python ML Engineering

---

# Future Improvements

Potential extensions:

- Multi-option portfolios
- Gamma/Vega hedging
- Heston stochastic volatility
- Transaction-cost calibration
- Market impact modeling
- Continuous-action SAC agents
- Distributional RL
- Real option market data

---

# Why This Project Matters

Derivative hedging is a sequential decision-making problem under uncertainty, making it a natural application for reinforcement learning.

This project demonstrates how modern RL methods can potentially improve upon classical hedging frameworks when realistic trading frictions are introduced.

---

# Disclaimer

This project is for educational and research purposes only.

It is not financial advice and should not be used for live trading without extensive additional validation.

---
