# Street Lighting's Impact on Urban Sexual Assaults in Louisville Metro (2023)

## Introduction

Original author: Andrew Mavizha, LMPHW Intern Fall 2025.
This project investigates the relationship between street lighting infrastructure and sexual assault incidents in Louisville, Kentucky during 2023. The analysis combines data from city 311 service requests for streetlight maintenance with official sexual assault crime reports to examine whether areas with higher concentrations of streetlight requests correlate with sexual assault patterns, particularly during nighttime hours.

The project aims to:
- Analyze the geographic and temporal distribution of sexual assault incidents across council districts
- Examine streetlight infrastructure requests and their patterns across Louisville
- Explore potential correlations between streetlight density and assault rates
- Provide data-driven insights for urban safety planning and resource allocation

## Installation

### Prerequisites
- Python 3.8 or higher
- Jupyter Notebook or Jupyter Lab
- pip or conda package manager
- ArcGis software

### Required Dependencies

The project requires the following Python packages:
```
pandas
numpy
scikit-learn
imbalanced-learn
matplotlib
plotnine
seaborn
joblib
category-encoders
xgboost
lightgbm
scipy
```

### Setup Instructions

1. Clone the repository:
```bash
git clone <repository-url>
cd Street-lighting-impact-on-urban-sexual-assaults-in-Louisville-Metro-2023-main
```

2. Create a virtual environment (recommended):
```bash
python -m venv venv
venv\Scripts\activate  # On Windows
# or
source venv/bin/activate  # On macOS/Linux
```

3. Install required packages:
```bash
pip install pandas numpy scikit-learn imbalanced-learn matplotlib plotnine seaborn joblib category-encoders xgboost lightgbm scipy
```

4. Ensure you have the following data files in the project directory:
   - `assault incidents data.csv` - Sexual assault incident records
   - `311_2023.csv` - City 311 service requests (including streetlight requests)

## Usage

The project consists of three main Jupyter notebooks that should be run in sequence:

### 1. Sexual Assaults Analysis (`sexual assaults analysis.ipynb`)
This notebook performs exploratory data analysis on sexual assault incidents:
- Loads and cleans the assault incident dataset
- Filters for 2023 incidents and nighttime occurrences.
- Analyzes assault patterns by:
  - Gender of victims
  - Age distribution
  - Geographic distribution (council districts)
  - Temporal trends (monthly patterns)
  - Race/age demographics

**Run:**
```bash
jupyter notebook "sexual assaults analysis.ipynb"
```

### 2. Street Lights Analysis (`streetlights analysis.ipynb`)
This notebook analyzes streetlight infrastructure and maintenance requests:
- Loads and processes the 311 service request data
- Filters for streetlight-related requests
- Analyzes streetlight request patterns by:
  - Council district distribution
  - Monthly trends
  - Request frequency and status
  - Top service request categories

**Run:**
```bash
jupyter notebook "streetlights analysis.ipynb"
```

### 3. Combined Analysis (`Combined Analysis.ipynb`)
This notebook merges and correlates the two datasets:
- Combines assault and streetlight data at the district and monthly level
- Performs statistical analysis including:
  - Correlation tests (Pearson, Spearman, Kendall)
  - Normality assessments (Shapiro-Wilk tests)
  - LOWESS regression analysis
  - Heatmaps showing the relationship between streetlights and assaults
  - Identifies districts with both high streetlight requests and high assault rates

**Run:**
```bash
jupyter notebook "Combined Analysis.ipynb"
```

## Code Overview

### Project Structure
```
Street-lighting-impact-on-urban-sexual-assaults-in-Louisville-Metro-2023-main/
├── sexual assaults analysis.ipynb        # Sexual assault data analysis
├── streetlights analysis.ipynb           # Streetlight infrastructure analysis
├── Combined Analysis.ipynb               # Integrated analysis and correlation study
├── images/                               # Output visualizations and charts
├── processed_data/                       # Intermediate processed datasets
├── artifacts/                            # Generated reports and outputs
└── report_streetlightproject.pdf         # Summary report
```

### Data Processing Workflow

1. **Data Loading & Cleaning**
   - Both notebooks load raw CSV files
   - Handle missing values and duplicates
   - Convert date/time columns to proper datetime formats

2. **Feature Engineering**
   - Extract temporal features (hour, month, year) from timestamps
   - Create nighttime flag for sexual assaults incidents
   - Normalize district identifiers across datasets

3. **Exploratory Analysis**
   - Descriptive statistics for each variable
   - Distribution analysis with histograms and Q-Q plots
   - Categorical summaries by district, gender, age, and time

4. **Correlation & Regression**
   - Statistical correlation analysis between streetlight and assault percentages
   - Normality testing to determine appropriate statistical tests
   - LOWESS (Locally Estimated Scatterplot Smoothing) regression visualization

5. **Visualization**
   - Uses plotnine (ggplot2-style grammar of graphics) for publication-quality plots
   - Heatmaps showing district-level relationships
   - Time series plots for temporal trends
   - Distribution plots and Q-Q plots for statistical validation

### Key Variables

