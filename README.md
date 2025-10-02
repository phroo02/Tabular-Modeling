# 🏆 Kaggle Tabular Data Competition – My Solution (Top 3% Finish)



This repository documents my full workflow for a Kaggle **tabular data competition**, where I achieved a **Top 3% leaderboard ranking** (Public LB score: 0.2309).  
The project represents my most sophisticated work so far, covering **data preprocessing, exploratory analysis, feature engineering, boosting models, neural networks, stacked ensembling, and interpretability**.  

📖 This project was inspired by and developed as part of my study of *Deep Learning for Coders with fastai & PyTorch* by Jeremy Howard and Sylvain Gugger, which emphasizes reproducible, competitive workflows and interpretability in machine learning.  

---

## 📌 Path I Took

This README is structured as a **narrative** of the steps I took, with visualizations at each stage to explain the decisions and techniques I used.

---

## 🔍 1. Exploratory Data Analysis (EDA)

I started with **distribution analysis** of the categorical and numeric features. For example, the `ProductSize` variable showed strong class imbalance, while `YearMade` revealed historical patterns in the dataset.

<img src="./images/output6.png" width="400"/>  
<img src="./images/output7.png" width="400"/>  

- Identified missing values in categorical features like `ProductSize`.  
- Observed skewed year distribution, requiring binning and transformations.  

---

## 🛠 2. Feature Correlation & Redundancy Check

To avoid redundant features, I used **hierarchical clustering** and correlation plots to understand dependencies between features.

<img src="./images/output5.png" width="500"/>  

This step helped identify collinear features and guided feature selection for models like linear/logistic regressors, which are sensitive to multicollinearity.

---

## 🧩 3. Feature Importance (Baseline Models)

Next, I trained early LightGBM/XGBoost models to check **feature importance**.

<img src="./images/output4.png" width="500"/>  

Key findings:
- `YearMade`, `ProductSize`, and `Coupler_System` were the strongest predictors.  
- Some IDs (`MachineID`, `ModelID`) carried signal due to being proxies for hidden categorical structures.  

---

## 🔬 4. Partial Dependence & Interpretability

To further understand how the most important features affected predictions, I plotted **Partial Dependence Plots (PDPs)**.

<img src="./images/output8.png" width="600"/>  

Additionally, I generated **SHAP-style explanations** to understand feature contributions at the instance level.

<img src="./images/output9.png" width="500"/>  

---

## ⚙️ 5. Feature Engineering

Based on the insights:
- Created ratios (`rooms_per_household`, `bedrooms_per_room`, etc. for analog variables).  
- Engineered domain-driven transformations like **log-scaling** skewed numeric variables.  
- Encoded categorical variables with **OneHotEncoding** and **CatBoost encoding**.  
- Applied **binning** for features with skewed distributions.  

---

## 🤖 6. Model Training

I benchmarked several models:

- **Gradient Boosting**:  
  - LightGBM (best single model)  
  - XGBoost  
  - CatBoost  

- **Neural Network**:  
  - Simple dense net with BatchNorm + Dropout  
  - Tuned learning rate schedules  

Learning rate finder example:

<img src="./images/output10.png" width="400"/>  

Training curves:

<img src="./images/output3.png" width="400"/>  

---

## 🧬 7. Ensembling & Stacking

The biggest performance gain came from **stacked ensembling**:
- First layer: LightGBM, XGBoost, CatBoost, Neural Net.  
- Meta-model: Logistic Regression / LightGBM.  
- Final submission: weighted blending of top learners.  

This reduced variance and improved generalization.  

---

## 📊 8. Final Feature Importance (Stacked Model)

After stacking, I re-evaluated feature importances:

<img src="./images/output.png" width="500"/>  

- `YearMade` and `ProductSize` consistently dominated across all boosting models.  
- Cross-validation confirmed their predictive stability.  

---

## 🏅 9. Results

- **Leaderboard Rank**: Top 3%  
- **Public Score**: 0.2309  
- **Insight**: Stacked ensembles outperformed single learners by a clear margin.  
- **Interpretability**: Used PDPs, SHAP, and feature importances to explain models.  

---

## 🧰 Tech Stack

- **Languages**: Python  
- **Libraries**: Pandas, NumPy, scikit-learn, XGBoost, LightGBM, CatBoost, PyTorch, Matplotlib, Seaborn  
- **Tools**: Jupyter Notebook, Git/GitHub  

---

## 🙏 Credits
Special thanks to Jeremy Howard and Sylvain Gugger, authors of Deep Learning for Coders with fastai & PyTorch.
Their book heavily influenced my approach to designing reproducible ML pipelines, competitive modeling strategies, and interpretability workflows.
