# CRISP-DM report: road traffic deaths dashboard (SDG 3.6)

## 1. Business understanding

The dashboard analyses global road traffic deaths under SDG indicator 3.6.1. It covers:

- death rates per 100,000 population
- differences between demographic groups
- urban versus rural settings

It also points to likely causes, such as poor infrastructure and the economic challenges of low-income countries.

**Problem statement.** Road traffic injuries are one of the leading causes of preventable death worldwide. They hit vulnerable groups hardest, such as children, pedestrians and cyclists, particularly in low-income countries. Several factors make the problem worse:

- poor road infrastructure
- weak traffic safety measures
- weak healthcare systems
- economic instability, which limits investment in safer roads and in enforcing traffic laws

As a result, progress towards SDG target 3.6, halving road traffic deaths by 2030, remains a major global challenge.

**Research question.** How do road traffic death rates vary across demographics, regions, and urban versus rural settings? How does the current mean death rate compare with the SDG 3.6 target of 9.1 deaths per 100,000 population?

## 2. Data understanding

**Sources**

- **World Health Organization:** estimated road traffic death rates and death counts by country, from the [Global Status Report on Road Safety 2023](https://www.who.int/teams/social-determinants-of-health/safety-and-mobility/global-status-report-on-road-safety-2023).
- **Statistics Netherlands (CBS):** [road traffic deaths in the Netherlands](https://www.cbs.nl/en-gb/news/2024/15/684-road-traffic-deaths-in-2023), used as an urban comparison case.

**Key variables**

| Variable | Meaning |
|---|---|
| Country or region | Geographic unit |
| Year | Observed year |
| Death rate | Deaths per 100,000 population |
| Population | Total population of each country |
| Total deaths | Derived from the death rate and the population |

**Data quality issues**

- Gaps for some years and demographic groups.
- Duplicate rows.
- Inconsistent reporting, especially in low-income regions.
- Many columns with no analytical value.

**Initial insights**

- Death rates remain above the SDG target of 9.1 per 100,000.
- Low-income regions such as Africa have higher rates.
- Rural countries with poor infrastructure report higher rates than highly urbanised countries such as the Netherlands.

## 3. Data preparation

- **Excel:**
  - Removed duplicate rows and standardised column names.
  - Filtered the data to low-income countries, keeping global figures for comparison.
  - Excluded high-income countries, except the Netherlands, which was kept as the urban case study.
- **Python:**
  - Calculated total deaths per country as death rate × population ÷ 100,000.
  - Created a column per age group and split the data by year (2021, 2022 and 2023).
  - Rounded the results.
- **Power Query and measures:**
  - Removed columns with many missing values.
  - Created measures for the visuals, including the standard deviations and covariance needed for the correlation between population and death rate.

## 4. Modelling

No predictive model was built: the dashboard is descriptive and exploratory. The analytical element is a correlation coefficient between population size and death rate per 100,000. It is calculated with Power BI measures from the covariance and standard deviations, and was checked against the same calculation in Python.

To make the visuals meaningful, the data was segmented by year and grouped into categories. A new variable, total deaths, was added, along with mean and median death rates for demographic and regional comparisons.

## 5. Evaluation

The dashboard meets its objectives:

- **Coverage:** it shows death rates per 100,000, demographic differences and trends over 2021–2023.
- **Urban versus rural:** it compares rural countries with the Netherlands as an urban case.
- **Correlation:** population and death rate have a **weak negative correlation**, so larger populations don't mean higher death rates. Several countries with far smaller populations than the Netherlands have much higher median death rates, which points to infrastructure and socio-economic factors.

**Limitations**

- Missing data for some countries and groups needed imputation or exclusion.
- Only three years are covered (2021–2023), too short for long-term trends.
- The correlation leaves out other factors, such as road quality, vehicle safety and enforcement.
- The focus on low-income countries limits how well the findings apply to high-income countries.
- There is no predictive component.

**Improvements**

- Add variables on road infrastructure quality, vehicle ownership and traffic enforcement.
- Cover a longer period, to evaluate trends and interventions.
- Add regression or machine learning models to forecast deaths and rank the drivers.
- Include more high-income countries for comparison.
- Add more slicers, for example by region, age group and gender.

## 6. Deployment

The plan was to publish the dashboard to Power BI Service and share it through a link with restricted access.

Updates would require two steps:

1. Download newer WHO and CBS data.
2. Repeat the Excel and Python preparation, then refresh the dataset in Power BI.

## 7. Future research

- **More data:** sources on road infrastructure, vehicle safety standards and enforcement would explain more of the variation.
- **New techniques:** machine learning or geospatial analysis could predict trends and identify high-risk areas.
- **Fresher data:** regular, more detailed updates would keep the dashboard relevant, especially for low-income regions with inconsistent reporting.

These would help policymakers, NGOs and affected communities direct resources and interventions.
