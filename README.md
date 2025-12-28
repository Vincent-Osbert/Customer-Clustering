# Customer Segmentation Analysis: Credit Card Behavioral Patterns

## Project Overview
This project utilizes **Unsupervised Machine Learning** to analyze the usage behavior of **8,950 active credit card holders**. The primary objective is to identify distinct customer archetypes to facilitate **differentiated marketing strategies** and **risk management optimization**.

## Key Insights & Data Interpretation
The analysis of raw financial data revealed critical behavioral patterns which directly dictated the technical preprocessing strategy.

### 1. Financial Disparity & Distribution Skewness
*   **Observation:** The dataset exhibited **extreme right-skewness** in key metrics such as `BALANCE` and `PURCHASES`. While the median balance was relatively low, the maximum values extended significantly higher.
*   **Insight:** The customer base contains a minority of **High-Net-Worth Individuals** whose financial footprint vastly outweighs the average user.
*   **Technical Response:** To prevent these extreme values from biasing the model, **Winsorization (Capping)** was applied at the 95th percentile, followed by **Logarithmic Transformation** to normalize the distribution.

### 2. Behavioral Duality (Transactors vs. Revolvers)
*   **Observation:** Correlation analysis indicated a **negative or weak correlation** between `PURCHASES` (retail transactions) and `CASH_ADVANCE` (ATM withdrawals).
*   **Insight:** Customers tend to exhibit mutually exclusive behaviors: they either use the card as a **payment tool** (Transactors) or as a **liquidity source** (Revolvers).
*   **Technical Response:** This distinct separation justified the use of **K-Means Clustering**, which effectively groups data points based on Euclidean distance similarities.

### 3. Tenure Stability
*   **Observation:** The vast majority of users possess a **tenure of 12 months**.
*   **Insight:** The dataset reflects a **mature and stable customer base**, making the resulting clusters reliable for long-term retention strategies rather than acquisition modeling.

## Cluster Profiles (Output)
The modeling process resulted in the identification of **two primary customer segments**:

### Cluster 0: The Cash-Advance User (Revolvers)
*   **Behavior:** Characterized by **high balance maintenance** and **frequent cash advances**, but **minimal retail purchases**.
*   **Risk Profile:** Higher credit risk due to revolving debt.
*   **Strategic Action:** Suitable for **low-interest balance transfer offers** or **installment loan products**.

### Cluster 1: The Retail Spender (Transactors)
*   **Behavior:** Characterized by **high purchase frequency** (both one-off and installments) and **low revolving balance**.
*   **Risk Profile:** Lower credit risk; financially disciplined.
*   **Strategic Action:** Suitable for **reward programs**, **cashback offers**, and **merchant partnerships** to stimulate transaction volume.

## Technical Methodology
The code implementation follows a rigorous workflow designed to address the data characteristics mentioned above:

1.  **Data Sanitization**
    *   **Median Imputation:** Applied to `CREDIT_LIMIT` and `MINIMUM_PAYMENTS` to handle missing values without being influenced by outliers.
    *   **Noise Reduction:** Removal of non-predictive features (e.g., Customer ID).

2.  **Feature Engineering**
    *   Creation of relative metrics such as **Monthly Average Purchase** and **Credit Limit Usage Ratio** to provide scale-independent behavioral indicators.

3.  **Advanced Preprocessing**
    *   **Log Transformation:** Implemented to unskew distributions and satisfy the normality assumption of many statistical methods.
    *   **Standardization (Z-Score):** Utilized **StandardScaler** to ensure all features contribute equally to the distance calculations, preventing variables with large magnitudes (like Credit Limit) from dominating the model.

4.  **Dimensionality Reduction**
    *   **PCA (Principal Component Analysis):** Reduced dataset dimensions to **2 Principal Components** to allow for 2D visualization and verification of cluster separation.

5.  **Model Optimization**
    *   **Elbow Method & Silhouette Score:** Used to mathematically determine the optimal number of clusters ($k$).

## Technologies Used
*   **Python**
*   **Pandas & NumPy** (Data Manipulation)
*   **Scikit-Learn** (K-Means, PCA, Preprocessing)
*   **Matplotlib & Seaborn** (Data Visualization)
