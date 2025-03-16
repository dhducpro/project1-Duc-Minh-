# Proposal

---

## 1. Description of the Dataset

The dataset, tentatively named **longbeach.csv**, appears to contain intake and outcome information from an animal shelter, presumably located in or near Long Beach. Each row represents an animal intake or outcome record, and includes attributes such as:

- **Latitude** and **Longitude**: Numeric coordinates indicating where the animal was found or picked up.  
- **Animal Type**: Categorical feature indicating species (e.g., dog, cat).  
- **Primary Color**: Categorical feature indicating the animal’s main color (e.g., black, brown).  
- **Sex**: Categorical feature indicating male/female and whether altered (e.g., neutered/spayed).  
- **Intake Condition**: Categorical feature describing the condition of the animal at intake (e.g., healthy, injured).  
- **Reason for Intake**: Categorical feature describing why the animal came into the shelter (e.g., stray, owner surrender).  
- **Outcome Type**: Categorical feature describing what happened to the animal after intake (e.g., adopted, returned to owner).

Although the specific provenance details are not fully documented here, we can infer that the data was collected by shelter staff for operational and record-keeping purposes. The dataset’s **dimensions** (number of rows and columns) will be confirmed upon exploratory analysis; we can expect potentially several thousand records and around 10–15 columns, typical for shelter operations data.

---

## 2. Reason for Choosing the Dataset

This dataset is ideal for investigating questions related to **animal shelter outcomes** and **factors affecting adoption** because it:

1. **Captures Critical Intake and Outcome Variables**: Includes both intake details and final outcomes.
2. **Has Geographical Information**: Allows us to explore how location (latitude, longitude) might relate to certain animal types or patterns in intakes.
3. **Enables Analysis of Adoption Predictors**: Contains outcome labels (e.g., “Adopted”) and various animal attributes (type, color, etc.) for identifying key influences on adoption rates.

---

## 3. The Two Research Questions

1. **Question 1**: How does the location (latitude, longitude) relate to the type of animal?  
   - **Motivation**: Investigate whether certain animal types (e.g., cats vs. dogs) are more commonly found in particular neighborhoods or geographic regions.  
   - **Key Variables**:  
     - **Latitude, Longitude** (numerical)  
     - **Animal Type** (categorical: dog, cat, etc.)

2. **Question 2**: What factors influence the likelihood of an animal being adopted?  
   - **Motivation**: Identify which attributes of an animal or aspects of its intake most strongly predict successful adoption.  
   - **Key Variables**:  
     - **Outcome Type** (filtering for “Adopted”)  
     - **Animal Type**  
     - **Primary Color**  
     - **Sex**  
     - **Intake Condition**  
     - **Reason for Intake**

---

## 4. Plan for Answering Each Question

### 4.1. Plan for Question 1: Geographical Correlation with Animal Type

1. **Data Subset/Preparation**  
   - Identify relevant columns: `latitude`, `longitude`, `animal_type`.  
   - Exclude records with missing or invalid latitude/longitude.

2. **Analytical Approach**  
   - **Exploratory Data Analysis (EDA)**: Generate descriptive statistics and create visualizations (e.g., scatter plots of latitude vs. longitude, colored by animal type).  
   - **Statistical Tests**: Optionally use cluster analysis or chi-square tests on binned geographic data to see if distributions differ by animal type.

3. **Potential Outcomes**  
   - Reveal whether certain animal types are more prevalent in specific geographic regions.  
   - Inform targeted interventions (e.g., spay/neuter campaigns) in areas with high numbers of specific animal intakes.

---

### 4.2. Plan for Question 2: Factors Influencing Adoption Likelihood

1. **Data Subset/Preparation**  
   - Filter the dataset by `outcome_type` to distinguish “Adopted” vs. other outcomes.  
   - Ensure relevant features (`animal_type`, `primary_color`, `sex`, `intake_condition`, `reason_for_intake`) are available and clean.

2. **Analytical Approach**  
   - **Descriptive Analysis**: Compute adoption rates for each factor (e.g., by animal type, color). Create bar charts to visualize these rates.  
   - **Predictive Modeling**:  
     - Use **Logistic Regression** to model “Adopted” (1) vs. “Not Adopted” (0).  
     - Examine regression coefficients to see which factors significantly affect adoption odds.  
     - Optionally, use tree-based models (e.g., Random Forest) to confirm variable importance.

3. **Statistical Tests**  
   - Use chi-square or other relevant tests for categorical predictors to see if differences in adoption rates are statistically significant.

4. **Visualizations**  
   - Bar charts showing adoption proportions by factor (animal type, color, etc.).  
   - Plots of logistic regression coefficients indicating direction (positive/negative) and relative magnitude of influence.

5. **Interpretation**  
   - Determine which characteristics (e.g., animal type, color, intake condition) most strongly correlate with adoption.  
   - Provide recommendations (e.g., marketing campaigns for less-adopted animals).

---

## 5. Possible External Data for Merging

- **Breed Popularity Data**: Publicly available breed rankings could be matched on the breed or category level to see if popular breeds are adopted more quickly.  
- **Event or Campaign Data**: Information about local adoption events or public awareness campaigns could be joined by date to see if these events influence adoption rates.

---

### Summary

By leveraging **longbeach.csv**, this proposal outlines a two-pronged research approach:

1. Examine how **location** relates to **animal type** via mapping and statistical clustering.  
2. Determine which factors most strongly predict **adoption** using logistic regression or related methods.  

Through these analyses, we aim to uncover actionable insights to optimize animal rescue and adoption strategies.
