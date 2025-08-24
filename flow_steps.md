# Loading the dataset

# Preliminary analysis:- high level overview

# Data Quality & Cleaning

# Univariate Analysis of features

# Bivariate & Multivariate Analysis

# Feature Engineering: Encoding, Transformation, Missing, Outlier

# Feature Selection

# Model Training

# Prediction

# Evaluation 

🛠️ 1. Data Quality & Cleaning

The goal: Ensure the dataset is accurate, consistent, and usable.

Checklist:

1. Missing Values
* Count missing per feature (df.isnull().sum()).
* Identify patterns (missing completely at random, systematic).

Imputation strategies:

* Numeric → mean, median, KNN-imputer.
* Categorical → mode, "Unknown".
Time series → forward/backward fill.

* If too many missing values (>40%), consider dropping the column.

2. Duplicates
* Remove exact duplicates.
* For near-duplicates, confirm with domain expert before dropping.

3. Inconsistent Entries
* Standardize categorical labels (Male, M, male).
* Normalize text (lowercase, strip whitespace).
* Fix unit inconsistencies (e.g., USD, Rs).

4. Outliers & Noise
* Detect outliers (IQR, Z-score, Isolation Forest).
* Decide whether to cap (winsorization), transform, or drop.
* Validate with domain knowledge (e.g., age > 120 is unrealistic).

5. Data Types & Formats
* Convert object to category where relevant.
* Convert dates into datetime.
* Check numeric columns for incorrect types (e.g., stored as string).

6. Target Variable Check
* Ensure target column has no leakage (future info).
* Check class balance (will affect modeling).

📊 2. Exploratory Data Analysis (EDA)

#### The goal: Understand patterns, relationships, anomalies, and insights.

1. Univariate Analysis
* Plot distributions of numerical features (histogram, KDE, boxplot).
* Compute summary statistics (mean, median, skewness, kurtosis).
- For categorical → value counts, bar plots.
* Identify rare categories (frequency < 1%).

2. Bivariate Analysis (Feature ↔ Target)
* Numerical vs. target → t-test, boxplots, mean differences.
* Categorical vs. target → Chi-square, group bar plots.
* Correlation with target (Pearson, Spearman).

5. Multivariate Analysis (Feature ↔ Feature)
* Correlation heatmap for numeric variables.
* Check multicollinearity (VIF > 10 is a warning).
* Interaction plots for important variables.

4. Class Imbalance
* Target variable distribution (imbalanced? >70/30 split).
* Plan resampling/weighting strategies if needed.

5. Segmentation/Profiling
* Compare customer groups (e.g., Age vs Subscription).
* Cluster-like patterns in data?

🏗️ 3. Feature Engineering

The goal: Create useful, meaningful, and machine-readable features.

1. Encoding Categorical Variables
* Binary features → Label Encoding (0/1).
* Nominal categories → One-hot encoding.
* High cardinality (>20 unique categories) → Target encoding / Hash encoding.

2. Scaling/Transformations
* StandardScaler (mean=0, std=1) for linear models.
* MinMaxScaler (0–1) for neural nets or distance-based methods.
* Log transform for skewed distributions.

3. Handling Outliers
* Apply capping (e.g., values above 99th percentile).
* Winsorization or transformation (log/sqrt).

4. Date & Time Features
* Extract year, month, day, weekday, hour.
* Time since last event (recency).
* Rolling averages/trends if temporal.
* Domain-Driven Features (very important in real-world DS)
* Ratios (income-to-expense, clicks-to-impressions).
* Aggregates (average transaction value, engagement score).
* Flags (e.g., "is_high_income").

5. Interaction Features
* Combine two features (Age × Income).
* Polynomial features if non-linear patterns exist.

6. Missing Indicator Features
* Add a binary flag: "was_missing" → sometimes missingness is informative.

🎯 4. Feature Selection

The goal: Keep only the most relevant features and reduce noise.

Checklist:

Filter Methods (statistical tests)

Pearson correlation for numeric.

Chi-square test for categorical vs target.

ANOVA F-test for continuous vs categorical target.

Remove highly correlated features (|corr| > 0.9).

Wrapper Methods

Recursive Feature Elimination (RFE).

Forward/Backward selection.

Embedded Methods

Lasso Regression (L1 penalty → drives some coefficients to 0).

Tree-based models (Random Forest, XGBoost feature importance).

Dimensionality Reduction

PCA/UMAP/T-SNE if features are highly correlated and high-dimensional.

Keep enough components to explain 90–95% variance.

Business Validation

Don’t just trust stats — check if features make business sense.

Drop features that cause leakage (e.g., “days_since_subscription_start”).