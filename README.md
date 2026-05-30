# QuantumCreditForge

> **Quantum Credit Risk & Portfolio Optimization Engine** — Enterprise Credit Risk Platform

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**QuantumCreditForge** is a plug-and-play Python toolkit for enterprise credit risk intelligence. It combines quantum-enhanced algorithms with classical financial models to assess PD/LGD/EAD, optimize portfolios, run stress tests, and generate Basel III/IV regulatory reports.
<img width="1914" height="1030" alt="Screenshot 2026-05-30 185049" src="https://github.com/user-attachments/assets/a0764f9e-9d49-4702-84db-a22f05857fab" />

---

## Features

- **5 Quantum Pipelines**
  1. Data-Reuploading VQC — loan feature embedding
  2. VQE Risk Profiling — Ising Hamiltonian ground-state baseline
  3. Density Matrix Entropy — uncertainty quantification
  4. Quantum Kernel Fidelity — overlap with low-risk reference state
  5. QAOA Portfolio Risk — Ising portfolio optimization for capital allocation
- **Classical Models** — Merton structural PD, Vasicek UL, LGD/EAD computation
- **Basel III/IV Calculator** — IRB RWA, CET1/Tier1/CAR, LCR, NSFR compliance
- **Stress Testing** — 9 macro scenarios + combined multi-shock + Monte Carlo VaR/ES
- **Early Warning System** — WATCH/CONCERN/CRITICAL tiers with trend analysis
- **Vintage Analysis** — origination-quarter cohort tracking with delinquency & sub-IG rates
- **Meta-Optimizer** — Bayesian hyperparameter tuning via Optuna
- **AI Consensus Layer** — multi-provider LLM fallback with memory and skill extraction
- **Rich CLI** — colorful terminal dashboards with tables and progress bars
- **CustomTkinter GUI** — dark-themed desktop interface with CSV import

---

## Quick Start

### 1. Clone & Install

```bash
git clone https://github.com/quantumcreditforge/QuantumCreditForge.git
cd QuantumCreditForge
pip install -e .
```

### 2. Run It

```bash
# GUI mode (default)
quantum-credit-forge

# CLI demo (fast, classical)
quantum-credit-forge --cli --classical
<img width="1324" height="859" alt="Screenshot 2026-05-30 185420" src="https://github.com/user-attachments/assets/8b1dc617-8ede-4902-ad93-07b7d378378e" />


# Batch CSV processing
quantum-credit-forge --batch loans.csv --classical

# Programmatically
python -m quantum_credit_forge --demo --classical
```

---

## Installation Options

```bash
# Core (classical mode)
pip install -e .

# With quantum backend (PyQPanda3 GPUQVM)
pip install -e ".[quantum]"

# With GUI
pip install -e ".[gui]"

# With data processing (pandas)
pip install -e ".[data]"

# With meta-optimizer (Optuna)
pip install -e ".[optimize]"

# Everything
pip install -e ".[all]"

# Development
pip install -e ".[dev]"
```

---

## Environment Variables

Optional API keys for the AI consensus layer:

```bash
export NVIDIA_API_KEY="..."
export HF_API_KEY="..."
export XAI_API_KEY="..."
export OPENROUTER_API_KEY="..."
export ANTHROPIC_API_KEY="..."
export GEMINI_API_KEY="..."
export DEEPSEEK_API_KEY="..."

# Optional Telegram notifications
export TELEGRAM_BOT_TOKEN="..."
export TELEGRAM_CHAT_ID="..."
```

> **Never commit API keys.** The app reads them from environment variables only. Copy `.env.example` to `.env` and fill in your keys.

### Force Classical Mode

```bash
# CLI flag
quantum-credit-forge --cli --classical


# Or environment variable
export QCF_CLASSICAL=1
python -m quantum_credit_forge --demo
```
<img width="1324" height="859" alt="Screenshot 2026-05-30 185420" src="https://github.com/user-attachments/assets/6b16a2be-b213-4b47-a96d-67b79b31d3e6" />

