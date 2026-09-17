# Smart TV Consumer Intelligence & Competitive Positioning

**Analyzing 111,191 Amazon reviews and 1,097 Smart TV products across Samsung, LG, Sony, TCL, and Hisense.**

## Overview

**Research question:** What product attributes are associated with consumer satisfaction, and how are major Smart TV brands positioned relative to competitors?

This project combines product specifications and consumer review signals to examine rating patterns and compare brand profiles. It describes associations, not causal effects or current market performance.

## Dataset

- **Source:** McAuley Lab's Amazon Reviews 2023, Electronics category
- **Period:** 2015–2023
- **Sample:** 3,027 products and 218,226 reviews initially; **1,097 products and 111,191 reviews** after cleaning
- **Scope:** Samsung, LG, Sony, TCL, and Hisense

Price was excluded as a primary analytical variable because valid price data covered only 9.25% of initial products; perceived value was examined through reviews instead.

## Analysis Pipeline

| Notebook | Analysis |
| --- | --- |
| [01 · Data Collection](notebooks/01_data_collection.ipynb) | Select TV products and match reviews from Amazon data. |
| [02 · Data Cleaning](notebooks/02_data_cleaning.ipynb) | Define the analytical sample, clean reviews, and extract product attributes. |
| [03 · Exploratory Analysis](notebooks/03_exploratory_analysis.ipynb) | Compare ratings, specifications, and review concentration. |
| [04 · Consumer Review Analysis](notebooks/04_consumer_review_analysis.ipynb) | Identify eight review aspects and examine associations with ratings using OLS with HC3 robust standard errors. |
| [05 · Competitive Positioning](notebooks/05_competitive_positioning.ipynb) | Compare product portfolios and relative consumer-experience profiles across five brands. |

## Key Findings

### 1. Rating aggregation changes brand comparisons

Review-weighted and product-weighted ratings produce different results because products receive unequal numbers of reviews.

For example, Sony's review-weighted average rating is 3.97 stars, compared with a product-weighted average of 4.16 stars.

This distinction matters when interpreting brand-level satisfaction because a small number of highly reviewed products can disproportionately influence review-weighted results.

### 2. Review volume is concentrated among popular products

TCL's five most-reviewed products account for approximately 67.71% of its reviews.

This concentration suggests that brand-level averages may reflect the experiences associated with a relatively small number of popular products rather than the entire product portfolio equally.

### 3. Product specifications show descriptive associations with ratings

OLED products average approximately 4.29 stars, compared with 3.98 stars for LED/LCD products.

Screen size, resolution, and display technology also show differences across rating groups. However, these patterns are descriptive associations and do not establish that a particular specification causes higher satisfaction.

### 4. Consumer experience extends beyond hardware specifications

Picture Quality is the most frequently mentioned consumer experience aspect, appearing in approximately 40.8% of reviews.

Ease of Use & Setup is positively associated with ratings in the regression analysis, while reviews mentioning Reliability and Customer Support show strong negative associations.

These findings highlight associations between consumer ratings and both everyday product experiences and ownership-related issues.

Importantly, an aspect mention indicates that a topic was discussed. It does not directly measure whether the reviewer expressed positive or negative sentiment about that specific aspect.

### 5. Brands exhibit different competitive profiles

The competitive positioning analysis combines product portfolio characteristics with review-based consumer experience measures.

LG shows above-average aspect-associated ratings across several experience dimensions, while Sony also shows positive relative results in multiple areas.

TCL shows relatively positive results in usability and value, while Samsung and Hisense display different patterns across the measured dimensions.

These profiles describe differences within the five-brand analytical sample rather than overall brand quality or current market performance.


## Visualizations

**Consumer experience positioning** — Relative aspect-associated ratings across four dimensions (Core Experience, Usability, Ownership, and Value), measured against the five-brand average. Positive and negative values represent differences from the sample average, not absolute product-quality scores.

![Consumer experience positioning](outputs/figures/05_consumer_experience_positioning_relative_to_brandav.png)

**Display technology mix** — Distribution of extracted display technology categories across the five brands. Categories are inferred from product metadata and may contain classification errors or unknown values.

![Display technology mix](outputs/figures/05_display_technology_mix_by_brand.png)

**Rating aggregation** — Comparison of two brand-rating aggregation methods, illustrating the influence of unequal review volume across products.

![Rating aggregation comparison](outputs/figures/03_weighted_rating_comparison.png)

Additional figures and result tables are available in [`outputs/`](outputs/).

## Limitations

Amazon reviewers and selected products may not represent the wider market. The data cover **2015–2023**, not today's market. Keyword-based aspect detection identifies *mentions*, not aspect-specific sentiment, and metadata-derived specifications may contain errors. Review concentration affects aggregate ratings, price coverage is limited, and all reported relationships are **associations rather than causal effects**.

## Repository Structure & Reproduction

```text
smart-tv-consumer-intelligence/
├── data/
│   └── README.md
├── notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_exploratory_analysis.ipynb
│   ├── 04_consumer_review_analysis.ipynb
│   └── 05_competitive_positioning.ipynb
├── outputs/
│   ├── figures/
│   └── tables/
├── .gitignore
├── README.md
└── requirements.txt
```

The Parquet datasets are excluded from GitHub because of their size. The notebooks document the data preparation and analysis workflow.

- [`notebooks/`](notebooks/) — Five notebooks in execution order
- [`outputs/figures/`](outputs/figures/) — Visualizations
- [`outputs/tables/`](outputs/tables/) — Result CSVs
- [`data/README.md`](data/README.md) — Data information; large Parquet files are excluded from GitHub
- [`requirements.txt`](requirements.txt) — Python dependencies

## How to Run

Run the notebooks from the `notebooks/` directory because the relative data and output paths are defined from that working directory.

1. Clone this repository and install the dependencies listed in `requirements.txt`.
    ```
    git clone https://github.com/choah0116/smart-tv-consumer-intelligence.git
    cd smart-tv-consumer-intelligence
    python -m pip install -r requirements.txt
    ```
2. Obtain the Amazon Reviews 2023 Electronics dataset and run `01_data_collection.ipynb` to generate the raw product and review Parquet files.
3. Run `02_data_cleaning.ipynb` to construct the final analytical sample.
4. Run `03_exploratory_analysis.ipynb`, followed by `04_consumer_review_analysis.ipynb` and `05_competitive_positioning.ipynb`.

The original large-scale data collection was performed in Google Colab. Subsequent cleaning and analysis were conducted locally in VS Code.

The data collection notebook has not been fully re-executed in the final local environment. Reproducing the project from scratch requires downloading and processing the original dataset.


## Tools and Libraries

Python, pandas, NumPy, Matplotlib, Seaborn, scikit-learn, statsmodels, Hugging Face Datasets, Jupyter Notebook, and Google Colab.
