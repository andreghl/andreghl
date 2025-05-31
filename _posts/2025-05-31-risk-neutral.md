---
layout: post
title: "Single Period Markets"
date: 2025-05-31
---

The mathematical modeling of discrete time financial markets often involves a risk-free asset representing the time value of money, and different risk-bearing assets such as stocks and financial derivatives. The market model is defined over a finite sample space $\Omega$, a finite time horizon $T$, and a market probability measure $\mathbb{P}$. The sample space is composed of $K < \infty$ elements. Each element $\omega$ can be thought of as a potential state of the world and is assigned a probability $P(\omega)$ that specifies the likelihood of its outcome. In a single period model, the trading takes place at initial time $t = 0$ and the choices are evaluated at time $t = 1$ called the terminal date.

The market contains a bank account process or numéraire 
$$S_{0} = \set{ S_{0}(t): t = 0, 1}$$ where $S_{0}(0) = 1$ and the interest rate $r > 0$, $N$ stocks 
$$S_{n} = \set{ S_{n}(t): t = 0, 1 \text{ and } n = 1, \dots, N}$$, and a financial derivative $X$. The stock prices at initial time are positive scalars known to the investors and the stock prices at time $t = 1$ are non-negative random variables whose realization is only known at the terminal date. Investors define a trading strategy $\varphi = (\varphi_{0}, \varphi_{1}, \dots ,\varphi_{N})$ which outlines the number of units (or shares) of a security $n$ held by the investor between the two periods and the first element $\varphi_{0}$ specifies the amount of money invested in the bank account.

Lastly, the value process $V$ describes the total value of the portfolio at each point in time for a strategy $\varphi$. At time $t = 1$, the value process is a random variable  and is defined by

$$
V^{\varphi}(t) := \sum_{n = 0}^{N} \varphi_{n} S_{n}(t) \qquad t = 0, 1
$$

## Derivatives Pricing

Derivatives are financial products whose value is derived from the value of one or more underlying assets. These financial products are useful to those that seek to hedge against other investments or speculate, however their value at initial time is not always so easy to find intuitively. One technique is to obtain the intial price of a portfolio that has the same value as the option at the terminal date for all possible states of the world, relying on the presumption that the derivative is replicable. Such presumption is not always guarenteed to hold and the derivation of the replicating portfolio might not always be so straightfoward. For this reason, the introduction of a new quantity called the risk-neutral probability measure is necessary.

### Risk Neutrality

The First Fundamental Theorem of asset pricing states that in a market model with a finite sample size and a finite time $T$, the existence of a risk-neutral probability measure guarantees the absence of arbitrage opportunities in the market, and inversely. This no-arbitrage situation is interesting in market modeling as it signals that all possible claims in the market can be priced "fairly" (replicated using a portfolio) meaning that no other trader can make a free profit using a mispriced derivative contract. It is time-consuming (and impossible) to manually check that every single possible claim is replicable and thus often market modellers resort to the computation of the risk-neutral probability measure. This measure, if it exists, provides an efficient way to identify and price all attainable claims in the market and offers a range of fair prices for non-replicable claims. 

A risk-neutral probability measure $\mathbb{Q}$ on a finite sample $\Omega$ is a probability measure, equivalent to the market probability $\mathbb{P}$, with $Q(\omega_{k}) > 0$ for $k = 1, \dots, K$ and $\sum_{k = 1}^{K} q_{k} = 1$ such that

$$
E_{Q}[\tilde{S}_{n}(1)] = \sum_{k = 1}^{K} q_{k} \frac{S_{n}(1)}{S_{0}(1)} = S_{n}(0) \qquad n = 1, \dots, N
$$

Based on the First Fundamental Theorem of asset pricing, a market with no risk-neutral measure means that there exists some arbitrage opportunities. Some claims in the market cannot be priced fairly. The presence of multiple risk-neutral probabilities means that some claims in the market are not attainable. This means that the payoff of some derivatives cannot be replicated using a market portfolio but one can find a range of arbitrage-free prices. Lastly, the presence of a unique risk-neutral measure implies that the market model is complete and all financial derivatives are attainable with a unique arbitrage-free price. In complete markets, the initial price $\pi_{X}(0)$ of financial derivatives $X$ can be computed as follows

$$
\pi_{X}(0) = E_{Q}[\frac{X}{S_{0}(1)}] = \frac{1}{S_{0}(1)} \cdot \sum_{k = 1}^{K} q_{k} X(\omega_{k})
$$

In markets in which multiple risk-neutral measure exists, some claims cannot be replicated. These claims have a range of arbitrage-free prices defined as $\pi_{X}(0) \in (\pi_{X}^{\text{bid}}(0), \pi_{X}^{\text{ask}}(0))$ with

$$
\begin{split}
\pi_{X}^{\text{bid}}(0) &:= \inf_{Q \in \mathbb{Q}}{\set{E_{Q}[\frac{X}{S_{0}(1)}]}}
\\
\pi_{X}^{\text{ask}}(0) &:= \sup_{Q \in \mathbb{Q}}{\set{E_{Q}[\frac{X}{S_{0}(1)}]}}
\end{split}
$$

These results derived for discrete-time single period models can be extended to multiperiod market models quite easily. However, multiperiod modelling requires the introduction of new concepts such as information flows and martingales.