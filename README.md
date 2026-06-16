# Heavy-Tailed Return Modeling

Statistical investigation of heavy-tailed behavior in equity returns through distribution fitting, hypothesis testing and extreme-event analysis.

## Overview

Classical financial models frequently assume that asset returns follow a Gaussian (normal) distribution. While mathematically convenient, this assumption often underestimates the probability of large market movements.

This project evaluates the validity of Gaussian assumptions using 15 years of NIFTY 50 daily returns. Gaussian and Student-t distributions are compared using goodness-of-fit tests, likelihood-based estimation and empirical tail-event analysis.

## Objectives

- Evaluate whether NIFTY returns are consistent with Gaussian assumptions.
- Quantify the extent of heavy-tailed behavior.
- Compare Gaussian and Student-t return models.
- Measure the frequency of extreme events relative to theoretical Gaussian expectations.
- Verify whether heavy tails persist outside crisis periods.

---

## Dataset

| Attribute | Value |
|------------|---------|
| Asset | NIFTY 50 Index |
| Ticker | ^NSEI |
| Source | Yahoo Finance |
| Period | Jan 2010 – May 2025 |
| Observations | 3,781 Daily Returns |

Log returns were computed as:

$$
r_t = \ln\left(\frac{P_t}{P_{t-1}}\right)
$$

---

## Methodology

### 1. Distributional Diagnostics

Computed:

- Skewness
- Kurtosis
- Jarque-Bera Test
- Anderson-Darling Test

to evaluate departures from normality.

---

### 2. Parametric Distribution Fitting

Fitted:

- Gaussian Distribution
- Student-t Distribution

using Maximum Likelihood Estimation (MLE).

The Student-t model introduces a degrees-of-freedom parameter:

$$
\nu
$$

which governs tail thickness.

---

### 3. Tail Event Analysis

Standardized returns were calculated using

$$
z_t = \frac{r_t-\mu}{\sigma}
$$

and empirical frequencies of

- 3σ events
- 4σ events
- 5σ events

were compared against Gaussian predictions.

---

### 4. Robustness Check

To ensure results were not driven solely by COVID-era volatility, kurtosis was computed separately for:

- Crisis period (2020)
- Non-crisis observations

---

## Key Findings

### Distributional Statistics

| Metric | Value |
|----------|----------|
| Skewness | -0.906 |
| Kurtosis | 16.351 |
| Anderson-Darling Statistic | 33.10 |
| Jarque-Bera p-value | ~0 |

Normality is decisively rejected.

---

### Student-t Fit

| Parameter | Value |
|------------|---------|
| Degrees of Freedom (ν) | 4.07 |
| Gaussian Log-Likelihood | 11831.64 |
| Student-t Log-Likelihood | 12173.57 |
| Improvement | +341.93 |

The Student-t model provides a substantially better fit to observed returns.

---

### Tail Event Frequencies

| Threshold | Observed | Gaussian Expected | Ratio |
|------------|-----------|--------------------|---------|
| 3σ | 43 | 10.21 | 4.21× |
| 4σ | 15 | 0.24 | 62.63× |
| 5σ | 10 | ≈0 | Extremely Large |

Large market moves occur far more frequently than predicted under Gaussian assumptions.

---

### Robustness Analysis

| Sample | Kurtosis |
|----------|----------|
| Crisis (2020) | 15.39 |
| Non-Crisis | 5.47 |

Heavy tails persist even after excluding crisis periods.

---

## Generated Figures

The notebook automatically exports report-ready figures:

```text
report_assets/
├── 01_histogram_gaussian_fit.png
├── 02_qq_plot_normality.png
├── 03_tail_probability_comparison.png
├── 04_crisis_vs_noncrisis_kurtosis.png
└── 05_gaussian_vs_student_t_fit.png
