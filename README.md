# Street Lighting's Impact on Urban Sexual Assaults in Louisville Metro (2023)

## Introduction


### Original author: Andrew Mavizha, LMPHW Intern Fall 2025.
### Updates added by Angela Graham - Jan 2026

This project investigates the relationship between street lighting infrastructure and sexual assault incidents in Louisville, Kentucky during 2023. The analysis combines data from city 311 service requests for streetlight maintenance with official sexual assault crime reports to examine whether areas with higher concentrations of streetlight requests correlate with sexual assault patterns, particularly during nighttime hours.
To ensure precise identification of nighttime incidents, sunset and sunrise times were obtained from the U.S. Naval Observatory for each day in 2023. The `sunset&sunrise_times.txt` file contains these daily records, which were used to accurately define the nighttime window (from sunset to sunrise of the following day) for temporal analysis across the entire year.
The project aims to:
- Analyze the geographic and temporal distribution of sexual assault incidents across council districts
- Examine streetlight infrastructure requests and their patterns across Louisville
- Explore potential correlations between streetlight density and assault rates
- Provide data-driven insights for urban safety planning and resource allocation

### Data Sources
- **Sexual Assault Incidents**: Louisville Metro Police Department
- **311 Service Requests**: Louisville Metro Government 311 system
- **Sunset and Sunrise Times**: U.S. Naval Observatory (available in `sunset&sunrise_times.txt`)

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
os
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
   - `streetlightcouncil.csv` - Sexual assault incident records (open records provided by LMPD, 2018-2023. Includes Metro Council District number spatially joined to data)
   - `sunset&sunrise_times{year}.txt` - Data downloaded from https://aa.usno.navy.mil/data/RS_OneYear for Louisville, KY 2018-2023 (one file per year)
   - `DST.txt` - Data downloaded from https://aa.usno.navy.mil/ with start and stop times for daylight savings every year 2018-2023
   - `crime_{year}.csv` - Data downloaded from https://data.louisvilleky.gov/. Louisville Metro Crime Data for years 2018-2023.
   - `311_2023.csv` - City 311 service requests (including streetlight requests)

## Usage

The project consists of three main Jupyter notebooks that should be run in sequence:

### 1a. Sexual Assaults Data Prep (`sexual_assaults_dataprep.ipynb`)
This notebook performs basic data preperation tasks on the LMPD data
- Loads data set and performs basic cleaning to date/time
- Processes the sunset/sunrise data into a dataframe and adjusts for daylight savings, adds a nighttime flag 
- Merges in the location/premise type variable from the open data records

**Run:**
```bash
jupyter notebook "sexual_assaults_dataprep.ipynb"
```

### 1b. Sexual Assaults Analysis (`sexual assaults analysis.ipynb`)
This was Andrew's notebook that performs exploratory data analysis on sexual assault incidents.  There is some redundancy with the data prep file. 
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


All visualizations and charts generated by the analysis notebooks are saved in the `images/` folder. These comprehensive visualizations provide detailed analysis of sexual assault patterns and streetlight infrastructure across Louisville.

### Key Visualizations

#### Streetlight Request Distribution

**Top Twenty City Service Requests**

![Top Service Requests](images/top20-service-requests.png)

Overview of the 20 most frequently requested city services in Louisville's 311 system, showing the prevalence and ranking of streetlight infrastructure requests among community demands.

**Street Light Service Requests by Council District**

![Streetlight Requests by Districts](images/streetlights-requests-by-districts.png)

Geographic distribution of streetlight service requests across council districts, identifying hotspots where infrastructure concerns are most prevalent.

**Monthly Trend Analysis of Street Light Requests**

![Monthly Streetlight Trends](images/trends-streelighting-requests.png)

Temporal patterns showing how streetlight service request percentages fluctuate throughout 2023, revealing seasonal variations and peak periods of infrastructure concerns.

**Street Light Service Request Status Overview**

![Streetlight Request Status](images/status-of-streetlights-request.png)

Comprehensive display of streetlight service requests showing status percentages and temporal distribution of closed and open requests throughout 2023.

#### Sexual Assault Demographics

**Nighttime Sexual Assault Victims Gender Distribution**

![Assault Victims Gender Distribution](images/assaults-gender.png)

Bar chart illustrating the gender disparity in nighttime sexual assault victimization for 2023, showing the disproportionate impact on female victims.

**Nighttime Sexual Assault Victims by Age Group**

![Assault Victims Age Distribution](images/assaults-age-distribution.png)

Distribution showing how nighttime sexual assault victims are distributed across different age groups in 2023, identifying vulnerable age demographics.

**Nighttime Sexual Assault Victims Race Distribution**

![Assault Victims Race Distribution](images/races-of-assault-victims.png)

Demographic breakdown showing racial composition of nighttime sexual assault victims in 2023 and victimization patterns across racial groups.

**Race and Age Group Demographics of Victims**

![Race and Age Demographics Combined](images/race-age-of%20assaults.png)

Combined analysis showing the intersection of race and age among nighttime sexual assault victims, revealing nuanced victimization patterns across demographic categories.

#### Geographic and Incident Analysis

**Sexual Assault Incident Frequencies by Council District**

![Assaults by Districts](images/assaults-by-districts.png)

Geographic mapping of nighttime sexual assault incident counts across all council districts in 2023, identifying high-risk zones for targeted intervention.

**Sexual Assault Case Status Overview**

![Assault Case Status](images/status-of-assault-cases.png)

Distribution of assault case statuses, providing insights into investigation outcomes and case resolution patterns.

#### Correlation and Statistical Analysis

**Heatmap: Streetlight Requests and Sexual Assault Correlation**

![Heatmap Combined Analysis](images/heatmap-for-combined.png)

Detailed heatmap visualization showing the relationship and potential correlations between streetlight service requests and sexual assault incidents across geographic areas.

**Robust Regression Model Analysis**

![Robust Regression Results](images/robust-regression.png)

Statistical regression results showing how streetlight coverage and environmental variables predict nighttime sexual assault rates, providing quantitative evidence of relationships in the data.
>>>>>>> upstream/main

## Results Summary

The analysis reveals:
- Significant geographic variation in both streetlight requests and assault incidents across council districts
- Temporal clustering of assaults during nighttime hours.
- Potential associations between areas with high streetlight concerns and elevated assault rates
- Demographic patterns in sexual assaults crime across age, gender, and race

## Methodology Notes

- **Time Period**: 2023
<<<<<<< HEAD
- **Nighttime Definition**: The timeframe between the sunset and the sunrise of the following day.
=======
- **Nighttime Definition**: The timeframe between the sunset and the sunrise of the following day. Sunset and sunrise times were recorded for different days throughout 2023 to accurately account for seasonal variations in daylight hours and ensure precise identification of nighttime incidents.
>>>>>>> upstream/main
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

