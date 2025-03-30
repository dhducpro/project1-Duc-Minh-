# Revised Proposal

## 1. Description of the Dataset

The dataset, **longbeach.csv**, contains intake and outcome records from an animal shelter in Long Beach. Each row represents an animal's journey through the shelter, with attributes including:

- **Latitude** and **Longitude**: Numeric coordinates of where the animal was found.
- **Animal Type**: Categorical (e.g., dog, cat, bird, reptile).
- **Primary Color**: Main color (e.g., black, brown).
- **Secondary Color**: Additional color, if present (e.g., white, gray).
- **Sex**: Gender and alteration status (e.g., Neutered, Spayed, Female, Male).
- **Date of Birth (dob)**: For calculating age.
- **Intake Date** and **Outcome Date**: Entry and exit dates for time-in-shelter calculations.
- **Intake Condition**: Condition at intake (e.g., normal, injured severe).
- **Intake Type**: Reason for intake (e.g., stray, owner surrender).
- **Intake Subtype**: Specific details of intake (e.g., field, OTC).
- **Outcome Type**: Final outcome (e.g., adopted, euthanized, transferred).

The dataset likely includes thousands of records, collected by shelter staff for operational purposes, offering a robust foundation for spatial and predictive analyses.

---

## 2. Reason for Choosing the Dataset

This dataset is well-suited for the proposed research because it:

1. **Provides Detailed Intake and Outcome Data**: Enables exploration of factors influencing shelter outcomes.
2. **Includes Geographical Coordinates**: Facilitates spatial analysis of animal distributions across administrative areas.
3. **Contains Rich Animal Attributes**: Supports in-depth study of adoption predictors like age, color, and shelter stay duration.

---

## 3. The Two Research Questions

### Research Question 1
**How does human population density relate to the distribution of animal types (e.g., cats vs. dogs) across different administrative areas, and what insights can this provide for targeted animal welfare programs?**

- **Motivation**: Understanding why certain animal types are more prevalent in specific areas—beyond mere clustering—can reveal underlying socio-economic or environmental factors (e.g., population density, urban vs. rural settings). This can guide targeted interventions like spay/neuter campaigns or adoption drives in high-stray neighborhoods.
- **Key Variables**:
  - **Latitude, Longitude** (mapped to administrative areas)
  - **Animal Type** (categorical: dog, cat, etc.)
  - **External Population Density** (continuous, per administrative area)

### Research Question 2
**What factors, including animal attributes and shelter stay duration, influence the likelihood of an animal being adopted?**

- **Motivation**: Identifying predictors of adoption—such as age, time in shelter, or alteration status—can help shelters optimize strategies, such as prioritizing marketing for animals with lower adoption chances (e.g., older black cats).
- **Key Variables**:
  - **Outcome Type** (binary: Adopted vs. Not Adopted)
  - **Animal Type**
  - **Primary Color**, **Secondary Color**
  - **Sex** (including alteration status)
  - **Age** (derived from dob)
  - **Shelter Stay Duration** (outcome_date - intake_date)
  - **Intake Condition**, **Intake Type**, **Intake Subtype**

---

## 4. Plan for Answering Each Question

### 4.1. Plan for Research Question 1: Population Density and Animal Type Distribution

#### Data Preparation
- **Geographical Mapping**: Use latitude and longitude to assign each record to an administrative area (e.g., districts or neighborhoods) via geocoding or spatial joining with a shapefile of Long Beach administrative boundaries.
- **External Data**: Obtain population density data for each administrative area from sources like U.S. Census Bureau datasets.
- **Cleaning**: Exclude records with missing or invalid coordinates.

#### Analytical Approach
- **Exploratory Data Analysis (EDA)**:
  - Calculate the ratio of animal types (e.g., cat-to-dog ratio) per administrative area.
  - Compare these ratios to population density to identify correlations (e.g., higher stray cat rates in densely populated urban zones).
- **Visualization**:
  - Create **choropleth maps** where administrative areas are shaded by animal type ratios or stray density, overlaid with population density data for visual comparison.
  - Group individual data points into larger points per administrative area to reduce noise and improve readability.
- **Statistical Analysis**:
  - Use correlation tests (e.g., Pearson) to quantify the relationship between population density and animal type ratios.
