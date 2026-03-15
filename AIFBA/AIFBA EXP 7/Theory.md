# EXPERIMENT 7  
## Fraud Detection using Machine Learning Algorithms

## Theory

Fraud detection leverages **Machine Learning (ML) algorithms** to identify anomalous transactions in financial systems. Fraudulent activities often exhibit distinct patterns that ML models can recognize, making machine learning a powerful tool for detecting fraud.

---

## 1. Data Preprocessing

### Feature Engineering
Extract important variables from transaction data such as:

- Transaction time  
- Transaction amount  
- Transaction location  
- Transaction frequency  

These features help the model identify unusual transaction behavior.

### Handling Imbalanced Data

Fraud datasets usually contain very few fraud cases compared to normal transactions. Therefore, balancing techniques are used.

**SMOTE (Synthetic Minority Over-sampling Technique)**  
Generates synthetic samples of the minority class (fraud cases) to balance the dataset.

**Undersampling**  
Reduces the number of majority class samples (non-fraud cases) to balance the dataset.

---

## 2. Supervised Learning Models

**Logistic Regression**  
A simple baseline model used for binary classification of fraud vs non-fraud transactions.

**Decision Trees and Random Forest**  
Tree-based models that help identify important features influencing fraud detection.

**Gradient Boosting (XGBoost, LightGBM)**  
Advanced boosting algorithms that provide high accuracy, especially for imbalanced datasets.

**Neural Networks (Deep Learning)**  
Uses multiple layers to capture complex patterns and relationships in fraudulent transactions.

---

## 3. Unsupervised Learning for Anomaly Detection

**Isolation Forest**  
Detects anomalies by isolating rare observations that behave differently from normal data.

**Autoencoders (Deep Learning)**  
Neural networks that learn normal transaction behavior and identify unusual transactions as anomalies.

---

## 4. Model Evaluation Metrics

**Precision and Recall**  
These metrics focus on minimizing false negatives to ensure fraudulent transactions are not missed.

**AUC-ROC Score**  
Measures how well the model distinguishes between fraudulent and non-fraudulent transactions.

---

## 5. Real-Time Fraud Detection

**API Deployment (Flask, FastAPI)**  
The trained model can be deployed as an API to enable instant fraud detection in financial systems.

**Streaming Frameworks (Kafka, Spark)**  
Used for real-time processing of large volumes of transaction data.

---

## Conclusion

Thus, we have learned how **Fraud Detection using Machine Learning Algorithms** can effectively identify fraudulent transactions by using supervised and unsupervised learning techniques along with proper data preprocessing and evaluation metrics.
