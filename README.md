# Segmentation - Part 1 (Clustering)
Analysis of Bank Transactions

## 1. Data Observing
- Loaded the datasets and observed initial structures.
- Identified outliers in the `data` dataset.  
- Transformed the `sum` column to `abs_sum` (absolute values) for precise calculations.
- Plotted a boxplot using IQR calculations to visualize outliers.
- Retained outliers to preserve the essence of clustering.

---

## 2. Data Cleaning
### 2.1 Missing Values
- Verified that there were no missing values in the dataset.

### 2.2 Drop Duplicates
- Identified 19 duplicate records and removed them.

### 2.3 Data with Invalid Code/Type Values
#### 2.3.1 Removing invalid rows (code/type not in reference tables)
- Deleted rows where code/type values were not found in respective tables.

#### 2.3.2 Removing invalid descriptions (code/type)
- Removed rows with invalid descriptions in the reference tables.

#### 2.3.3 Resolving duplicates in type descriptions
- Removed duplicate descriptions from the `types` table and replaced invalid entries.

#### 2.3.4 Final Cleanup
- Removed duplicates and invalid rows from the `types` table.

### 2.4 Creation of a Cleaned Dataset
- Created a new version of the `data` dataset without invalid information and duplicates.

---

## 3. Exploratory Data Analysis (EDA)
- Conducted initial analysis to detect anomalies and patterns.
- Detected an outlier on day 195 with a significant transaction (~70 million).
- Analyzed time-of-day transaction distributions, suggesting subscriptions (e.g., Spotify, Netflix).

---

## 4. Feature Engineering
Produced new features to improve clustering accuracy:
### 4.1 Absolute Sum of Transactions (`abs_sum`)
- Created absolute values for transaction sums.

### 4.2 Number of Transactions (`n_transactions`)
- Calculated transaction counts for each client.

### 4.3 Average Transaction (`average_transaction`)
- Computed the average transaction amount per client.

### 4.4 Gender (`gender`)
- Merged gender data with the main dataset.

### 4.5 Percentage of Total Transactions (`percentage`)
- Determined each client's contribution to total transactions.

### 4.6 Cluster Descriptions
#### 4.6.1 Preprocessing Text Descriptions
- Tokenized text and performed TF-IDF vectorization for clustering.

#### 4.6.2 KMeans Clustering for Descriptions
- Implemented clustering to group transaction codes/types.

### 4.7 Registration and Transaction Timing
- Extracted registration time in minutes and calculated transaction frequencies.

### 4.8 RFM Analysis
- Derived `Recency`, `Frequency`, and `Monetary` features to rank clients.

---

## 5. Data Preprocessing
### 5.1 Quantile Transformer
- Applied a non-linear transformation to map data to a uniform distribution.

### 5.2 Normalization
- Normalized features for consistent scaling.

### 5.3 Preprocessing Conclusion
- Selected Quantile Transformer and Normalizer for best clustering results, as they are robust to outliers.

---

## 6. RFM Analysis
### 6.1 Feature Scoring
- Calculated scores for recency, frequency, and monetary values.

### 6.2 Customer Segmentation
- Ranked customers using aggregated RFM scores (range: `3-12`).
- Classified customers based on descriptive RFM scores (`111` to `444`).

### 6.3 Targeted Strategies
- Identified "golden" customers for rewards.
- Targeted "lost" customers for re-engagement.

---

## 7. Model Selection
Implemented KMeans and Agglomerative Clustering:
### 7.1 KMeans Clustering
#### 7.1.1 Optimal Cluster Count
- Chose 14 clusters based on SSE, Silhouette Coefficient, and other metrics.

#### 7.1.2 Cross-Validation
- Achieved a low cross-validation score, indicating effective preprocessing.

#### 7.1.3 Visualization
- Used TSNE to visualize cluster separation.

### 7.2 Agglomerative Clustering
#### 7.2.1 Model Creation
- Used "ward" linkage for hierarchical clustering.

#### 7.2.2 Metric Evaluation
- Confirmed optimal clustering using Silhouette, Calinski-Harabasz, and Davies-Bouldin metrics.

#### 7.2.3 Comparison with KMeans
- Results aligned 99% with KMeans clusters.

---

## 8. Outcomes
### Best Customers
- Clusters `13`, `9`, and `3`: High transaction volumes and balances, mostly male.

### Big Spenders
- Clusters `7` and `5`: Fewer transactions but large transaction values.

### Average Customers
- Clusters `1`, `11`, `4`, and `2`: Moderate activity and recent registrations.

### Almost Lost Customers
- Clusters `6`, `12`, `0`, `8`, and `10`: Low activity; require re-engagement strategies.

---

## Visualizations and Further Details
- Visualizations include time-based transaction distributions, outlier detections, and TSNE projections.
- Final segmentation ensures actionable insights for targeted marketing and client retention strategies.
