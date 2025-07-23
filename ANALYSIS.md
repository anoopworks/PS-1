---

### Analysis: Credit Score Model for Aave V2 Wallets

#### Introduction
This analysis assesses the unsupervised machine learning model designed to assign credit scores (0–1000) to Aave V2 wallets based on historical transaction behavior. The evaluation leverages a sample dataset of two transactions initially, with successful testing on the full 100K transaction dataset. The model aims to reward responsible behaviors (e.g., deposits, repayments) and penalize risky actions (e.g., liquidations, excessive borrowing), providing a reliable metric for wallet trustworthiness in a DeFi context.

#### Model Performance
The hybrid model, combining Isolation Forest for anomaly detection and K-Means for clustering non-anomalous wallets, performs well with 100K records. Isolation Forest effectively identified anomalies (e.g., frequent liquidations), assigning scores of 0–200, while K-Means grouped normal wallets into five distinct clusters, with scores of 200–1000 based on proximity to the ideal profile. Testing confirms robust clustering and scoring, with visualization (PCA-reduced) showing clear separation of clusters and centroids. The 10% contamination rate and 5-cluster setup proved suitable, though minor tuning could optimize results further.

#### Data Insights
With 100K records, feature engineering (e.g., num_deposits, total_borrow_usd, repayment ratios) captures diverse behaviors, from high depositors to risky borrowers. The ideal profile (max deposits, repayments, min liquidations) serves as a strong benchmark, with clusters closer to it exhibiting higher scores (e.g., 800–1000). Centroids reflect typical cluster behaviors, and the score distribution validates the model’s ability to differentiate reliability, with anomalies well-separated at the lower end (0–200).

#### Conclusion
The model demonstrates strong performance with 100K records, effectively scoring wallets based on behavior. The wallets coming under 0 - 170 (approx.) are considered anomalous and the wallets in range 600 - 1000 are considered non-anamolous (normal).

---