---

## Usage Examples

### Python API

```python
from quantum_credit_forge import CreditRiskEngine, generate_demo_portfolio

# Load sample portfolio
portfolio = generate_demo_portfolio()

# Run full assessment
engine = CreditRiskEngine()
result = engine.assess_portfolio(portfolio)

print(f"Portfolio: {result.name}")
print(f"Exposure:  ${result.total_exposure:,.2f}")
print(f"EL:        ${result.total_el:,.2f}")
print(f"UL:        ${result.total_ul:,.2f}")

# Top riskiest loans
for a in sorted(result.assessments, key=lambda x: -x.pd)[:5]:
    print(f"  {a.loan_id}: PD={a.pd:.4f} Rating={a.risk_rating}")
```

### CLI Demo

```bash
python -m quantum_credit_forge --cli --classical
```

Runs a full portfolio analysis with:
- Portfolio summary & loan risk tables
- Rating distribution
- 9 stress scenarios + combined multi-shock
- Monte Carlo VaR/ES (10,000 sims)
- Basel III/IV regulatory capital report
- QAOA portfolio optimization
- Quantum pipeline performance comparison
- AI consensus review
- Early Warning System scan
- Vintage cohort analysis


<img width="1903" height="945" alt="Screenshot 2026-05-30 190852" src="https://github.com/user-attachments/assets/aa1aee7b-b48f-4012-99e8-fa571c96ea97" />


### Batch CSV Import

```bash
python -m quantum_credit_forge --batch loans.csv --classical
```

Expected CSV columns:
- `loan_id`, `credit_score`, `debt_income_ratio`, `annual_income`, `age`
- `employment_years`, `loan_amount`, `loan_term_months`, `collateral_value`
- `payment_history_score`, `delinquency_count`, `num_credit_lines`, `monthly_expenses`
- `sector`, `geography`

---

## Project Structure

```
QuantumCreditForge/
├── src/quantum_credit_forge/
│   ├── __init__.py          # Public API
│   ├── __main__.py          # CLI entry point
│   ├── models.py            # Loan, Assessment, Portfolio, Report dataclasses
│   ├── config.py            # Settings, constants, env vars
│   ├── quantum.py           # 5 quantum pipelines
│   ├── analytics.py         # PD/LGD/EAD, rating, stress scenarios, vintage
│   ├── engine.py            # CreditRiskEngine, Basel, Stress, EWS, MetaOptimizer, Export
│   ├── demo.py              # Sample portfolio generator
│   ├── cli.py               # Rich terminal interface
│   ├── gui.py               # CustomTkinter GUI
│   └── ai/
│       ├── gateway.py       # Multi-provider LLM fallback
│       ├── memory.py        # SQLite-backed skill memory
│       └── consensus.py     # AI review + chatbox
├── examples/
│   ├── cli_demo.py
│   ├── api_example.py
│   └── batch_example.py
├── tests/
│   ├── conftest.py          # Disables quantum backend for fast tests
│   ├── test_models.py
│   ├── test_analytics.py
│   └── test_engine.py
├── config/
│   └── default_config.json
├── pyproject.toml
├── requirements.txt
├── README.md
└── LICENSE
```

---

## Quantum Backend

Quantum pipelines auto-detect **PyQPanda3** and use GPUQVM when available. If PyQPanda3 is not installed, all pipelines gracefully fall back to high-performance classical approximations.

```bash
pip install pyqpanda3>=0.3.2
```

> Requires CUDA 12.8+ and compatible NVIDIA GPU for GPUQVM acceleration.

---

## Testing

```bash
pytest tests/
```

---

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run tests and linting
5. Submit a pull request

---

## License

MIT License — see [LICENSE](LICENSE) for details.

---

## Disclaimer

QuantumCreditForge is a research and analytical toolkit. Credit risk assessments, capital calculations, and regulatory metrics are illustrative and should be validated against professional auditors and regulatory standards before use in financial or compliance decisions.
