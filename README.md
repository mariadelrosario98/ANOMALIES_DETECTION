## 📌 Problem Description: Anomaly Detection in Credit Card Transactions

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

---
## 📌 Objective

**The goal is to evaluate both approaches and understand their effectiveness in accurately flagging fraudulent transactions while minimizing false alarms.
**---

## 🚀 Models

### 🔹 Isolation Forest (Unsupervised)

- Learns to isolate observations in the feature space
- Flags observations that are "easier to isolate" as anomalies
- Does **not** use the `Class` label for training

### 🔸 Random Forest (Supervised)

- Uses historical labels to learn patterns of fraud
- Standard classification algorithm with high interpretability

---

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
