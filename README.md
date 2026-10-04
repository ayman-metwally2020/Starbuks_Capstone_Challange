# Starbucks Capstone: Who Responds to Offers?

![Python](https://img.shields.io/badge/python-3.8%2B-blue) ![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange) ![Udacity](https://img.shields.io/badge/Udacity-Data%20Scientist%20Nanodegree-02b3e4)

Capstone project for the Udacity Data Scientist Nanodegree. It uses simulated data from the Starbucks Rewards app to find **which customers respond to which offers** (BOGO, discount, informational), and what drives their spend.

![Response rate overall](pic/response_rate_overall.png)

## Problem

Not every customer receives every offer, and an offer only counts as successful if the customer *views* it **and** spends past its difficulty within the offer window. The work:

1. Clean and join three sources: the offer portfolio, customer profiles and the event transcript.
2. Attribute each transaction to the offer that was active and viewed at that time (the hardest part).
3. Explore response rates by age, income, gender and membership tenure.
4. Model customer spend with Linear Regression, Random Forest and SVR.

## Key findings

- **BOGO and discount offers** drive far more response than informational offers.
- **Higher-income customers, women, and members with about three years' tenure** respond and spend the most. They are the best targets for paid offers.
- Top drivers of response: total spend, membership tenure, the social channel, offer difficulty, duration and reward.
- Advertising lifts revenue but not necessarily profit. With low base response rates, untargeted promotions can cost more than they return.

| Model | R² train | R² test |
|---|---|---|
| Linear Regression | 0.40 | 0.41 |
| Random Forest | 0.41 | 0.37 |
| SVR | 0.42 | 0.42 |

*R² of about 0.4 means demographics and offer attributes explain part of the spend, but not most of it. More behavioural features would help (see Next steps).*

| | |
|---|---|
| ![Response by income](pic/response_rate_on_income.png) | ![Response by age](pic/response_rate_on_age.png) |

## Repository

| Path | Contents |
|---|---|
| `Starbucks_Capstone_notebook.ipynb` | Full analysis (also exported as HTML) |
| `data/` | `portfolio.json`, `profile.json`, `transcript.zip` (unzip to `transcript.json`) |
| `pic/` | Charts used in this README |

```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels
unzip data/transcript.zip -d data/
jupyter notebook Starbucks_Capstone_notebook.ipynb
```

## Next steps

- Reframe the task as classification (will the customer complete a viewed offer?) and optimise for F1 on the imbalanced classes.
- Engineer behavioural features: recency, frequency, and spend before the offer.
- Uplift modelling, to target customers an offer actually changes rather than ones who would buy anyway.

## Data schema

<details><summary>portfolio / profile / transcript fields</summary>

**portfolio.json**: `id`, `offer_type` (bogo / discount / informational), `difficulty`, `reward`, `duration` (days), `channels`
**profile.json**: `id`, `age`, `gender`, `income`, `became_member_on`
**transcript.json**: `person`, `event` (transaction / offer received / viewed / completed), `time` (hours from start), `value` (offer id or amount)

</details>

Data is simulated and provided by Udacity and Starbucks for educational use.

---
Author: [Ayman Metwally](https://github.com/ayman-metwally2020)
