# credit-risk-scorecard
End to end credit risk application scorecard built on 2.26 million Lending Club loan records using Python, WoE/IV methodology and logistic regression.
**Business Problem**__
Lenders need a reliable, interpretable and regulatorily compliant way to assess the creditworthiness of loan applicants. This scorecard predicts the probability of default and converts it into an intuitive points based score to support approve/decline decisions.

**Source: Lending Club Loan Data (Kaggle)**
Size: 2.26 million loan records
Period: 2007 to 2018
Target Variable: Loan Status — Fully Paid (Good) vs Charged Off (Bad)
Bad Rate: 20%

**Methodology**
**1. Data Preparation**
Defined Good/Bad/Indeterminate population
Removed leakage variables — post default performance data
Handled missing values — median imputation for numerical, mode for categorical
Reduced dataset from 151 variables to 70 after initial cleaning

**2. Variable Selection — Information Value (IV)**
Calculated IV for all variables
Removed variables with IV below 0.02
Removed date columns, free text columns and duplicate variables
Reduced to 44 candidate variables

**3. WoE Binning**
Applied automatic binning using scorecardpy
Reviewed monotonicity of WoE trends for all variables
Removed non monotonic variables
Final variable list reduced to 27 variables

**4. Multicollinearity Check**
Calculated correlation matrix across all numeric variables
Removed pairs with correlation above 0.70
Final model variables — 19

**5. WoE Transformation**
Transformed all variables from raw values to WoE values
Ensures all variables speak the same risk language for logistic regression

**6. Logistic Regression**
Built logistic regression on WoE transformed training data
Checked p-values using statsmodels — all variables significant
Removed variables with incorrect coefficient signs
Final model — 19 variables all with positive coefficients

**7. Scorecard Scaling**
Converted logistic regression coefficients to scorecard points
PDO = 20, Base Score = 600
Score range — 303 to 704

**8. Model Validation**
Validated on out of time test sample (30% holdout)
Gini: 42%
KS: 0.30
AUC: 0.71
PSI: 0.0 — model is stable

**9. Cut Off Selection**
Selected cut off score of 504
Approval rate: 73%
Bad rate at cut off: 13.6%

**Tech Stack**
Python 3.12
pandas — data manipulation
numpy — numerical operations
scorecardpy — WoE/IV and scorecard development
sklearn — logistic regression and train test split
statsmodels — p-value and coefficient analysis
matplotlib — visualisation


**Files**
FileDescriptionlending_club_scorecard.ipynbMain Jupyter notebookscorecard_objects.pklSaved model objectsREADME.mdProject documentation

**Key Learnings**
Real world credit data requires significant cleaning — leakage variables silently inflate model performance
WoE transformation elegantly handles both categorical and numerical variables in a single framework
Monotonicity of WoE bins is critical for scorecard interpretability and regulatory acceptance
A PSI of 0.0 confirms the model generalises well to unseen data


**Author**
**Komal Jaitly**
Credit and Finance Professional transitioning into Quantitative Credit Risk Modelling
www.linkedin.com/in/komal-jaitly05

**Acknowledgements**
Lending Club dataset via Kaggle
