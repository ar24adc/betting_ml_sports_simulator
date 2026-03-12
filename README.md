# ML-Based Sports Betting Prediction Analysis

## Project Overview
A machine learning-based sports betting prediction framework that integrates outcome prediction, probability calibration, and value-based decision-making using historical sports data from Football, Tennis, and Cricket.

**MSc Data Science Individual Project Module (7PAM2002-0901-2025)**  
**University of Hertfordshire | Department of Physics, Astronomy and Mathematics**

## Author
- **Student**: Ravi Ajay Kumar  
- **Student ID**: 446474413  
- **Supervisor**: Ashley Spindler  
- **Submission Date**: 13 January 2026

---

## Research Aim
To develop and evaluate a machine learning–based sports betting framework that integrates outcome prediction, probability calibration, and value-based decision criteria using historical sports data.


---

## Dataset Sources

### Football
- **Source**: [football-data.co.uk](http://football-data.co.uk)
- **Period**: 2021-2024 seasons
- **Format**: CSV files containing match outcomes, team statistics, and bookmaker odds
- **Key Features**: FTHG (Full Time Home Goals), FTAG (Full Time Away Goals), FTR (Full Time Result)

### Tennis
- **Source**: [Jeff Sackmann's ATP Tennis GitHub Repository](http://github.com/JeffSackmann/tennis_atp)
- **Period**: 2021-2024 seasons (real data), 2025 (synthetic - 100 matches)
- **Match Counts**: 2,733 (2021), 2,917 (2022), 2,986 (2023), 3,076 (2024)
- **Key Features**: Player rankings, winner/loser statistics, surface type

### Cricket
- **Source**: [Cricsheet.org](http://cricsheet.org)
- **Period**: 2021-2025 (synthetic data - 100 matches per year)
- **Format**: YAML match files processed to CSV
- **Note**: Real data download failed during execution; synthetic data used for pipeline demonstration
- **License**: Creative Commons Attribution 4.0 International (CC BY 4.0)

---

## Machine Learning Models

### Primary Models
- **Random Forest Classifier/Regressor**: Ensemble learning with bootstrap aggregation to reduce overfitting
- **XGBoost**: Gradient boosting with iterative loss minimization for high-dimensional data
- **LightGBM**: Efficient gradient boosting for large-scale datasets

### Ensemble Approach
- **Soft Voting Ensemble** with weights: RF=1, XGBoost=2, LightGBM=2
- **Probability Calibration**: Isotonic regression via `CalibratedClassifierCV` (cv=5)

### Hyperparameter Optimization
- **Method**: Bayesian optimization using Optuna
- **Trials**: 20 trials per model for efficient parameter space exploration

---

## Features

### Data Processing
- Date standardization and missing value handling
- Categorical variable encoding (team/player names)
- Sport-specific feature engineering
- Train/test split: 80/20 with stratified 5-fold cross-validation

### Model Training
- Fixed random seed for reproducibility
- Stratified K-fold cross-validation (k=5) for balanced class distribution
- Hold-out validation to prevent data leakage

### Betting Simulation
- **Confidence Threshold**: 60% minimum predicted probability
- **Expected Value (EV) Calculation**: EV = (p × odds) – 1
- **Starting Bankroll**: $10,000
- **Stake Strategy**: Fixed-unit stakes
- **Performance Tracking**: Win/loss ratio, ROI, bankroll evolution

---


## Installation

### Requirements
```bash
python >= 3.8
pandas
numpy
scikit-learn
matplotlib
seaborn
xgboost
lightgbm
optuna
pyyaml
requests
```

### Install Dependencies
```bash
pip install pandas numpy scikit-learn matplotlib seaborn xgboost lightgbm optuna pyyaml requests
```

---

## Usage


### Jupyter Notebook Analysis
```python
# Open the analysis notebook
jupyter notebook sports_betting_analysis.ipynb
```

---

## Project Structure
```
betting_ml_sports_simulator/
├── data/
│   ├── football/           # Football CSV files
│   ├── tennis/             # Tennis ATP match data
│   └── cricket/            # Cricket YAML/CSV files
├── betting_system.ipynb
├── reports/
└── README.md
```

---

## Evaluation Metrics

### Classification Metrics
- **Accuracy**: Overall prediction correctness
- **F1 Score**: Harmonic mean of precision and recall (handles class imbalance)
- **Log Loss**: Probabilistic measure of prediction quality
- **Brier Score**: Calibration quality assessment

### Financial Metrics
- **Expected Value (EV)**: (predicted_probability × bookmaker_odds) – 1
- **Return on Investment (ROI)**: (Final Bankroll – Initial Bankroll) / Initial Bankroll × 100%
- **Win Rate**: Percentage of profitable bets
- **Bankroll Growth**: Tracking capital over time

---

## Key Findings

### Strengths
1. Successfully identified sport-specific feature importance (home advantage in football, rankings in tennis, run-scoring in cricket)
2. Generated calibrated probabilistic predictions across all sports
3. Demonstrated modular architecture applicable to multiple sports
4. Proved ability to identify betting opportunities using EV analysis

### Limitations Identified
1. **Target Leakage**: Football (HomeGoals/AwayGoals) and Tennis (Upset feature) contained post-match data
2. **Market Efficiency**: Bookmaker margins and efficient odds limited profitability despite high accuracy
3. **Data Constraints**: Missing real-time contextual factors (injuries, weather, tactical changes)
4. **Fixed Stakes**: Did not account for confidence levels or risk tolerance
5. **Limited Temporal Coverage**: Two-season review may miss long-term trends

### Conclusion
High predictive accuracy (97-100%) does not guarantee profitable betting outcomes. The consistent net losses across all three sports confirm that accurate predictions are insufficient against efficient betting markets with built-in bookmaker margins. This aligns with established literature (Bunker & Susnjak, 2022; Walsh & Joshi, 2023; Knoll & Stübinger, 2020).

-
### Responsible Gambling Statement
All betting simulations were conducted **offline using historical data only**. No real currency, active markets, or encouragement of gambling behavior was involved. This project presents ML prediction frameworks for academic research purposes, not as gambling recommendations. The system's net losses are clearly documented to avoid encouraging irresponsible wagering.

---


## License
This project is submitted as part of the **MSc Data Science Individual Project Module (7PAM2002-0901-2025)** at the University of Hertfordshire.

For academic and research purposes only.

---

## Acknowledgements
- **University of Hertfordshire** - School of Physics, Engineering and Computer Science
- **Project Supervisor**: Ashley Spindler
- **Data Sources**: football-data.co.uk, Jeff Sackmann (tennis_atp), Cricsheet.org
- **MSc Data Science Programme** - Academic Year 2025-26

---

## Contact
For questions or academic discussions about this project:
- **University Email**: ar24adc@herts.ac.uk

---

## Disclaimer
This research project is for **educational and academic purposes only**. It does not constitute financial advice, gambling recommendations, or encouragement to participate in sports betting. The documented net losses demonstrate the challenges of profitable betting against efficient markets. Always gamble responsibly and within legal frameworks.

