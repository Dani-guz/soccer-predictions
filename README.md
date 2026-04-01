# ⚽ Soccer Predictions

Machine learning project to estimate match outcome probabilities 
in La Liga (Spanish football), with focus on FC Barcelona.

## 🎯 Objective

Predict the probability of Home Win, Draw, and Away Win for each 
match using historical data, and evaluate against professional 
bookmaker benchmarks (Bet365).

## 📊 Key Results

| Model | Test Accuracy | Test Log Loss | Barcelona Accuracy |
|-------|:------------:|:------------:|:-----------------:|
| Always predict Home Win | 44.1% | 1.074 | — |
| Random Forest Classifier | 52.2% | 1.015 | 57.9% |
| **Poisson Model (best)** | **52.8%** | **1.007** | **76.3%** |
| Bet365 (benchmark) | 54.6% | 0.953 | — |

## 🔬 Approach

The project follows an iterative methodology across 6 notebooks:

1. **Data Collection & EDA** — 5 seasons of La Liga from football-data.co.uk
2. **Feature Engineering** — Rolling stats, league standings simulation, 
 differential features (all with strict temporal anti-leakage)
3. **Baseline Models** — Naive baselines + Logistic Regression
4. **Advanced Models** — Random Forest, XGBoost (diagnosed overfitting)
5. **Multi-League Experiment** — Added 4 European leagues (~9,500 matches)
6. **Poisson Model** — Predict expected goals → derive probabilities 
 via Poisson distribution

## 🏗️ Project Structure

SOCCER-PREDICTIONS/
├── data/
│   ├── raw data/
│   │   ├── la_liga_raw_2020_2025.csv
│   │   └── multi_league_raw_2020_2025.csv
│   └── processed/
│       ├── la_liga_clean_2020_2025.csv
│       ├── la_liga_features_2020_2025.csv
│       └── multi_league_features_2020_2025.csv
│
├── notebooks/
│   ├── 01_Cleaning_&_EDA.ipynb
│   ├── 02_Feature_Engineering.ipynb
│   ├── 03_Modeling_Baseline.ipynb
│   ├── 04_Advanced_Models.ipynb
│   ├── 05_Multi_League_Data.ipynb
│   └── 06_Poisson_Model.ipynb
│
├── models/                  ← Guardar modelos entrenados
│   └── (te doy el código abajo)
│
│
├── references/              ← Fuentes y contexto
│   └── references.md
│
├── reports/                 ← Resumen ejecutivo del proyecto
│   ├── final_report.md
│   └── figures/             ← Gráficos clave exportados
│
├── LICENSE
├── README.md               
└── requirements.txt

## ⚙️ Setup

# Clone the repository
git clone https://github.com/Dani-guz/soccer-predictions.git
cd soccer-predictions

# Create virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # Linux/Mac
# venv\Scripts\activate   # Windows

# Install dependencies
pip install -r requirements.txt

# Run notebooks in order
jupyter notebook notebooks/01_Cleaning_&_EDA.ipynb
📈 Key Learnings
Feature engineering matters more than model complexity for tabular data
Temporal validation is critical — random splits cause data leakage
More data isn't always better — relevance > quantity
Poisson modeling naturally handles draws and produces interpretable outputs
XGBoost overfits with small datasets (~1,100 training samples)
Professional benchmarks (bookmakers) are extremely hard to beat
📝 Data Source
football-data.co.uk — Free historical football data including match results, basic statistics, and betting odds.

🛠️ Tech Stack
Python | pandas | scikit-learn | XGBoost | SciPy | matplotlib | seaborn

📄 License
MIT License — see LICENSE for details.
