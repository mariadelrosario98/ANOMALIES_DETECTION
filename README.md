## 🕵️ Problem Description: Anomaly Detection in Credit Card Transactions

In the domain of financial services, one of the most critical challenges is the detection of fraudulent credit card transactions. Fraudulent transactions represent a small fraction of all operations, yet they can lead to significant financial losses and security breaches.

This task is framed as an anomaly detection problem, where:

- The vast majority of transactions are legitimate (normal behavior)

- A very small subset are fraudulent (anomalies)

Key **challenges** in this setting include:

- Extreme class imbalance: Fraudulent transactions are often less than 0.2% of the data
- Lack of clear patterns: Fraud behaviors evolve and may not follow consistent trends
- High stakes: Both false positives and false negatives can be costly
False positives: Inconvenience users, block valid transactions
False negatives: Let fraud slip through undetected

To address this, we explore both:

1. Unsupervised methods like Isolation Forest, which identify anomalies without using labels

2. Supervised methods like Random Forest, which leverage labeled historical data to learn patterns of fraud

## 📌 Objective
The goal is to evaluate both approaches and understand their effectiveness in accurately flagging fraudulent transactions while minimizing false alarms.

## 🚀 Models

### 🕵️‍♂️ Isolation Forest (Unsupervised Learning)

**Isolation Forest** is designed for **anomaly detection**. Instead of profiling normal data, it isolates anomalies based on the idea that they are **easier to separate** from the rest of the data.

#### 🔍 How it works:
1. Builds an ensemble of **isolation trees**, where:
   - Each tree splits data randomly on a selected feature and split value.
2. Anomalies are expected to be **isolated in fewer splits** (shorter path lengths).
3. The **average path length** across trees is used to calculate an **anomaly score**.

#### ⚙️ Key Parameters:
| Parameter              | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| `n_estimators`         | Number of isolation trees to build                                          |
| `max_samples`          | Number of samples to draw from the dataset to train each tree               |
| `contamination`        | Expected proportion of outliers (used to define the decision threshold)     |
| `max_features`         | Number of features to draw when training each tree                          |
| `bootstrap`            | Whether to bootstrap samples when building trees                            |
| `random_state`         | Controls randomness and reproducibility                                     |

---

**🌳 Random Forest** is an ensemble classification and regression algorithm that builds multiple decision trees and combines their outputs to improve accuracy and reduce overfitting.

#### 🔍 How it works:
1. Creates multiple decision trees using **bootstrapped subsets** of the training data.
2. At each node, selects a **random subset of features** to split on.
3. **Aggregates predictions** (majority vote for classification, average for regression).

#### ⚙️ Key Parameters:
| Parameter              | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| `n_estimators`         | Number of trees in the forest                                               |
| `max_depth`            | Maximum depth of each tree                                                  |
| `max_features`         | Number of features to consider when looking for the best split              |
| `min_samples_split`    | Minimum number of samples required to split a node                          |
| `min_samples_leaf`     | Minimum number of samples required to be at a leaf node                     |
| `class_weight`         | How to handle class imbalance (e.g., `'balanced'`)                          |
| `random_state`         | Controls reproducibility of results                                         |


## 📊 Results
### ✅ Confusion Matrix: Isolation Forest

|                | Predicted: 0 | Predicted: 1 | Notes              |
|----------------|--------------|--------------|---------------------|
| **Actual: 0**  | 270,491      | 13,824       | False positives ⚠️  |
| **Actual: 1**  | 75           | 417          | True positives ✅    |

**True Negatives (TN):** 270,491

**False Positives (FP):** 13,824

**False Negatives (FN):** 75

**True Positives (TP):** 417

### ✅ Confusion Matrix: Random Forest

|                | Predicted: 0 | Predicted: 1 | Notes                       |
|----------------|--------------|--------------|------------------------------|
| **Actual: 0**  | 56,860       | 4            | Very few false positives ✅  |
| **Actual: 1**  | 19           | 79           | Detects most frauds ✅       |


**True Negatives (TN):** 56,860

**False Positives (FP):** 4

**False Negatives (FN):** 19

**True Positives (TP):** 79

## 📊 2. Metric Comparison

| **Metric**          | **Isolation Forest**                        | **Random Forest**                    |
|---------------------|---------------------------------------------|--------------------------------------
| **Accuracy**        | Good (but misleading due to imbalance)      | Very high                            
| **Precision**       | 417 / (417 + 13824) ≈ **2.9%**              | 79 / (79 + 4) ≈ **95.2%** ✅          
| **Recall**          | 417 / (417 + 75) ≈ **84.7%** ✅             | 79 / (79 + 19) ≈ **80.6%** ✅         
| **False Positives** | Very high (**13,824**) ⚠️                   | Very low (**4**) ✅                   
| **False Negatives** | Low (**75**) ✅                             | Lower (**19**) ✅                     
| **Type**            | Unsupervised                                | Supervised                           

---

## ✅ Conclusion
- **Random Forest** significantly outperforms Isolation Forest in this case, thanks to access to labeled data.
- It achieves **high precision and recall**, making it ideal for production fraud detection pipelines.
- **Isolation Forest**, while unsupervised, still manages to catch most anomalies and is a valuable tool when labels are unavailable.

---