- **Clustering**:
  - Apply **DBSCAN** (Density-Based Spatial Clustering of Applications with Noise) to identify areas with unusually high stray rates relative to population density. DBSCAN is preferred for spatial data as it handles noise well and doesn’t require specifying cluster numbers upfront, unlike **K-means**, which assumes spherical clusters and may struggle with irregular spatial patterns.

#### Potential Outcomes
- Identify neighborhoods with high stray animal rates disproportionate to their population density, suggesting areas needing targeted spay/neuter or adoption programs.
- Uncover why these patterns exist (e.g., dense urban areas may lack resources for pet retention), informing resource allocation.

---

### 4.2. Plan for Research Question 2: Factors Influencing Adoption Likelihood

#### Data Preparation
- **Feature Engineering**:
  - Calculate **Age** by subtracting `dob` from `intake_date`.
  - Compute **Shelter Stay Duration** (in days) as `outcome_date` - `intake_date`.
- **Data Subset**:
  - Filter for records with valid `outcome_type`, coding as binary (1 = Adopted, 0 = Not Adopted).
  - Ensure all predictors (`animal_type`, `primary_color`, `secondary_color`, `sex`, `intake_condition`, `intake_type`, `intake_subtype`, `age`, `shelter_stay_days`) are clean and encoded (e.g., one-hot encoding for categorical variables).
- **Handling Missing Data**: Impute or exclude missing values as needed (e.g., median age for missing `dob`).

#### Analytical Approach
- **Descriptive Analysis**:
  - Compute adoption rates by attribute (e.g., by color, age group, alteration status).
  - Analyze relationships, such as how shelter stay duration varies by age or color (e.g., “Adult black cats wait 20% longer than other cats”).
- **Predictive Modeling**:
  - Use **Logistic Regression** as a baseline to model adoption likelihood, interpreting coefficients for feature impact (e.g., positive coefficient for “Neutered” indicates higher adoption odds).
  - Explore **Random Forest** to capture non-linear relationships and rank feature importance (e.g., age vs. shelter stay).
- **Statistical Tests**:
  - Apply chi-square tests to assess associations between categorical predictors (e.g., `secondary_color`, `sex`) and adoption.
- **External Data**:
  - Merge with American Kennel Club (AKC) breed popularity rankings (for dogs) to test if trendy breeds have shorter shelter stays.

#### Visualizations
- **Bar Charts**: Adoption rates by attribute (e.g., color, alteration status).
- **Box Plots**: Shelter stay duration by age group or animal type.
- **Feature Importance Plots**: From Random Forest, highlighting top predictors.

#### Interpretation
- Identify key adoption predictors (e.g., younger animals or altered pets) and provide actionable recommendations (e.g., promote older animals with longer shelter stays).

---

## 5. Possible External Data for Merging

### Population Density Data
- **Source**: U.S. Census Bureau or local government demographic datasets.
- **Integration**: Match by administrative area names or codes to the geocoded shelter data.
- **Purpose**: Correlate human population density with animal type distributions to identify high-stray areas and underlying socio-economic factors.

### Breed Popularity Data
- **Source**: American Kennel Club (AKC) annual breed popularity rankings.
- **Integration**: Map AKC breed names to `animal_type` (for dogs) using approximate matching or manual categorization.
- **Purpose**: Assess if popular breeds are adopted faster, aiding marketing strategies for less popular breeds.

### Additional Considerations
- **Local Campaign Data**: Check availability of adoption event records from Long Beach shelter archives or local animal welfare organizations. If unavailable, analyze temporal adoption trends (e.g., seasonal patterns) as a proxy.
- **Socio-Economic Data**: Optionally include income levels or urban/rural classifications from census data to enrich Question 1’s analysis.

---

## Summary

This revised proposal leverages **longbeach.csv** to:

1. **Research Question 1**: Investigate how population density influences animal type distributions across administrative areas using choropleth maps and DBSCAN clustering, providing insights for targeted welfare programs.
2. **Research Question 2**: Model adoption likelihood with enhanced predictors (e.g., age, shelter stay duration, alteration status) via logistic regression and Random Forest, integrating breed popularity data to optimize shelter strategies.
