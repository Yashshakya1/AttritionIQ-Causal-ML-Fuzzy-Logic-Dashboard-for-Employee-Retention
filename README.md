# 🧠 AttritionIQ — Causal ML & Fuzzy Logic Dashboard for Employee Retention

[![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)](https://python.org)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.43+-red?style=flat-square&logo=streamlit)](https://streamlit.io)
[![DoWhy](https://img.shields.io/badge/DoWhy-0.14-green?style=flat-square)](https://py-why.github.io/dowhy)
[![EconML](https://img.shields.io/badge/EconML-0.16-orange?style=flat-square)](https://econml.azurewebsites.net)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)

> An end-to-end AI-powered HR analytics platform combining **Causal Machine Learning** and **Fuzzy Logic** to predict and explain employee attrition risk — with a beautiful interactive dashboard.

---

## 📸 Demo

![Dashboard Preview](assets/dashboard_preview.png)

**Live Demo:** [attritioniq.onrender.com](https://attritioniq.onrender.com)

---

## ✨ Features

- 🎯 **Fuzzy Logic Engine** — 5-variable, 7-rule fuzzy inference system for attrition risk scoring
- 🔗 **Causal ML with DoWhy** — Backdoor identification + refutation tests (placebo, random cause)
- 🌲 **EconML CausalForestDML** — Individual heterogeneous treatment effects (Uber vs Lyft pricing)
- 📊 **Interactive Dashboard** — Real-time risk gauge, radar chart, distribution plot, sensitivity analysis
- 🔄 **Batch Employee Analysis** — Compare multiple employee profiles simultaneously
- 🚀 **REST API** — Flask backend for programmatic risk predictions

---

## 🏗️ Project Structure

```
attritioniq/
│
├── attrition_dashboard.py   # Streamlit frontend dashboard
├── app.py                   # Flask REST API
├── causal_ml_improved.ipynb # Full analysis notebook
├── requirements.txt         # Python dependencies
├── README.md
│
└── assets/
    └── dashboard_preview.png
```

---

## 🧩 Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | Streamlit + Plotly |
| **Fuzzy Logic** | scikit-fuzzy |
| **Causal ML** | DoWhy 0.14 + EconML 0.16 |
| **ML Models** | RandomForestRegressor, LinearDML, CausalForestDML |
| **API** | Flask + Gunicorn |
| **Dataset** | Rideshare Kaggle + IBM HR Analytics |
| **Deployment** | Render |

---

## 🚀 Quick Start

### 1. Clone the repo
```bash
git clone https://github.com/yourusername/attritioniq.git
cd attritioniq
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the dashboard
```bash
streamlit run attrition_dashboard.py
```

### 4. Run the Flask API (optional)
```bash
python app.py
```

Dashboard opens at **http://localhost:8501**
API runs at **http://localhost:5000**

---

## 🔌 API Usage

### Predict attrition risk
```bash
POST /predict
Content-Type: application/json

{
  "overtime": 8,
  "worklife": 3,
  "satisfaction": 2,
  "salary": 4,
  "years": 2
}
```

**Response:**
```json
{
  "risk_score": 8.4,
  "risk_level": "High"
}
```

---

## 🧠 How It Works

### Part 1 — Causal ML (Rideshare Pricing)

```
Treatment:  surge_multiplier
Outcome:    price
Confounders: distance, temperature, hour, cab_type, service_name

DoWhy Result:    Causal Effect = 21.73
EconML (LinearDML ATE): 22.07
Refutation Tests: ✅ Passed (Placebo ≈ 0.002)
```

**Pipeline:**
1. Load & preprocess rideshare dataset (693K rows)
2. Define causal DAG with confounders
3. Identify effect via backdoor criterion
4. Estimate with Linear Regression + CausalForestDML
5. Validate with refutation tests

### Part 2 — Fuzzy Logic (Employee Attrition)

**Input Variables:**
| Variable | Range | Description |
|---|---|---|
| `overtime` | 0–1 | Overtime hours indicator |
| `worklife` | 0–10 | Work-life balance score |
| `satisfaction` | 0–10 | Job satisfaction score |
| `salary_level` | 0–10 | Compensation level |
| `years_at_company` | 0–20 | Tenure in years |

**Rules (7 total):**
```
IF overtime=HIGH AND worklife=POOR  → risk=HIGH
IF satisfaction=LOW                 → risk=HIGH
IF worklife=GOOD AND satisfaction=HIGH → risk=LOW
IF salary=LOW AND satisfaction=MEDIUM  → risk=HIGH
IF salary=HIGH AND satisfaction=HIGH   → risk=LOW
IF years=NEW AND worklife=POOR      → risk=HIGH
IF years=VETERAN AND worklife=MEDIUM → risk=LOW
```

---

## 📊 Dashboard Sections

| Section | Description |
|---|---|
| **Risk Score Card** | Live score (0–10) with confidence interval |
| **Risk Factor Breakdown** | Per-factor contribution bars |
| **Risk Gauge** | Animated speedometer chart |
| **Distribution Plot** | Employee vs workforce population |
| **Profile Radar** | Multi-axis comparison with avg employee |
| **Sensitivity Analysis** | How each factor impacts final risk |
| **Causal Effect Panel** | DoWhy results + refutation test status |

---

## ☁️ Deploy on Render

### Flask API Service
| Setting | Value |
|---|---|
| Build Command | `pip install -r requirements.txt` |
| Start Command | `gunicorn app:app` |

### Streamlit Dashboard Service
| Setting | Value |
|---|---|
| Build Command | `pip install -r requirements.txt` |
| Start Command | `streamlit run attrition_dashboard.py --server.port $PORT --server.address 0.0.0.0` |

---

## 📦 Requirements

```txt
streamlit
plotly
numpy
flask
gunicorn
requests
dowhy==0.14
econml==0.16.0
scikit-fuzzy
scikit-learn
pandas
matplotlib
seaborn
graphviz
```

---

## 📁 Notebook

The full analysis notebook `causal_ml_improved.ipynb` contains:

- ✅ EDA with 3 visualization plots
- ✅ Causal graph construction
- ✅ DoWhy effect identification & estimation
- ✅ Refutation tests (2 types)
- ✅ LinearDML with confidence intervals
- ✅ CausalForestDML heterogeneous effects
- ✅ Uber vs Lyft causal effect comparison
- ✅ Fuzzy logic system (5 variables, 7 rules)
- ✅ Batch employee risk analysis

All changes are documented inline with `# [CHANGE]` comments explaining **what** was changed and **why**.

---

## 🤝 Contributing

Pull requests welcome! For major changes, open an issue first.

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

## 👤 Author

**Yash Shakya**
- GitHub: [@yourusername](https://github.com/yourusername)
- LinkedIn: [linkedin.com/in/yourprofile](https://linkedin.com/in/yourprofile)

---

<div align="center">
  <sub>Built with ❤️ using DoWhy, EconML, scikit-fuzzy, and Streamlit</sub>
</div>
