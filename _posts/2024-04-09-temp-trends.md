---
layout: post
title: "Analysis of Trends in Temperature"
date: 2024-04-09
published: false
---

{% marginfigure 'Paper' "../assets/temp-trend.svg" 'This is a summary of the main points that were presented in a group paper that I wrote for my Mathematical Statistics class.'%}

## Introduction

There exists a growing body of scientific research aimed at assessing the causes and effects of climate change and global warming in the world. While the causes are, today, well-established, it is important to estimate the temperature trends on a regional scale in order to correctly assess the effects on the local ecosystems and improve policymaking. The assignment focused on the Netherlands, a country known for its vulnerability to the rising sea levels and it is highly probable that a sizable increase in temperature would linfluence the likelihood of such phenomenon. The scope of our investigation was limited to 3 cities: De Bilt, Eelde, and Maastricht over the span of a century *(1907-2023)* and aimed to estimate the presence of a long-term trend in the daily, monthly, and annual temperature data provided by the course coordinator, [Prof. Stephen Smeekes](https://www.stephansmeekes.nl/).

## Data

{% marginfigure 'Fig1' "../assets/temp-trends/1.jpeg" 'Figure 1: Annual Dutch Temperatures' %}

The temperature data for the three cities can be thought of as the realization of three time series processes. Since the analysis is concerned with the Netherlands, those series are more useful when aggregated. We have, thus, generated a new series for the Netherlands by averaging the three processes.

The time series processes still seem quite *"rocky"*, we decided to smooth the data by computing the cumulative ten-year average for each point as follows:

```r
tenyear <- function(data) {
  n <- length(data) - 9 
  averages <- rep(0, n)
  for(i in 1:n) {
    subset <- data[i:(i+9)]  
    averages[i] <- mean(subset)
  }
  return(averages) 
}
```

The series appear smoother than in the original plot. What appeared to be a positive trend in Figure $1$, seems to confirmed in the smoothed plot. Despite some slight differences in average temperatures of around $1$ degree Celsius, the series fluctuate in the same way. This is, however, unsurprising due to the small size of the country.

{% maincolumn "../assets/temp-trends/2.jpeg" 'Figure 2: Smoothed Annual Dutch Temperatures' %}

{% marginfigure 'Fig3' "../assets/temp-trends/3.jpeg" 'Figure 3: Histogram of ```Netherlands```' %}

The paper relies exclusively on the use of ordinary least squares regression to estimate the trend in the temperature data. This method is sensible to the presence of outliers which tends to bias the estimated coefficients. Their presence can be investigated using a histogram. The plot only shows the possibility of right-skewness which could hint towards an upward trend in the data{% sidenote 'Fig3' "The skewness indicates that above-average temperatures are less common than those below while being more likely to deviate further from the mean." %}.

Measuring the statistical significance of the possible trend requires us to make some distributional assumption. Given the limited sample *(of $117$ observations)*, it makes sense to assume that the data is generated from a $\text{T}$-distribution with $116$ degrees of freedom. To simplify the analysis, the data is assumed to be *independent and identically distributed* (i.i.d). This may be unlikely to hold due to the nature of the data.

## Code

For the assignment, we were required to code most of the statistical methods we wished to use ourselves. Since the paper relies heavily on the simple linear regression, below I present the ```R``` function that was used to estimate each model.

```r
regress <- function(y, x, truebeta = 0, alpha = 0.05) {
  
  n <- nrow(dataset) 
  meanX <- mean(x)
  meanY <- mean(y)
  # Calculating Beta 
  Covariance <- sum((x - meanX) * (y - meanY))
  Variance <- sum((x - meanX) ^ 2) 
  # Calculating Estimators 
  slope <- Covariance / Variance
  intercept <- meanY - slope * meanX  
  # Calculate error term
  error <- rep(0, n)
  error <- y - intercept -  slope * x
  # SE of Slope
  var.slope <- sum(error^2) / ((n - 2) * Variance)
  se.slope <- sqrt(var.slope)
  # T(X) of Slope
  T.slope <- (slope - truebeta) / se.slope
  # P-value of T(X)
  p.slope <- pt(T.slope, df = n - 1, lower.tail = FALSE)
  # Confidence Interval for slope
  p <- alpha / 2
  level <- 1 - alpha
  # Bounds
  Lower <- slope - qt(p, n - 1, lower.tail = FALSE) * se.slope  
  Upper <- slope + qt(p, n - 1, lower.tail = FALSE) * se.slope 
  LowerCI <- slope - qt(alpha, n - 1, lower.tail = FALSE) * se.slope # One-Sided
  ... 
}
```

## Research

The first model we investigate is the regression of temperature of the Netherlands over a trend.

$$
\tag{1}
{NL}_{t} = \alpha + \beta t + \epsilon_{t}
$$