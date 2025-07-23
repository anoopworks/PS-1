Certainly! Here's the same content, now structured with **clear section titles** for each paragraph:

---

### Project Overview

This project develops a credit scoring model for wallets interacting with the Aave V2 protocol, assigning scores between 0 and 1000. The aim is to assess wallet behavior based on on-chain activity, rewarding responsible financial actions and penalizing risky behavior. Since labeled creditworthiness data is unavailable, we use an unsupervised machine learning approach combining Isolation Forest for anomaly detection and K-Means clustering for score assignment.

### Feature Engineering

The process starts with feature engineering, extracting metrics that reflect financial behavior. These include the number and volume of deposits and repayments, borrowing activity, repayment-to-borrow ratios, liquidation frequency, number of unique assets used, and active time span. These features form the behavioral fingerprint of each wallet.

### Anomaly Detection

Anomaly detection is performed using Isolation Forest, which identifies the most unusual 10% of wallets. These wallets are considered high-risk and are assigned low credit scores in the range of 0 to 200, scaled based on their anomaly severity.

### Clustering and Score Assignment

The remaining non-anomalous wallets are clustered using K-Means into five behavioral groups. A synthetic "ideal profile" is created by maximizing desirable behaviors (like high repayments and long activity span) and minimizing undesirable ones (like high liquidation count). Each wallet’s similarity to this ideal profile is measured using standardized distance, and scores are assigned using a non-linear exponential decay function. This approach rewards wallets that are closer to the ideal with higher scores in the range of 200 to 1000.

### Conclusion

This hybrid scoring model offers a robust, data-driven way to evaluate DeFi wallets based solely on on-chain activity. By blending anomaly detection and clustering with behavior-based profiling, it enables fair and scalable credit assessment
