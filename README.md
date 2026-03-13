# Bayesian Inference in Lending Risk

> Estimating Interest Rate Drivers with Posterior Distributions

This project applies Bayesian inference to two lending risk questions — whether
debt-to-income ratio drives interest rates and whether homeownership status
produces meaningful rate differences — using the `loans_full_schema` dataset
from the `openintro` package. Using `rstanarm` to fit the models and
`bayestestR` to characterise the resulting posterior distributions, we
demonstrate how credible intervals, the Region of Practical Equivalence, and
the Probability of Direction together provide a richer and more
decision-relevant picture of parameter uncertainty than classical frequentist
regression. The analysis concludes that both DTI and homeownership status carry
practically significant effects on loan pricing, and that the Bayesian
framework — with its direct probability statements, honest uncertainty
quantification, and business-calibrated significance tests — is particularly
well-suited to the explainability and governance demands of modern risk model
management.

---

## Project Structure

```
.
├── bayesian_lending_risk.qmd   # Main Quarto source document
├── bayesian_lending_risk.html  # Rendered HTML output
|-- brand.yml  #quarto branding document
|-- data
    |-- loans_full_schema.csv   # downloaded data
└── README.md
```

---

## Models

| Model | Predictor | Response | Type |
|---|---|---|---|
| A | Debt-to-Income Ratio | Interest Rate | Continuous |
| B | Homeownership Status | Interest Rate | Categorical |

---

## Key Concepts Demonstrated

- Bayesian vs. frequentist regression — baseline comparison using `lm()` and `stan_glm()`
- Posterior distribution extraction and visualisation via `get_parameters()`
- Point estimation — mean, median, and Maximum A Posteriori (MAP)
- Credible intervals using the 89% Highest Density Interval (HDI)
- Region of Practical Equivalence (ROPE) — distinguishing statistical detectability from practical materiality
- Probability of Direction (pd) — confidence in effect sign
- Unified posterior summary with `describe_posterior()`
- MCMC diagnostics — R̂ and Effective Sample Size (ESS)

---

## Dataset

**`loans_full_schema`** from the [`openintro`](https://cran.r-project.org/package=openintro) package.

A real-world personal lending dataset sourced from Lending Club, containing
10,000 loan applications with variables spanning borrower financials, loan
characteristics, and credit history. The analytic sample retains complete cases
on `interest_rate`, `debt_to_income`, and `homeownership`.

---

## Requirements

### R Packages

```r
install.packages(c(
  "rstanarm",
  "bayestestR",
  "insight",
  "openintro",
  "ggplot2",
  "dplyr",
  "tidyr"
))
```

> **Note:** `rstanarm` requires a working C++ toolchain and the
> [RStan](https://mc-stan.org/rstan/) backend. See the
> [RStan Getting Started](https://github.com/stan-dev/rstan/wiki/RStan-Getting-Started)
> guide if you encounter installation issues.

### Rendering

```bash
quarto render bayesian_lending_risk.qmd
```

Requires [Quarto](https://quarto.org/) ≥ 1.3. The document uses
`cache: true` — Stan chains run once and are cached on subsequent renders.

---

## References

Bray, A., Çetinkaya-Rundel, M., & Hardin, J. (2023). *openintro: Data sets
and supplemental functions from OpenIntro textbooks*. R package.
https://CRAN.R-project.org/package=openintro

Cohen, J. (1988). *Statistical power analysis for the social sciences* (2nd
ed.). Lawrence Erlbaum.

Goodrich, B., Gabry, J., Ali, I., & Brilleman, S. (2023). *rstanarm: Bayesian
applied regression modeling via Stan*. R package.
https://mc-stan.org/rstanarm/

Kruschke, J. (2014). *Doing Bayesian data analysis: A tutorial with R, JAGS,
and Stan* (2nd ed.). Academic Press.

Makowski, D., Ben-Shachar, M. S., & Lüdecke, D. (2019). bayestestR:
Describing effects and their uncertainty, existence and significance within
the Bayesian framework. *Journal of Open Source Software, 4*(40), 1541.
https://doi.org/10.21105/joss.01541

McElreath, R. (2018). *Statistical rethinking: A Bayesian course with examples
in R and Stan*. Chapman & Hall/CRC.

---

*Built with [Quarto](https://quarto.org/) · [R](https://www.r-project.org/) ·
[Stan](https://mc-stan.org/)*
