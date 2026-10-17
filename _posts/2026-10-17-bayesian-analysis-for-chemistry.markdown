---
layout: post
title:  "Bayesian Analysis for Chemistry"
date:   2026-10-17 21:42:31 +0800
categories: jekyll update
---
## From Property Prediction to Molecular Design

In chemistry, the forward problem is to predict a property for a given molecule. The predictive model could be density functional theory (DFT), coupled-cluster theory, or any other model that maps a molecular structure to a property.

Let $$m$$ denote a molecule and $$p$$ its property. The forward model defines the likelihood

\begin{equation}
p(p\mid m),
\end{equation}

which is the probability distribution of the property given the molecule. This distribution can also account for uncertainty in the prediction.

The inverse problem is molecular design: given a desired property $$p^{\ast}$$, which molecules are likely to exhibit it? In this case, we want the posterior distribution $$p(m\mid p^{\ast})$$.

## Bayes' Rule for Inverse Design

Bayes' rule connects the forward model to the inverse-design problem:

\begin{equation}
p(m\mid p^{\ast})=\frac{p(p^{\ast}\mid m)p(m)}{p(p^{\ast})}.
\end{equation}

Here, $$p(m)$$ is the prior distribution over molecules, $$p(p^{\ast}\mid m)$$ is the likelihood, and $$p(p^{\ast})$$ is a normalization factor called the evidence. For a discrete set of candidate molecules, the evidence is

\begin{equation}
p(p^{\ast})=\sum_{m^{\prime}}p(p^{\ast}\mid m^{\prime})p(m^{\prime}).
\end{equation}

Thus, Bayes' rule uses a forward property predictor to construct a posterior distribution over candidate molecules.

## High-Throughput Virtual Screening

For a dataset containing $$N$$ candidate molecules, a simple prior is the uniform distribution

\begin{equation}
p(m_i)=\frac{1}{N},\qquad i=1,\ldots,N.
\end{equation}

We can sample a molecule from this prior, predict its property with the forward model, and evaluate the likelihood at the desired property $$p^{\ast}$$. With a uniform prior, the posterior probability of each candidate is

\begin{equation}
p(m_i\mid p^{\ast})=\frac{p(p^{\ast}\mid m_i)}{\sum_{j=1}^{N}p(p^{\ast}\mid m_j)}.
\end{equation}

Candidates whose predicted properties are close to the target have larger likelihoods and therefore larger posterior probabilities. A Bayesian high-throughput screening procedure is then:

1. Choose a prior distribution over the dataset, such as a uniform distribution.
2. Sample a candidate molecule from the prior.
3. Predict its property using the forward model.
4. Assign an acceptance probability based on the likelihood, so that candidates close to the desired property are more likely to be retained.
5. Rank the candidates by their posterior probabilities and validate the most promising ones with higher-level calculations or experiments.

The prior can also include preferences beyond a uniform distribution. For example, it can favor molecules that are inexpensive, stable, or easy to synthesize, allowing these considerations to guide the inverse-design search.