**Sexual Assault Dataset:**
- `Offense Start Date` - Date and time of incident
- `Sex` - Gender of victim
- `Age` - Age of victim
- `COUNDIST` - Council district
- `Case Status` - Investigation status
- `Location Category` - Type of location (street, home, etc.)

**Streetlight Dataset (311 Service Requests):**
- `requested_datetime` - Date/time of request
- `service_name` - Type of service request
- `service_request_id` - Unique request identifier
- `council_district` - Geographic council district
- `status` - Request status (open, closed, in-progress)

## Images Folder

All visualizations and charts generated by the analysis notebooks are saved in the `images/` folder. The 15 comprehensive visualizations provide detailed analysis of sexual assault patterns and streetlight infrastructure across Louisville.

### Key Visualizations

#### 1. City Service Requests Overview

![Top Twenty City Service Requests](images/01-Top-Twenty-City-Service-Requests-Visualization-Showing-Community-Demand-Patterns-And-Providing-Context-For-Analyzing-Street.png)

**Top Twenty City Service Requests** - A comprehensive visualization displaying the 20 most frequently requested city services in Louisville's 311 system, providing essential context for understanding where streetlight requests rank among community demands and highlighting the prevalence of infrastructure maintenance needs across the city.

#### 2. Streetlight Requests by Council District

![Street Light Service Requests by District](images/02-Percentage-Distribution-Of-Street-Light-Service-Requests-By-Council-District-Highlighting-Highest-Concentrations-In-Distric.png)

**Street Light Service Requests by Council District** - Detailed percentage distribution of streetlight service requests across all council districts, identifying geographic hotspots where streetlight infrastructure concerns are most prevalent and revealing which districts have the highest demand for lighting maintenance.

#### 3. Monthly Trends in Streetlight Requests

![Monthly Street Light Trends](images/03-Monthly-Trend-Analysis-Of-Street-Light-Service-Request-Percentages-Showing-Seasonal-Variations-Peaks-During-Spring-And-Fall.png)

**Monthly Trend Analysis of Street Light Requests** - Temporal analysis showing how streetlight service request percentages fluctuate throughout 2023, revealing seasonal patterns and identifying peak periods when lighting infrastructure concerns are most acute, with notable variations across different months.

#### 4. Streetlight Service Request Status Overview

![Street Light Service Request Status](images/04-Comprehensive-Display-Of-Street-Light-Service-Requests-Combining-Pie-Chart-Status-Percentages-With-Monthly-Closed-And-Open-.png)

**Comprehensive Street Light Service Request Status** - A multi-faceted visualization combining pie chart status percentages (open, closed, in-progress) with monthly trends of closed and open requests, demonstrating municipal response efficiency and the status distribution of streetlight maintenance work throughout 2023.

#### 5. Nighttime Sexual Assaults Victims Gender Distribution

![Nighttime Assault Victims Gender](images/05-Bar-Chart-Showing-Nighttime-Sexual-Assault-Victim-Gender-Distribution-For-2023-Highlighting-The-Extremely-High-Proportion-O.png)

**Nighttime Sexual Assaults Victims Gender Distribution** - Bar chart clearly illustrating the stark gender disparity in sexual assault victimization during nighttime hours in 2023, with females representing an overwhelmingly high proportion of victims compared to male victims.

#### 6. Nighttime Sexual Assaults Victims by Age Group

![Age Distribution of Nighttime Victims](images/06-Detailed-Pie-Chart-Illustrating-Percentage-Distribution-Of-Nighttime-Victims-By-Age-Group-For-2023-Showing-Strong-Concentra.png)

**Nighttime Sexual Assault Victims by Age Group Distribution** - Pie chart providing percentage distribution of nighttime sexual assault victims across different age groups in 2023, showing strong concentration among working-age and young adult demographics, with insights into age-based vulnerability patterns.

#### 7. Nighttime Sexual Assaults  Victims by Race

![Race Distribution of Nighttime Victims](images/07-Comprehensive-Visualization-Of-Nighttime-Victim-Race-Percentages-For-2023-Showing-Significant-Representation-Among-White-An.png)

**Nighttime Sexual Assaults Victims Race Distribution** - Comprehensive visualization of racial demographics among nighttime sexual assault victims in 2023, demonstrating representation across multiple racial categories and highlighting disparities in victimization patterns across different racial groups.

#### 8. Sexual Assaults Race and Age Group Demographics

![Race and Age Demographics](images/08-Race-And-Age-Group-Distribution-Of-Nighttime-Victims-For-2023-Showing-Significant-Differences-Across-Racial-Categories-And-.png)

**Race and Age Group Demographics of Victims** - Combined visualization showing the intersection of race and age among nighttime sexual assault victims in 2023, revealing significant differences in victimization patterns across both racial categories and age groups, providing nuanced demographic insights.

#### 9. Sexual Assaults Incidents by Council District

![Sexual Assaults Incidents by District](images/09-Detailed-Visualization-Of-Nighttime-Incident-Frequencies-By-District-For-2023-Highlighting-High-Risk-Zones-Such-As-District.png)

