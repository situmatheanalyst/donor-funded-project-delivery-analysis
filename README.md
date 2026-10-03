# donor-funded-project-delivery-analysis
Quantitative statistical analysis examining how project monitoring and control techniques relate to project delivery in donor-funded projects in Kenya using IBM SPSS Statistics.
---

title: "Donor-Funded Project Delivery Analysis"
author: "Situma The Analyst"
date: "`r Sys.Date()`"
output:
github_document:
toc: true
toc_depth: 3
------------

# Donor-Funded Project Delivery Analysis

**Quantitative statistical analysis examining how project monitoring and control techniques relate to project delivery in donor-funded projects in Kenya using IBM SPSS Statistics and R.**

**Author:** [Situma The Analyst](https://github.com/situmatheanalyst)

**Repository:** [donor-funded-project-delivery-analysis](https://github.com/situmatheanalyst/donor-funded-project-delivery-analysis)

---

## Research Title

**Effect of Project Monitoring and Control Techniques on Project Delivery: A Quantitative Study of Donor-Funded Projects in Kenya**

---

## 1. Project Overview

This project investigates the relationship between project monitoring and control techniques and project delivery in donor-funded projects in Kenya.

The study examines how different monitoring and control techniques relate to project delivery outcomes and assesses whether institutional capacity moderates these relationships.

The analysis demonstrates the application of quantitative statistical methods to survey data using **IBM SPSS Statistics and R**.

The project covers:

* Data preparation and screening
* Descriptive statistics
* Reliability analysis
* Pearson correlation analysis
* Multiple linear regression
* Regression diagnostics
* Moderation analysis
* Interaction effects
* Statistical interpretation
* Reproducible research

---

## 2. Research Aim

The main aim of the study is to examine the effect of project monitoring and control techniques on project delivery in donor-funded projects in Kenya.

---

## 3. Research Objectives

The study has four main objectives:

1. To examine the effect of specific project monitoring and control techniques, including Earned Value Management (EVM), Critical Path Method (CPM), variance analysis, milestone tracking, and risk-based control, on project delivery.

2. To determine which project monitoring and control technique has the strongest predictive effect on project delivery.

3. To examine interaction effects among project monitoring and control techniques.

4. To assess whether institutional capacity moderates the relationship between project monitoring and control techniques and project delivery.

---

## 4. Research Questions

The study addresses the following research questions:

1. What is the effect of project monitoring and control techniques on project delivery?

2. Which monitoring and control technique has the strongest predictive relationship with project delivery?

3. Are there interaction effects among project monitoring and control techniques?

4. Does institutional capacity moderate the relationship between monitoring and control techniques and project delivery?

---

## 5. Study Scope

The study focuses on donor-funded projects implemented in Kenya.

The projects considered include projects in:

* Infrastructure
* Health
* Education
* Agriculture
* Water
* Governance

The study covers projects financed by bilateral and multilateral donors between **2019 and 2025**.

The study focuses on completed or near-completion projects.

Private-only projects and county-only projects were excluded from the study scope.

---

## 6. Research Methodology

### Research Philosophy

The study follows a **postpositivist research philosophy**.

### Research Approach

A **deductive research approach** was adopted.

### Research Method

The study uses a **quantitative survey methodology**.

### Research Design

The research uses a:

* Cross-sectional design
* Non-experimental design
* Correlational approach
* Moderation analysis framework

### Data Collection

Data were collected using a structured questionnaire administered through Qualtrics.

The questionnaire used a **5-point Likert scale** to measure the study constructs.

---

## 7. Dataset

The dataset contains **60 participant records**.

However, the number of valid observations varied across questionnaire sections:

| Questionnaire Section | Valid Observations |
| :-------------------- | -----------------: |
| Q1–Q4                 |                 36 |
| Q5–Q23                |                 30 |

The substantive statistical analyses were based on **30 valid observations**.

Missing values were retained as system missing values, with listwise deletion applied where required for composite statistical analyses.

---

## 8. Study Variables

| Code     | Construct               | Description                                                            |
| :------- | :---------------------- | :--------------------------------------------------------------------- |
| EVM      | Earned Value Management | Project performance monitoring using earned value techniques           |
| CPM      | Critical Path Method    | Scheduling and critical path monitoring                                |
| VAR      | Variance Analysis       | Identification and assessment of deviations from project plans         |
| RISK     | Risk-Based Control      | Monitoring and controlling project risks                               |
| QUALITY  | Quality                 | Project quality-related measures                                       |
| IC       | Institutional Capacity  | Capacity of institutions to support project implementation and control |
| DELIVERY | Project Delivery        | Project delivery outcome                                               |

---

# 9. Data Analysis Workflow

The analytical workflow followed a structured statistical process:

```text
Survey Data
     ↓
Data Preparation
     ↓
Data Screening
     ↓
Descriptive Statistics
     ↓
Reliability Analysis
     ↓
Correlation Analysis
     ↓
Multiple Regression
     ↓
Regression Diagnostics
     ↓
Moderation Analysis
     ↓
Interaction Effects
     ↓
Interpretation
```

---

# 10. R Environment

```{r setup, message=FALSE, warning=FALSE}
# Install packages if necessary
# install.packages(c(
#   "tidyverse",
#   "psych",
#   "car",
#   "lmtest",
#   "interactions",
#   "knitr"
# ))

library(tidyverse)
library(psych)
library(car)
library(lmtest)
library(interactions)
library(knitr)

knitr::opts_chunk$set(
  echo = TRUE,
  warning = FALSE,
  message = FALSE
)
```

---

# 11. Data Import

The cleaned dataset is expected to be stored in the `data` directory.

```{r import-data}
data <- read.csv("data/project_data.csv")

head(data)
```

---

# 12. Data Screening

## Dataset Structure

```{r data-structure}
str(data)
```

## Summary Statistics

```{r data-summary}
summary(data)
```

## Missing Values

```{r missing-values}
colSums(is.na(data))
```

## Duplicate Records

```{r duplicate-check}
sum(duplicated(data))
```

## Variable Names

```{r variable-names}
names(data)
```

---

# 13. Descriptive Statistics

Descriptive statistics were calculated for the major study constructs using the mean and standard deviation.

```{r descriptive-statistics}
descriptive_statistics <- data %>%
  summarise(
    EVM_Mean = mean(EVM, na.rm = TRUE),
    EVM_SD = sd(EVM, na.rm = TRUE),

    CPM_Mean = mean(CPM, na.rm = TRUE),
    CPM_SD = sd(CPM, na.rm = TRUE),

    VAR_Mean = mean(VAR, na.rm = TRUE),
    VAR_SD = sd(VAR, na.rm = TRUE),

    RISK_Mean = mean(RISK, na.rm = TRUE),
    RISK_SD = sd(RISK, na.rm = TRUE),

    QUALITY_Mean = mean(QUALITY, na.rm = TRUE),
    QUALITY_SD = sd(QUALITY, na.rm = TRUE),

    IC_Mean = mean(IC, na.rm = TRUE),
    IC_SD = sd(IC, na.rm = TRUE),

    DELIVERY_Mean = mean(DELIVERY, na.rm = TRUE),
    DELIVERY_SD = sd(DELIVERY, na.rm = TRUE)
  )

descriptive_statistics
```

### Reported Descriptive Results

| Construct | Mean |   SD |
| :-------- | ---: | ---: |
| EVM       | 3.38 | 1.03 |
| CPM       | 3.55 | 0.97 |
| VAR       | 3.49 | 0.92 |
| RISK      | 3.48 | 1.00 |
| QUALITY   | 3.98 | 0.84 |
| IC        | 3.62 | 1.05 |
| DELIVERY  | 3.51 | 1.04 |

---

# 14. Reliability Analysis

Internal consistency reliability was assessed using **Cronbach's alpha**.

| Construct | Cronbach's Alpha |
| :-------- | ---------------: |
| EVM       |            0.753 |
| CPM       |            0.662 |
| VAR       |            0.734 |
| RISK      |            0.750 |
| QUALITY   |            0.794 |
| IC        |            0.810 |
| DELIVERY  |            0.849 |

### Reliability Analysis in R

If the individual questionnaire items are available, Cronbach's alpha can be calculated using the `psych` package.

```{r reliability-analysis}
# Example:
# alpha(data[, c("EVM1", "EVM2", "EVM3", "EVM4")])

# Example:
# alpha(data[, c("CPM1", "CPM2", "CPM3", "CPM4")])
```

---

# 15. Pearson Correlation Analysis

Pearson correlation analysis was used to examine the relationships among the major study variables.

```{r correlation-analysis}
correlation_matrix <- cor(
  data[, c(
    "EVM",
    "CPM",
    "VAR",
    "RISK",
    "QUALITY",
    "IC",
    "DELIVERY"
  )],
  use = "pairwise.complete.obs",
  method = "pearson"
)

round(correlation_matrix, 3)
```

### Correlation Visualisation

```{r correlation-plot}
correlation_data <- as.data.frame(
  as.table(correlation_matrix)
)

ggplot(
  correlation_data,
  aes(
    x = Var1,
    y = Var2,
    fill = Freq
  )
) +
  geom_tile() +
  geom_text(
    aes(label = round(Freq, 2))
  ) +
  labs(
    title = "Correlation Matrix",
    x = NULL,
    y = NULL,
    fill = "Correlation"
  ) +
  theme_minimal()
```

---

# 16. Multiple Linear Regression

Multiple linear regression was used to examine the relationship between project monitoring and control techniques and project delivery.

The regression model is expressed as:

$$
DELIVERY =
\beta_0 +
\beta_1EVM +
\beta_2CPM +
\beta_3VAR +
\beta_4RISK +
\epsilon
$$

Where:

* `DELIVERY` = Project delivery
* `EVM` = Earned Value Management
* `CPM` = Critical Path Method
* `VAR` = Variance Analysis
* `RISK` = Risk-Based Control
* $\epsilon$ = Error term

---

## 16.1 Regression Model

```{r regression-model}
regression_model <- lm(
  DELIVERY ~ EVM + CPM + VAR + RISK,
  data = data
)

summary(regression_model)
```

---

## 16.2 Regression Results

The reported regression model produced:

* **F(4, 25) = 5.963**
* **p = .002**
* **R² = .488**

The model therefore accounted for approximately **48.8% of the observed variation in project delivery** within the analysed sample.

---

# 17. Regression Diagnostics

Regression assumptions should be assessed before interpreting the regression model.

## Normality of Residuals

```{r residual-normality}
hist(
  residuals(regression_model),
  main = "Distribution of Regression Residuals",
  xlab = "Residuals"
)
```

### Q-Q Plot

```{r qq-plot}
qqnorm(residuals(regression_model))
qqline(residuals(regression_model))
```

## Residuals vs Fitted Values

```{r residual-fitted}
plot(
  fitted(regression_model),
  residuals(regression_model),
  xlab = "Fitted Values",
  ylab = "Residuals",
  main = "Residuals vs Fitted Values"
)

abline(h = 0)
```

## Breusch-Pagan Test

```{r breusch-pagan}
bptest(regression_model)
```

## Multicollinearity

Variance Inflation Factors (VIF) can be used to assess multicollinearity.

```{r vif}
vif(regression_model)
```

---

# 18. Moderation Analysis

The study examines whether **institutional capacity (IC)** moderates the relationship between project monitoring and control techniques and project delivery.

A moderation model evaluates whether the relationship between a predictor and an outcome changes according to the level of a moderator.

The general model is:

$$
DELIVERY =
\beta_0 +
\beta_1X +
\beta_2IC +
\beta_3(X \times IC)
+
\epsilon
$$

Where:

* `X` = Project monitoring/control technique
* `IC` = Institutional Capacity
* `X × IC` = Interaction term
* `DELIVERY` = Project delivery

---

# 19. Centering Institutional Capacity

```{r center-moderator}
data <- data %>%
  mutate(
    IC_c = IC - mean(IC, na.rm = TRUE)
  )
```

---

# 20. Example EVM Moderation Model

```{r evm-moderation}
evm_moderation <- lm(
  DELIVERY ~ EVM * IC_c,
  data = data
)

summary(evm_moderation)
```

The interaction term is:

```text
EVM:IC_c
```

A statistically significant interaction term would provide evidence that institutional capacity changes the relationship between EVM and project delivery.

---

# 21. Hierarchical Moderation Model

## Block 1 — Main Effects

```{r moderation-block1}
model_block1 <- lm(
  DELIVERY ~ EVM + CPM + VAR + RISK + IC,
  data = data
)

summary(model_block1)
```

## Block 2 — Interaction Effects

```{r moderation-block2}
model_block2 <- lm(
  DELIVERY ~
    EVM +
    CPM +
    VAR +
    RISK +
    IC +
    EVM:IC +
    CPM:IC +
    VAR:IC +
    RISK:IC,
  data = data
)

summary(model_block2)
```

---

# 22. Comparing Moderation Models

```{r model-comparison}
anova(
  model_block1,
  model_block2
)
```

The model comparison can be used to examine whether adding the interaction terms produces an improvement in model fit.

---

# 23. Interaction Visualisation

An interaction can be visualised using the `interactions` package.

```{r interaction-plot}
interact_plot(
  evm_moderation,
  pred = EVM,
  modx = IC_c,
  interval = TRUE
)
```

The interaction plot provides a visual representation of the relationship between EVM and project delivery at different levels of institutional capacity.

---

# 24. Hypotheses

### General Hypothesis

**H₁:** Project monitoring and control techniques have a significant relationship with project delivery in donor-funded projects in Kenya.

### Moderation Hypothesis

**H₂:** Institutional capacity significantly moderates the relationship between project monitoring and control techniques and project delivery.

Individual hypotheses can also be specified for each monitoring and control technique.

---

# 25. Statistical Significance

The study uses a conventional significance level of:

$$
\alpha = 0.05
$$

Therefore:

* **p < 0.05** indicates statistical evidence against the null hypothesis at the 5% significance level.
* **p ≥ 0.05** indicates insufficient statistical evidence to reject the null hypothesis at the 5% significance level.

Statistical significance should be interpreted alongside effect sizes, confidence intervals, model assumptions, and the research design.

---

# 26. Key Analytical Findings

The descriptive analysis produced the following mean scores:

| Construct | Mean |   SD |
| :-------- | ---: | ---: |
| EVM       | 3.38 | 1.03 |
| CPM       | 3.55 | 0.97 |
| VAR       | 3.49 | 0.92 |
| RISK      | 3.48 | 1.00 |
| QUALITY   | 3.98 | 0.84 |
| IC        | 3.62 | 1.05 |
| DELIVERY  | 3.51 | 1.04 |

The reliability coefficients ranged from **0.662 to 0.849** across the study constructs.

The multiple regression model reported:

$$
F(4,25) = 5.963,\quad p = .002,\quad R^2 = .488
$$

This indicates that the model explained approximately **48.8% of the observed variation in project delivery** within the analysed sample.

---

# 27. Limitations

### Cross-Sectional Design

Because the data were collected at one point in time, the study cannot establish temporal precedence or strong causal conclusions.

### Self-Reported Data

The study relies on participants' perceptions and responses, which may introduce response bias.

### Common Method Variance

Because the constructs were measured using the same survey instrument, common method variance may affect observed relationships.

### Sample Size

The substantive analyses were based on **30 valid observations**, which limits statistical power and generalisability.

### Generalisability

The findings are specific to the context of donor-funded projects in Kenya and may not directly generalise to private-sector or other project environments.

---

# 28. Data Privacy and Research Ethics

The project follows principles of responsible research data management.

The survey data were collected anonymously and participation was voluntary.

The study incorporated:

* Informed consent
* Anonymous participation
* No personally identifiable information in the analytical dataset
* Secure data collection
* Controlled access to research data
* Appropriate handling of research information

The research also considers the requirements of the **Kenya Data Protection Act**.

> **Important:** Respondent-level raw data should not be uploaded to a public GitHub repository unless appropriate permission has been obtained.

The public repository should instead contain:

* Analysis scripts
* Documentation
* Variable definitions
* Aggregated results
* Reproducible code
* Non-sensitive example data where appropriate

---

# 29. Repository Structure

```text
donor-funded-project-delivery-analysis/
│
├── README.md
├── README.Rmd
│
├── data/
│   └── README.md
│
├── R/
│   ├── data_preparation.R
│   ├── descriptive_statistics.R
│   ├── reliability_analysis.R
│   ├── correlation_analysis.R
│   ├── regression_analysis.R
│   └── moderation_analysis.R
│
├── analysis/
│   └── SPSS/
│       ├── data_preparation.sps
│       ├── descriptive_statistics.sps
│       ├── reliability_analysis.sps
│       ├── correlation_analysis.sps
│       ├── regression_analysis.sps
│       └── moderation_analysis.sps
│
├── outputs/
│   ├── descriptive_statistics/
│   ├── reliability/
│   ├── correlations/
│   ├── regression/
│   └── moderation/
│
├── figures/
│   ├── conceptual_framework.png
│   └── analysis_figures/
│
└── documentation/
    ├── methodology.md
    ├── variable_dictionary.md
    └── findings.md
```

---

# 30. Tools & Technologies

| Tool                    | Application                                    |
| :---------------------- | :--------------------------------------------- |
| **IBM SPSS Statistics** | Survey and statistical analysis                |
| **R**                   | Statistical analysis and reproducible research |
| **R Markdown**          | Reproducible reporting                         |
| **Microsoft Excel**     | Data preparation and inspection                |
| **GitHub**              | Version control and portfolio presentation     |
| **ggplot2**             | Data visualisation                             |
| **psych**               | Reliability analysis                           |
| **car**                 | Regression diagnostics                         |
| **lmtest**              | Statistical tests                              |
| **interactions**        | Moderation analysis and interaction plots      |

---

# 31. Portfolio Value

This project demonstrates practical application of statistical analysis to a real-world project management research problem.

The project showcases skills in:

* Quantitative research
* Survey data analysis
* Data cleaning
* Descriptive statistics
* Reliability analysis
* Correlation analysis
* Regression modelling
* Moderation analysis
* Interaction effects
* Regression diagnostics
* Statistical interpretation
* SPSS
* R programming
* R Markdown
* Reproducible research

The analytical workflow demonstrates how to move from **survey data to statistical evidence and research insights**.

---

# 32. About Situma The Analyst

## Situma The Analyst

**Data Analytics & Statistical Consulting for Researchers, Businesses and Organisations**

I am a statistician and data analyst focused on transforming raw data into meaningful statistical, research, and business insights.

### Areas of Work

* Statistical analysis
* Research data analysis
* Data cleaning
* Regression analysis
* Survey analysis
* SPSS analysis
* Stata analysis
* R programming
* Python analytics
* Excel analytics
* Power BI
* Tableau
* SQL
* Data visualisation

I work with researchers, businesses, and organisations to transform data into clear evidence that supports better decision-making.

---

# 33. Professional Tagline

> **Numbers don't lie. Let's find the truth in your data.**

---

# 34. Connect With Me

**GitHub:** [situmatheanalyst](https://github.com/situmatheanalyst)

**This Project:** [donor-funded-project-delivery-analysis](https://github.com/situmatheanalyst/donor-funded-project-delivery-analysis)

---

# 35. Disclaimer

This repository is intended for **research, educational, analytical, and portfolio demonstration purposes**.

The findings should be interpreted within the context of the study design, sample size, measurement approach, and stated limitations.

The repository does not claim that the observed statistical relationships establish causality.

---

## Author

**Situma The Analyst**

*Data Analytics & Statistical Consulting for Researchers, Businesses and Organisations*

> **Numbers don't lie. Let's find the truth in your data.**
