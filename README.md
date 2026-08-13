# German FinTech Report

## Project Overview

This project analyzes a dataset of predominantly German FinTech companies.

The main objective is to study the characteristics associated with company `Status` and to predict whether a company is active or inactive using supervised learning methods.

The analysis was conducted in Python using a Jupyter Notebook.

## Dataset

The original dataset contains information on **978 FinTech companies** described by **16 variables**.

After the data-cleaning process, companies with a high number of missing values were removed. This resulted in a final dataset of **947 usable observations**.

The dataset includes information about:

- Company age.
- Country of headquarters.
- Company segment and subsegment.
- Cooperation with banks.
- Insolvency status.
- Liquidation status.
- Company status.

## Data Preparation

The following preprocessing steps were performed:

- Companies with a high number of missing values were removed.
- The `Founding_year` variable was transformed into `Age`.
- Inconsistencies between `Segment` and `Subsegment` were corrected.
- The strong correlation between `Status` and `Liquidation` was considered.
- The `Segment` variable was encoded using dummy variables.
- One segment was used as the reference category.

## Exploratory Analysis

The exploratory analysis investigates:

- The distribution of company age.
- The geographical distribution of companies.
- The distribution of companies across the four main segments.
- The distribution of the binary variables.
- The relationship between `Status` and `Liquidation`.
- The geographical distribution of company segments across German postal areas, known as `Leitzonen`.

## Predictive Models

Two supervised learning models were used to predict company `Status`.

The predictors included in both models were:

- `Age`
- `Bank_Cooperation`
- `Insolvency`
- `Segment`

The dataset was divided into:

- **Training set**: 67% of the observations.
- **Validation set**: 33% of the observations.

### Logistic Regression

The logistic regression model was evaluated using a confusion matrix, classification metrics, the ROC curve, and the Area Under the Curve (AUC).

The model achieved an **AUC of 0.67**, indicating a moderate ability to distinguish between the two status categories.

### Classification Tree

A classification tree was developed using the entropy criterion.

The model achieved an accuracy of **83.3%**. After pruning, the accuracy decreased slightly to **82.3%**, indicating that the model remained relatively stable after reducing its complexity.

A bagging model based on **100 decision trees** achieved an accuracy of approximately **82.7%**.

## Classification Groups

The classification tree divided companies into four main groups according to company age and insolvency:

- **Group 0**: companies aged 8 years or less with `Insolvency = 0`.
- **Group 1**: companies aged more than 8 and up to 15 years with `Insolvency = 0`.
- **Group 2**: companies aged more than 15 years with `Insolvency = 0`.
- **Group 3**: companies with `Insolvency = 1`.

Group 3 was the smallest group and showed the most uncertain distribution of company status.

## Geographic Analysis

A map of Germany was created using only companies headquartered in Germany.

The original geographical data were provided as an ESRI Shapefile. To make the project easier to share, the geographical data were converted into a simplified GeoJSON file called `germany_map.geojson`.

Each `Leitzone` was coloured according to the classification group most frequently represented in that geographical area. Areas without available observations were displayed in grey.

Group 1 was the most common group and was mainly located in central-western Germany. Groups 0 and 2 were distributed relatively evenly across the rest of the country. Group 3 did not appear as the predominant group in any area, probably because it contained the fewest observations.

## Main Conclusions

Both supervised learning models produced consistent results.

The analysis suggests that company age, bank cooperation, insolvency, and economic segment provide useful information for predicting company status.

Logistic regression offers a more interpretable and linear approach, while the classification tree is more flexible and can identify non-linear relationships between the variables.

The two models are therefore complementary and together provide a more reliable interpretation of the data.

## Repository Structure

```text
.
├── README.md
├── German_FinTech_Analysis.ipynb
├── German_FinTech.xlsx
└── germany_map.geojson
```

## How to Run the Project

1. Download or clone this repository.
2. Install the required Python libraries, including `pandas`, `geopandas`, `matplotlib`, and `scikit-learn`.
3. Open `German_FinTech_Analysis.ipynb`.
4. Make sure the dataset and map paths are defined as follows:

```python
german_fin = pd.read_excel('German_FinTech.xlsx')

shapefile = 'germany_map.geojson'
geo_data = gpd.read_file(shapefile)
```

5. Run the notebook cells in order.

## Author

Elisa Diemmi
