---
layout: post
title: "Risk Neutrality"
date: 2025-04-25
published: true
---

In a recent course at the Norwegian School of Economics, we delved into the mathematical modeling of financial markets. The course was restricted to the study of markets composed of one risk-free asset, a bond, and one or more risky assets such as stocks and financial derivatives in a discrete time setting. The pricing of financial derivatives is a crucial issue in finance and relies on the condition of non-arbitrage.

The non-arbitrage assumption guarantees that there exists no possibility of riskless profit in the market. In other words, any investment strategy with a positive expected return must have a cost greater than $0$. I believe that the investors, in these market models, assumed to be rational to some extent, would never participate in a losing trade. Trading can be seen as a zero-sum game as a transaction can only happen between two agents with diametrically opposed expectations about the future price of the security. No investor would trade with the expectation of making a loss or allow the other agent to make a profit.

## Single Period Markets

These markets are defined over the time steps $t \in [0, 1]$ and consists of one bond $B$, $N$ stocks $S$, and $M$ financial derivatives $D$. While the value of the bond is deterministic, the stocks and derivatives are random variables with known values at time $t = 0$. The model also contains a sample space $\Omega$ of $K < \infty$ possible scenarios $\omega_{k}$, a (market) probability measure $\mathbb{P}$ that assigns a non-null probability to each scenario in $\Omega$, and a terminal date $T = 1$.

Let $V$ represent the value process of a portfolio $\varphi = (x, y, z)$ consisting of $x$ bonds, $y$ shares, and $z$ derivatives. This value process is denoted by $V^{\varphi}(t)$ and defined as

$$
V^{\varphi}(t) := xB(t) + yS(t) + zD(t) \quad \text{for } t = 0, 1
$$

Let the value $D(0)$ denote the price at which the derivative $D$ is traded at time $t = 0$, the derivatives pricing problem aims to find values of $D(0)$ that do not create arbitrage opportunities. These values are said to be "fair" prices for the derivative $D$. These fair prices can be found through the creation of a *replicating* portfolio. It is a portfolio $\varphi^{*} = (x, y, 0)$ whose value at time $t = 1$ is equal to the value of the derivative $D$ is all possible scenarios,

$$
V^{\varphi^{*}}(1, \omega) = D(1, \omega) \quad \forall \omega \in \Omega
$$

or $V^{\varphi^{\ast}}(0) = D(1)$ for short. If there exist such a portfolio, then the derivative $D$ is said to be *attainable*. The Law of one Price would require that, as both processes result in the same values for each scenarios at time $t = 1$, then they must have the same price at the initial time $t = 0$. If otherwise, the market would contain an arbitrage opprtunity. The unique initial price for the derivative $D$ is $D(0) = V^{\varphi^{*}}(0)$. This process for the computation of the initial price of a financial derivative can become time-consuming or laborious once one extends the model to multi-period markets or markets with more than one stock or derivative. Thus, it is necessary to introduce the concept of a risk-neutral probability measure.

### Risk-neutral Probability

A risk-neutral probability measure $\mathbb{Q}$ for a single period model with $N$ stocks and $K$ scenarios is a family $(q_{1}, \dots, q_{K})$ with $\sum_{k = 1}^{K} q_{k} = 1$ and $q_{k} \in (0, 1)$ for $k = 1, 2, \dots, K$ satisfying

$$
S_{n}(0) = \mathbb{E}_{\mathbb{Q}}[\tilde{S}_{n}(1)] = \sum_{k = 1}^{K} q_{k} \tilde{S}_{n}(1) = \sum_{k = 1}^{K} q_{k} \frac{S_{n}(1)}{B(1)}
$$

The equation above is a vector equation meaning that this relationship should hold for every stock in the market model. Furthermore, the probability measure $\mathbb{Q}$ is required to be equivalent to the market probability $\mathbb{P}$. This means that for every set $A \sube \Omega$, we have $\mathbb{Q}(A) > 0$ if and only if $\mathbb{P}(A) > 0$. Such risk-neutral probability measures provide a more efficient method to determine the fair price of a derivative in a viable market since, under this measure, the price at time $t = 0$ of any derivative is simply the expectation of the discounted price of the derivative at time $t = 1$,

$$
D(0) = E_{\mathbb{Q}}[\tilde{D}(1)]
$$

The usefulness of risk-neutral probabilities is not limited to the computation of the initial price of derivatives. It is also useful for determining the initial price of a portfolio. Since under this measure, for any portfolio $\varphi$

$$
E_{\mathbb{Q}}[\tilde{V}^{\varphi}(1)] = V^{\varphi}(0)
$$

This post contains a very short presentation of the course content and of course more content on mathematical finance could likely follow.