**Sexual Assaults Nighttime Incident Frequencies by Council District** - Detailed visualization mapping nighttime sexual assault incident counts across all council districts in 2023, identifying high-risk zones and geographic clusters with elevated assault rates, enabling targeted intervention and resource allocation strategies.

#### 10. Sexual Assaults Incidents Locations

![Incident Locations](images/10-Comprehensive-Visualization-Of-Sexual-Assault-Locations-Revealing-That-Most-Incidents-Occur-In-Homes-Or-Residential-Apartme.png)

**Sexual Assaults Incidents Location Analysis** - Comprehensive visualization showing the distribution of assault incidents by location type, revealing that the majority of incidents occur in homes or residential apartments, with important implications for prevention strategies and victim support services.

#### 11. Dual-Line Chart: Monthly Trends Comparison

![Monthly Trends Comparison](images/11-Dual-Line-Chart-Illustrating-How-Nighttime-Sexual-Assault-Incidents-And-Streetlight-Requests-Change-Monthly-In-2023-To-Reve.png)

**Monthly Trends: Sexual Assaults vs Streetlight Requests** - Dual-line chart comparing how nighttime sexual assault incidents and streetlight service requests fluctuate monthly throughout 2023, revealing temporal synchronization patterns and potential seasonal correlations between the two variables.

#### 12. Geographic Heatmap: Sexual Assaults and Streetlight Requests

![Geographic Heatmap Analysis](images/12-Detailed-Heatmap-And-Point-Distribution-Of-2023-Sexual-Assaults-And-Streetlight-Outage-Reports-To-Identify-Geographic-Corre.png)

**Geographic Heatmap: Sexual Assaults & Streetlight Requests** - Detailed heatmap and point distribution visualization mapping both 2023 sexual assaults and streetlight outage reports spatially, enabling identification of geographic correlations and clusters where high assault rates coincide with streetlight infrastructure deficiencies.

#### 13. Relationship: Streetlight vs Assault Percentages

![Streetlight vs Sexual Assaults Correlation](images/13-Scatterplot-Showing-Relationship-Between-Streetlight-Percentage-And-Nighttime-Assault-Percentage-With-LOWESS-Smoother-And-S.png)

**Streetlight Percentage vs Sexual Assaults Percentage Relationship** - Scatterplot analysis showing the relationship between streetlight request percentages and nighttime assault percentages across districts, including LOWESS smoother curve and statistical significance testing to assess correlation strength.

#### 14. Lagged Analysis: Streetlight Requests vs Sexual Assaults

![Lagged Correlation Analysis](images/14-Lagged-Scatterplot-Comparison-Showing-How-Streetlight-Request-Percentages-Relate-To-Nighttime-Assault-Rates-Using-LOWESS-Tr.png)

**Lagged Analysis: Temporal Relationship** - Lagged scatterplot comparison examining how streetlight request percentages in one time period relate to nighttime sexual assaults rates in subsequent periods, using LOWESS trends to identify potential causal or predictive relationships between infrastructure concerns and assault patterns.

#### 15. Robust Regression Model Results

![Robust Regression Analysis](images/15-Model-Summary-From-Robust-Linear-Regression-Showing-How-Streetlight-Coverage-And-Different-Environmental-Context-Variables-.png)

**Robust Regression Model Summary** - Statistical model summary from robust linear regression analysis showing how streetlight coverage and different environmental context variables predict nighttime sexual assault rates, providing quantitative evidence of the strength and significance of relationships in the data.

## Results Summary

The analysis reveals:
- Significant geographic variation in both streetlight requests and assault incidents across council districts
- Temporal clustering of assaults during nighttime hours.
- Potential associations between areas with high streetlight concerns and elevated assault rates
- Demographic patterns in sexual assaults crime across age, gender, and race

## Methodology Notes

- **Time Period**: 2023
- **Nighttime Definition**: The timeframe between the sunset and the sunrise of the following day.
- **Geographic Unit**: Council districts in Louisville metro area
- **Statistical Tests**: Shapiro-Wilk (normality), Pearson/Spearman correlations, LOWESS regression

## Dependencies & Libraries

- **pandas**: Data manipulation and analysis
- **numpy**: Numerical computing
- **matplotlib & seaborn**: Statistical visualization
- **plotnine**: ggplot2-inspired grammar of graphics for Python
- **scikit-learn**: Machine learning preprocessing and analysis
- **scipy**: Statistical functions and tests
- **joblib**: Efficient computation and caching

## Report

A comprehensive PDF report of the analysis findings is available in `report_streetlightproject.pdf`.

## Future Work

Potential extensions to this analysis:
- Predictive modeling for assault risk based on streetlight density
- Temporal analysis of assault trends before/after streetlight improvements
- Integration of additional socioeconomic variables
- Machine learning models for district-level risk assessment
- Network analysis of spatiotemporal patterns

## Contact & Attribution

For questions or contributions regarding this analysis, please contact the project team or submit an issue to the repository.

---

Last Updated: December 2023
Data Source: Louisville Metro Police Department & 311 Service Requests



