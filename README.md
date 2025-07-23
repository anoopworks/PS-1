# PS-1

Link For the PS-1: https://zerufinance.notion.site/Problem-statement-1-2300a8e4815880bc86b5ddc97b3d8cfd
### Credit Score for Aave V2 Wallet Scoring Model

#### Overview
This document details the scoring logic for an unsupervised machine learning model designed to assign credit scores ranging from 0 to 1000 to wallets interacting with the Aave V2 protocol. The primary objective is to evaluate historical transaction behavior, rewarding responsible actions such as consistent deposits and timely repayments while penalizing risky or exploitative behaviors like frequent liquidations or excessive borrowing without repayment. Given the absence of ground-truth labels, this unsupervised approach infers creditworthiness from transaction patterns, making it suitable for the provided 100K transaction dataset. The model’s design ensures it can scale effectively and provide actionable insights into wallet reliability.

#### Feature Engineering and Anomaly Detection
The scoring process begins with feature engineering, where key metrics such as transaction counts, total deposit and borrow amounts in USD, ratios (e.g., borrow-to-deposit), and temporal spans are extracted and validated for their relevance to DeFi creditworthiness. Isolation Forest is employed to detect anomalous wallets, assuming a 10% contamination rate, with scores ranging from 0 to 200 calculated as `max(0, 200 * (1 + anomaly_score))`. This isolates risky behaviors, supported by the model’s ability to identify outliers without labeled data, ensuring a robust initial filtering step.

#### Clustering and Score Assignment
For non-anomalous wallets, K-Means clustering groups them into five clusters based on standardized features, using Euclidean distance. Scores from 200 to 1000 are assigned based on the distance to an ideal profile—defined by maximum desirable features (e.g., deposits, repayments) and minimum undesirable ones (e.g., liquidations)—using the formula `200 + 800 * (1 - distance / max_distance)`. This linear mapping reflects gradations of creditworthiness, with proximity to the ideal profile driving higher scores. While the hybrid approach (Isolation Forest + K-Means) offers interpretability and scalability, parameters like the anomaly rate and cluster number may need adjustment with the full dataset to optimize performance.
