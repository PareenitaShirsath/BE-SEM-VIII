# AAI EXPERIMENT NO. 2  
## Design and Implementation of Bayesian Network for Outcome Prediction in Python

---

## Aim

To design and implement a Bayesian Network using Python for outcome prediction and to perform probabilistic inference based on given evidence.

---

## Theory

### Bayesian Network

A Bayesian Network is a probabilistic graphical model that represents a set of random variables and their conditional dependencies using a Directed Acyclic Graph (DAG). Each node in the graph represents a random variable, and each directed edge represents a causal or conditional dependency between variables.

Bayesian Networks are widely used in decision-making systems, medical diagnosis, risk analysis, and outcome prediction because they can effectively handle uncertainty and probabilistic reasoning.

---

### Structure of a Bayesian Network

A Bayesian Network consists of:

1. **Nodes (Random Variables)**  
   Each node represents a discrete random variable such as Pain, Swelling, Attendance, StudyHours, InternalMarks, or Result.

2. **Edges (Dependencies)**  
   Directed edges represent conditional dependencies between variables.  
   For example:
   - Pain → OrthopedicDisease  
   - Swelling → OrthopedicDisease  
   - OrthopedicDisease → LossOfMovement  
   - Attendance → InternalMarks  
   - StudyHours → InternalMarks  
   - InternalMarks → Result  

3. **Directed Acyclic Graph (DAG)**  
   The network does not contain cycles, ensuring valid probabilistic reasoning.

---

### Joint Probability Distribution

A Bayesian Network represents the joint probability distribution of all variables as a product of conditional probabilities:

**Normal text formula:**

P(X1, X2, ..., Xn) = Π P(Xi | Parents(Xi))

This factorization reduces computational complexity and allows efficient inference.

---

### Conditional Probability Distributions (CPDs)

Each node in the Bayesian Network is associated with a **Conditional Probability Distribution (CPD)**, which defines the probability of a variable given its parent variables.

Examples from the implementation:

- Probability of Pain and Swelling is defined using prior CPDs.
- OrthopedicDisease depends on Pain and Swelling.
- LossOfMovement depends on OrthopedicDisease.
- InternalMarks depends on Attendance and StudyHours.
- Result depends on InternalMarks.

CPDs are represented using **TabularCPD**, which stores probabilities in table format.

---

### Bayesian Inference

Inference in a Bayesian Network involves computing the probability of one or more query variables given observed evidence. In this experiment, inference is performed using the **Variable Elimination** algorithm.

Variable Elimination works by:
1. Selecting variables to eliminate
2. Marginalizing irrelevant variables
3. Computing posterior probabilities efficiently

**Normal text formula:**

P(Query | Evidence) =  
P(Query, Evidence) / P(Evidence)

---

### Outcome Prediction Using Bayesian Network

In this experiment, Bayesian Networks are used for outcome prediction in two scenarios:

1. **Medical Diagnosis Prediction**  
   Given evidence such as Pain and Swelling, the probability of OrthopedicDisease is predicted.

2. **Academic Result Prediction**  
   Given Attendance and StudyHours, the probability of Pass or Fail is predicted.

The outcome is determined by selecting the state with the highest posterior probability.

---

## Conclusion

In this experiment, a Bayesian Network was successfully designed and implemented using Python. The model accurately represented conditional dependencies between variables and performed probabilistic inference using Variable Elimination. The results demonstrate that Bayesian Networks are effective tools for outcome prediction under uncertainty and can be applied to both medical diagnosis and academic performance prediction.

---

