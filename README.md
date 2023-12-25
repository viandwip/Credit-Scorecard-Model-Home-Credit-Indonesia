# Credit Scorecard Model Using Machine Learning

## 1. Goals & Objectives
Minimize the number of clients who are approved but actually defaulters and create predictive model to determine potential client and default client.

## 2. Exploratory Data Analysis
<p align="center"><img src="images/Ratio of Default Client.png" alt="Ratio of Default Client" width = 40%></p>

### 2.1. Univariate Analysis
#### 2.1.1. Categorical Data
<p align="center"><img src="images/Univariate Analysis - Categorical Data.png" alt="Univariate Analysis - Categorical Data"></p>

#### Observation:
- The ratio of default clients who **own a house or car** is **not much different** from clients who **do not own a house or car**.
- Cash loans have a **slightly higher** default ratio compared to Revolving loans.
- Clients who own a house **less likely** to become default clients.
- The highest ratio of default clients comes from NAME_FAMILY_STATUS **Civil marriage** and the lowest comes from **Widow**.
- Clients who are accompanied by **family or partner** when applying for the loan are **less likely** to become default clients.
- The highest ratio of default clients comes from **Maternity leave** and **Unemployed** clients and the lowest comes from **Businessman**.
- The **higher** the education, the **less likely** to become the default clients.
- The highest ratio of default clients comes from clients working as **Low-skill Laborers** and the lowest comes from **Accountants**.

#### 2.1.2. Numerical Data
<p align="center"><img src="images/Univariate Analysis - Numerical Data.png" alt="Univariate Analysis - Numerical Data"></p>

#### Observation:
- The **older** the clients, the **less likely** to become default clients. 
- The **more family members and children**, the **more likely**, to become the default clients.

### 2.2. Bivariate Analysis
<p align="center"><img src="images/Bivariate Analysis.png" alt="Bivariate Analysis"></p>

#### Observation:
- AMT_ANNUITY have **strong positive** correlation with AMT_CREDIT.
- AMT_INCOME_TOTAL also have **positive** correlation with AMT_ANNUITY and AMT_CREDIT although **not very strong**.

## 3. Data Preprocessing
- Feature selection using **Predictive Power Score**.
- Remove features that have **more than 30%** missing values and impute the null values with ****mean** value for the **EXT_SOURCE_3** column and **mode** value for the **NAME_TYPE_SUITE** column.
- Remove duplicated data.
- Encode the features with **Label Encoding** if they have 2 unique values or ordinal data and with **OHE** if they have nominal data.
- Split the data into 70:30 proportions, **70% for training** and **30% for testing**.
- Handle the outliers using **IQR method**.
- Handle class imbalance using **oversampling method - SMOTE**.
- Conduct **standardization** process for the features used in the training and testing data.

## 4. Modeling
### 4.1. Model Training & Validation
| No | Model | Acc (Train) | Acc (Test) | Δ Acc | Time Elapsed |
| :- | :- | :- | :- | :- | :- |
| 1	| Logistic Regression |	0.84935	| 0.87699	| 0.02764	| 2.153283 |
| 2	| Random Forest	| 0.99776	| 0.85236	| -0.14540 | 82.075135 |
| 3	| ExtraTrees | 0.99781 | 0.84879 | -0.14902 |	53.402744 |
| 4	| GradientBoost |	0.85507 |	0.83701 |	-0.01806 | 42.769334 |
| 5	| Decision Tree	| 0.99781	| 0.82371	| -0.17410	| 2.938740 |
| 6 |	AdaBoost	| 0.84746	| 0.80384	| -0.04362	| 15.819693 |

### 4.2. Hyperparameter Tuning
| No | Model | Acc (Train) | Acc (Test) | Δ Acc | Time Elapsed |
| :- | :- | :- | :- | :- | :- |
| 1	| Logistic Regression	| 0.84939	| 0.87734	| 0.02795	| 169.779793 |
| 2	| ExtraTrees	| 0.95340	| 0.87382	| -0.07958	| 417.120225 |
| 3	| Random Forest	| 0.96629	| 0.86977	| -0.09652	| 865.018647 |
| 4	| GradientBoost	| 0.86552	| 0.85087	| -0.01465	| 1245.015871 |
| 5	| Decision Tree	| 0.91870	| 0.82055	| -0.09815	| 15.366524 |
| 6	| AdaBoost	| 0.84746	| 0.80384	| -0.04362	| 1248.123892 |

#### Observation:
Based on the **hyperparameter tuning** results, we will choose **Logistic Regression** as the model because it has **the highest accuracy** on the test data.

### 4.3. Feature Importances
<p align="center"><img src="images/Feature Importances (Coefficient).png" alt="Feature Importances (Coefficient)" width=70%></p>

### 4.4. Confusion Matrix
<p align="center"><img src="images/Confusion Matrix.png" alt="Confusion Matrix" width = 70%></p>

By using the results of *hyperparameter tuning* for the Logistic Regression model, we train the model again to get a **confusion matrix** as shown above, with the following results:

- **True Positive**: Predicted the loan was approved and it turned out to be correct 1,190 times.
- **True Negative**: Predicted the loan was not approved and it turned out to be correct 77,543 times.
- **False Positive**: Predicted the loan was approved and turned out to be wrong by 4,839 times.
- **False Negative**: Predicted the loan was not approved and turned out to be wrong 6,167 times.

## 5. Business Recommendation
- The **top 3 features** to predict the default clients are **NAME_FAMILY_STATUS**, **NAME_HOUSING_TYPE** and **NAME_TYPE_SUITE**.
- Focus on clients aged **40 years** and over, **widow** or **separated**, who live in **apartments**, are **accompanied by another person** when applying for the loan and have **high education** or an **academic degree** because most of them **do not have problems** when repaying the loan.
- Be careful with clients who are young or **under 40 years** old, **single** or **married**, still live with their **parents**, are **unaccompanied** when applying for the loan, and have **low education** because most of them **have problems** when repaying the loan.
