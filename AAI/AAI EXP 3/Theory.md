## Theory

### Gaussian Mixture Model (GMM)

A Gaussian Mixture Model (GMM) is a probabilistic machine learning model used to represent complex data distributions as a combination of multiple Gaussian (normal) distributions. Instead of assuming that all data points belong to a single distribution, GMM assumes that the data is generated from a mixture of several Gaussian components, each representing a latent cluster in the dataset.

GMM is widely used in pattern recognition and medical data analysis because it can model uncertainty, overlapping classes, and multimodal data distributions.

Mathematically, a GMM is defined as:

\[
P(x) = \sum_{k=1}^{K} \pi_k \mathcal{N}(x \mid \mu_k, \Sigma_k)
\]

where:
- \(K\) is the number of Gaussian components  
- \(\pi_k\) is the mixing coefficient of the k-th Gaussian  
- \(\mu_k\) is the mean vector  
- \(\Sigma_k\) is the covariance matrix  

---

### Likelihood of a Data Point

The likelihood represents how well a Gaussian mixture model explains a given data point. For a data point \(x_n\), the likelihood under a GMM is given by:

\[
P(x_n) = \sum_{k=1}^{K} \pi_k \mathcal{N}(x_n \mid \mu_k, \Sigma_k)
\]

In the implemented system, the likelihood of each test sample is computed using the trained GMM models. During prediction, the log-likelihood of the sample is calculated for each class-specific GMM, and the class with the highest likelihood value is selected as the predicted outcome.

This likelihood-based comparison forms the core decision rule of the implemented model.

---

### Posterior Probability (Cluster Responsibility)

The posterior probability, also known as cluster responsibility, represents the probability that a data point belongs to a particular Gaussian component. It is defined as:

\[
P(z_n = k \mid x_n) =
\frac{\pi_k \mathcal{N}(x_n \mid \mu_k, \Sigma_k)}
{\sum_{k=1}^{K} \pi_k \mathcal{N}(x_n \mid \mu_k, \Sigma_k)}
\]

In the implementation, these posterior probabilities are computed internally during the training phase by the Gaussian Mixture Model using the Expectation-Maximization algorithm. Although they are not explicitly calculated in the code, they are essential for parameter estimation and model convergence.

---

### Expectation-Maximization (EM) Algorithm

Gaussian Mixture Models are trained using the Expectation-Maximization (EM) algorithm, an iterative optimization technique used to estimate model parameters.

- **E-step (Expectation):** Computes the posterior probabilities (responsibilities) of each Gaussian component for every data point.
- **M-step (Maximization):** Updates the parameters of the model, including the means \(\mu_k\), covariance matrices \(\Sigma_k\), and mixing coefficients \(\pi_k\), to maximize the likelihood of the data.

These steps are repeated until the log-likelihood converges. In the implemented code, the EM algorithm is executed internally through the `GaussianMixture.fit()` method.

---

### Log-Likelihood Optimization and Prediction

The objective of the EM algorithm is to maximize the log-likelihood of the observed data, defined as:

\[
\log L = \sum_{n=1}^{N} \log \left( \sum_{k=1}^{K} \pi_k \mathcal{N}(x_n \mid \mu_k, \Sigma_k) \right)
\]

In this experiment, log-likelihood values are used directly during the prediction phase. For each test sample, the log-likelihood is computed using `score_samples()` for all class-specific GMMs. The class that produces the maximum log-likelihood value is selected as the final prediction.

This approach ensures stable numerical computation and accurate probabilistic classification.

---

