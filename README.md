# QuantShield 

**AI-Powered Portfolio Risk Intelligence System**

QuantShield transforms traditional portfolio analytics into a decision intelligence platform. It combines real-time risk monitoring, explainable analytics, forward-looking risk modeling, and scenario simulation to answer not just *what* your risk is, but *why* it's changing, *what* happens next, and *what to do about it*.

> This project is built for educational, research, and portfolio risk analysis purposes. It does not provide financial advice, investment recommendations, or trading signals.

---

## Table of Contents

- [Problem Statement](#problem-statement)
- [System Architecture](#system-architecture)
- [Intelligence Pipeline](#intelligence-pipeline)
- [Data Flow](#data-flow)
- [Risk Intelligence Framework](#risk-intelligence-framework)
- [Key Features](#key-features)
- [ML Architecture](#ml-architecture)
- [Data Infrastructure](#data-infrastructure)
- [Portfolio Input](#portfolio-input)
- [Dashboard Components](#dashboard-components)
- [Roadmap](#roadmap)

---

## Problem Statement

Most portfolio analytics platforms answer one question:

> *What is my current risk?*

QuantShield answers four:

| Question | QuantShield Capability |
|---|---|
| What is my risk? | Real-time VaR, Volatility, Sharpe & Beta monitoring |
| Why is it changing? | Correlation spike detection & root-cause attribution |
| What happens next? | 30-day risk transition probability via Markov + ML |
| What should I do? | Diversification recommendations with impact estimates |

---

## System Architecture

<!-- Add your architecture diagram below -->
<!-- Upload the image to /assets/ in your repo and update the src -->

![System Architecture](./assets/architecture-diagram.png)
*QuantShield 4-layer architecture: Monitoring → Intelligence → Forward Insight → Decision Support*

The platform is structured across four layers, each building on the previous:

```
┌─────────────────────────────────────────────────────────┐
│  Layer 4 — Decision Support                             │
│  Actionable recommendations · Scenario simulation       │
├─────────────────────────────────────────────────────────┤
│  Layer 3 — Forward Insight                              │
│  Risk forecasting · Regime transition prediction        │
├─────────────────────────────────────────────────────────┤
│  Layer 2 — Intelligence                                 │
│  Root-cause analysis · Risk drift detection             │
├─────────────────────────────────────────────────────────┤
│  Layer 1 — Monitoring                                   │
│  VaR · Volatility · Sharpe · Beta · Drawdown            │
└─────────────────────────────────────────────────────────┘
```

### Layer Breakdown

**Layer 1 — Monitoring**
Computes standard portfolio risk metrics in real time: portfolio volatility, Value at Risk (VaR), maximum drawdown, Sharpe ratio, Sortino ratio, Beta, concentration risk, and sector exposure.

**Layer 2 — Intelligence**
Explains *why* risk is changing. Detects risk drift (gradual regime transitions), hidden risks (correlation spikes, diversification breakdown), and generates a risk drift signature that attributes changes to specific causes.

**Layer 3 — Forward Insight**
Uses Hidden Markov Models and gradient boosting to estimate future risk regime transitions. Outputs 30-day transition probabilities and drawdown likelihood estimates.

**Layer 4 — Decision Support**
Converts forward-looking risk signals into actionable recommendations. Runs scenario simulations (market crash, sector shocks, rate changes) and generates diversification suggestions with quantified impact estimates.

---

## Intelligence Pipeline

<!-- Add your intelligence pipeline diagram below -->
<!-- Upload the image to /assets/ in your repo and update the src -->

![Intelligence Pipeline](./assets/intelligence-pipeline.png)
*From raw market data to natural-language risk narrative*

The pipeline processes raw financial data through feature engineering, risk classification, and an AI agent layer to produce human-readable insights:

```
Market Data
    │
    ▼
Feature Engineering
(returns, volatility, correlations, drawdowns)
    │
    ├──────────────────────────┐
    ▼                          ▼
Risk Classification      Regime Detection
(RF · XGBoost · LGBM)   (HMM · GB · Sequences)
    │                          │
    └────────────┬─────────────┘
                 ▼
        Root-Cause Attribution
                 │
                 ▼
      LangChain / LangGraph Agents
      ┌──────────────────────────┐
      │  Analytics Interpreter   │  ← reads and contextualizes metrics
      │  Correlation Analyst     │  ← identifies hidden risk linkages
      │  Risk Narrator           │  ← writes plain-English summaries
      └──────────────────────────┘
                 │
                 ▼
         Risk Narrative + Recommendations
```

---

## Data Flow

<!-- Add your data flow diagram below -->
<!-- Upload the image to /assets/ in your repo and update the src -->

![Data Flow](./assets/dataflow.png)
*Multi-source ingestion pipeline feeding the risk engine and AI agents*

```
┌─────────────────────────────────────┐
│           Data Sources              │
│                                     │
│  Polygon   — historical + realtime  │
│  Finnhub   — news + streaming       │
│  Groww API — NSE/BSE data           │
│  FMP       — fundamentals + macro   │
└────────────────┬────────────────────┘
                 │
                 ▼
         Feature Store
     (OHLCV · Returns · Correlations
      Drawdowns · Volatility · Sector)
                 │
        ┌────────┴────────┐
        ▼                 ▼
    ML Models         Risk Engine
  (Classification,   (Metric Computation,
   Regime, Drawdown)  Drift Detection)
        │                 │
        └────────┬────────┘
                 ▼
            AI Agents
       (LangChain / LangGraph)
                 │
                 ▼
            Dashboard
```

---

## Risk Intelligence Framework

<!-- Add your risk intelligence framework diagram below -->
<!-- Upload the image to /assets/ in your repo and update the src -->

![Risk Intelligence Framework](./assets/risk-intelligence-framework.png)
*How QuantShield connects raw risk signals to investor decisions*

The framework is built around three core concepts:

**1. Risk Signal Detection**
Raw metrics (volatility, correlations, drawdowns) are continuously monitored. Anomalies — sudden correlation spikes, concentration increases, or volatility regime shifts — trigger the intelligence layer.

**2. Causal Attribution**
Detected signals are attributed to root causes. A risk increase is explained as driven by, for example, rising correlations rather than individual asset volatility, giving investors a clear picture of what is actually happening.

**3. Decision Translation**
Attributed causes are translated into forward-looking probabilities and concrete recommendations with estimated impact, closing the loop from signal to action.

---

## Key Features

### Risk Monitoring

Continuous computation of standard portfolio risk metrics:

- Portfolio Volatility
- Value at Risk (VaR)
- Maximum Drawdown
- Sharpe Ratio and Sortino Ratio
- Beta
- Concentration Risk
- Sector Exposure

### Risk Intelligence

**Risk Drift Detection** — identifies gradual transitions between risk regimes before they become critical:

```
Week 1 → Medium Risk
Week 2 → Medium+
Week 3 → High Risk  ← alert triggered
```

**Hidden Risk Detection** — surfaces non-obvious risks:
- Diversification breakdown
- Correlation spikes between assets
- Sector concentration buildup
- Single-asset overexposure

**Risk Drift Signature** — attributes risk changes to specific drivers:
> Risk increase is primarily driven by rising asset correlations rather than individual volatility.

### Risk Narrative Engine

Converts raw metrics into plain-language summaries:

Instead of:
```
Volatility = 18%
VaR = -3%
Beta = 1.4
```

Generates:
> Portfolio risk is elevated. Volatility has increased over the past two weeks, asset correlations are converging, and drawdown depth is worsening. The portfolio is showing signs of transitioning into a high-risk regime.

### Forward-Looking Risk Modeling

- **Risk transition prediction** — probability of moving between Low / Medium / High risk states over the next 30 days
- **Drawdown probability** — estimated likelihood of experiencing a drawdown exceeding a specified threshold
- **Volatility regime detection** — identifies transitions between stable and unstable volatility environments

### Decision Support

Recommendations are generated based on diversification analysis, correlation structure, and concentration risk:

> Banking sector exposure is elevated at 32% of portfolio weight. Reducing allocation by 15% is estimated to lower drawdown risk by approximately 20% under current correlation conditions.

### Scenario Simulation

| Scenario | Input | Portfolio Impact |
|---|---|---|
| Market Crash | Market −10% | Portfolio −18% |
| Sector Shock | IT Sector −20% | Portfolio Risk +25% |
| Interest Rate Hike | Rates +1% | Portfolio Volatility +12% |

---

## ML Architecture

QuantShield models predict **portfolio risk behavior**, not stock prices, returns, or buy/sell signals.

| Objective | Models | Output |
|---|---|---|
| Risk Classification | Random Forest, XGBoost, LightGBM | `Low / Medium / High` label |
| Regime Transition | Hidden Markov Models, Gradient Boosting | Transition probability matrix |
| Drawdown Probability | Sequence Models | P(drawdown > threshold) over N days |
| Volatility Regime | Unsupervised clustering | `Stable / Unstable` label |

**Feature categories used:**
- Rolling returns and volatility at multiple windows
- Pairwise asset correlations and correlation trend
- Drawdown depth and duration
- Sector weights and concentration metrics
- Macro indicators (rates, index levels) from FMP

---

## Data Infrastructure

QuantShield is built on live financial market data across four providers:

| Provider | Role |
|---|---|
| **Polygon** | Historical OHLCV data, real-time market data, core analytics backbone |
| **Finnhub** | News data, streaming backup feed |
| **Groww API** | NSE/BSE market data, holdings integration, portfolio exposure |
| **FMP** | Company fundamentals, sector classification, macroeconomic data, explainability layer |

---

## Portfolio Input

**CSV Upload**

```csv
Ticker,Weight
RELIANCE.NS,20
TCS.NS,15
INFY.NS,10
HDFCBANK.NS,25
WIPRO.NS,30
```

**Manual Portfolio Builder**
Users can construct portfolios directly in the UI by specifying ticker symbols and allocation weights.

**Validation**
The system validates portfolio weights (must sum to 100), ticker availability across providers, duplicate holdings, and missing values before running any analysis.

---

## Dashboard Components

| Component | Description |
|---|---|
| Risk Gauge | Visual classification of current portfolio risk state |
| Portfolio Allocation | Breakdown of weights by asset and sector |
| Correlation Heatmap | Asset correlation matrix with trend overlay |
| Advanced Analytics | Full risk metric panel with historical comparison |
| AI Summary Panel | Natural-language interpretation of current risk state |

---

## Roadmap

- [ ] Enhanced regime detection models with longer historical context
- [ ] Advanced scenario library (geopolitical events, earnings shocks)
- [ ] Multi-portfolio monitoring and comparison
- [ ] AI Risk Copilot (conversational portfolio Q&A)
- [ ] Portfolio optimization suggestions
- [ ] Interactive risk education modules
- [ ] Institutional-grade risk reporting exports

---

## Tech Stack

| Layer | Technologies |
|---|---|
| Frontend | React, Tailwind CSS, shadcn/ui |
| Backend | FastAPI, WebSockets |
| Database | PostgreSQL |
| ML | scikit-learn, XGBoost, LightGBM, statsmodels |
| AI Agents | LangChain, LangGraph |
| Data | Polygon, Finnhub, Groww API, Financial Modeling Prep |

---

## Disclaimer

This project is intended for **educational, research, and portfolio risk analysis** purposes only.

QuantShield does not predict stock prices, provide investment advice, or generate trading signals. All risk metrics and forward-looking estimates are statistical outputs subject to model uncertainty and should not be used as the sole basis for any financial decision.

---
