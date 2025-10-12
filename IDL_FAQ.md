

## **Trading IDL (Incremental Default Loss) FAQ** 

---

## What is Trading IDL?

**Trading Incremental Default Loss (IDL)** quantifies the potential loss from the **default** of an entity—such as a bond **issuer** or a credit default swap (CDS) **reference entity**—under a **stressed market scenario**. Essentially, it measures the increase in risk exposure to defaults when market conditions are poor.

---

## What is the Scope of Trading IDL?

Trading IDL covers all positions in the **trading book** that are exposed to **default risk**. This includes, but isn't limited to, instruments like:

* **Debt:** such as sovereign, local government, and corporate debt
* **Derivatives:** such as Credit Default Swaps (CDS)
* **Equities** 

---

## How is Trading IDL Calculated?

The calculation involves a multi-step simulation process to model losses under stress:

### *1. Initial Stress Scenario and Jump-to-Default (JTD) Calculation*

First, a **stressed Jump-to-Default (JTD)** loss is calculated. This involves applying severe **market shocks**—such as dramatic changes in interest rates, FX, credit spreads, and equity prices—that correspond to a specific, predefined stressed scenario.

### *2. Default Scenario Simulation*

A **Gaussian copula model** (similar to the one used in the Basel 2.5 Incremental Risk Charge (IRC) model) is employed to simulate multiple **default scenarios**.

* Each scenario identifies a list of entities that default.
* The model assumes default dynamics are driven by **six systemic factors** (common to all entities) and an **idiosyncratic factor** (specific to each entity).


$$Y_i = \sum_{k=1}^{6} \beta_k^{(i)} \cdot Z_k + X_i \cdot \sqrt{1 - \sum_{k=1}^{6} \beta_k^{(i)}\cdot \beta_k^{(i)}} $$

Where:
* $Y_i$ is the latent variable for entity $i$
* $\beta_k^{(i)}$ is the correlation parameters for entities in the region/sector/rating bucket that entity $i$ belongs to
* $Z_k$ are the six systemic factors, each following a standard normal distribution
* $X_i$ is the idiosyncratic factor for entity $i$, also following a standard normal distribution

### *3. Recovery Rate Modeling*

If an entity defaults, the **recovery rate** (the percentage of the exposure that can be recovered) is also simulated. This simulation varies based on the **seniority** of the debt. The recovery rate for **equity positions** is conventionally assumed to be zero.

### *4. Loss Aggregation*

For every defaulted entity, the **Loss Given Default (LGD)** for each associated trading position is calculated. These individual position losses are then  **aggregated** across the entire portfolio (e.g., at the legal entity level).

### *5. Deriving the IDL Value*

* The simulation is repeated numerous times to generate a complete **loss distribution**.
* The IDL is then reported as the **average of the tail losses**, or **expected default shortfall (EDS)** of the loss distribution beyond a specified percentile. For example, in a "1-in-50 stressed scenario," the IDL is defined as the average of the **$5\%$ most severe losses** from the resulting distribution, or the **EDS at $95\%$**.

---

## What are the specific data and parameters required to run the IDL model?

The IDL model requires two main categories of inputs: **Model Parameters** and **Portfolio Exposures and Attributes**.

### *1. Model Parameters*

These parameters define the model's underlying risk characteristics and their derivation:

| Parameter | Derivation and Key Details |
| :--- | :--- |
| **Probability of Default (PD)** | The **six-month** PDs (corresponding to the liquidity horizon) are derived from the one-year rating migration matrices published by **Moody's**. PDs are driven by the entity's rating and whether it is a sovereign, muni, or corporate entity. |
| **Recovery Rates** | Derived from historical data published by **Moody's**. They depend on the **debt seniority** and the entity type (sovereign, muni, or corporate). A **beta distribution** is fitted to the historical data to simulate the recovery rates. Recovery rates for equity positions are assumed to be zero. |
| **Asset Correlations** | Parameters are similar to those used in the **Basel 2.5 IRC model**. Correlations depend on the region, sector, and rating of each entity. |

### *2. Portfolio Exposures and Attributes*

This portfolio-specific data defines the positions being analyzed:

1.  **Stressed JTD** (Jump-to-Default)
2.  **Notional amounts**
3.  **Entity Attributes:** Region, sector, and rating of each entity
4.  **Debt seniority**
5.  **Maturity of the position**
---

## How is the total IDL broken down by different sources (e.g., issuer or business)?

The total IDL is attributed to various sources, such as individual **issuer names** or **business lines**, by calculating the **component or contributory Expected Default Shortfall (cEDS)** for each source.

The **cEDS** for a source is defined as the average of the **tail losses** (those beyond the specified percentile) in the overall loss distribution that are specifically driven by the defaults of entities associated with that source.

Crucially, the sum of all cEDS values across all sources equals the total IDL. This allows for clear attribution, as shown in the example of the top contributing issuers to Citi's total IDL.

***[Insert Example Table or Chart Here]***

---
## What are typically the main contributors to trading IDL?
This rephrasing maintains clarity and conciseness while integrating the specific, detailed information about the parameters you requested.

***

## How are multi-name products treated in the IDL calculation?
## What happens if the underlying is an index?
## How does maturity affect the IDL calculation?
## How does debt seniority affect the IDL calculation?
## How are off-the-run bonds treated in the IDL calculation?
## How are non-linear instruments treated in the IDL calculation?
## How are positions with embedded options treated in the IDL calculation?
## How are positions with contingent features treated in the IDL calculation?
## How are positions with netting agreements treated in the IDL calculation?
## How are positions with guarantees treated in the IDL calculation?
## How frequently is IDL calculated?
## What is the time horizon for IDL?
## How is the global marke shocks applied?
## How is the percentile threshold calibrated?
## WHat are the main drivers of IDL?
## Why is the allocation to a particular desk changed significantly, even though the portfolio of the desk has changed very little?
## What should I pay attention to when signing off IDL numbers?
