# Proposal11111

---

## 1. Description of the Dataset

This dataset contains comprehensive records of animals handled by a shelter in or near Long Beach. Each row describes a single animal’s intake and outcome. It includes the following key information:

- **Animal-Specific Details**  
  - **animal_id**: Unique identifier for each animal.  
  - **animal_name**: Name assigned to the animal (if known).  
  - **animal_type**: Species (e.g., dog, cat).  
  - **primary_color**: Main coat color.  
  - **secondary_color**: Secondary coat color (if applicable).  
  - **sex**: Biological sex and alteration status (e.g., male/neutered, female/spayed).

- **Intake Information**  
  - **intake_date**: Date the animal was brought into the shelter.  
  - **intake_condition**: Condition of the animal upon intake (e.g., healthy, injured).  
  - **intake_type**: Broad category of intake (e.g., stray, owner surrender).  
  - **intake_subtype**: Additional details about how the animal was brought in (e.g., seized, walk-in).  
  - **reason_for_intake**: Reason provided for why the animal came to the shelter (e.g., lost, relinquishment).  
  - **crossing**: Possibly indicates cross streets or boundaries where the animal was found or transferred.  
  - **jurisdiction**: The legal area or municipality responsible for the animal’s intake.

- **Outcome Information**  
  - **outcome_date**: Date the animal left the shelter or its status was updated.  
  - **outcome_type**: Description of the animal’s outcome (e.g., adopted, returned to owner, euthanized).  
  - **outcome_subtype**: Additional specificity of the outcome (e.g., foster, transfer).  
  - **outcome_is_dead**: Binary indicator showing if the animal was deceased at outcome.  
  - **was_outcome_alive**: Binary indicator showing if the animal was alive at outcome (inverse of `outcome_is_dead`).

- **Geographical Information**  
  - **latitude**: Numeric latitude coordinate of where the animal was found.  
  - **longitude**: Numeric longitude coordinate of where the animal was found.  
  - **geopoint**: Combined geographic reference (latitude, longitude) for mapping.

The dataset likely contains **several thousand records** and about **15–20 columns**. It was gathered by shelter staff for operational tracking and record-keeping.

---

## 2. Reason for Choosing the Dataset

This dataset is highly suitable for research into **animal shelter outcomes** and **adoption factors** because:

1. **Comprehensive Animal Profiles**: It includes detailed descriptors (type, color, sex), enabling nuanced analyses of which animals are more frequently adopted.  
2. **Geographical Detail**: Latitude and longitude fields allow for spatial analyses (e.g., examining whether particular neighborhoods see more strays of a certain species).  
3. **Outcome Tracking**: Dates and types of outcomes facilitate longitudinal insights (e.g., time in shelter before adoption, reason for intake vs. final outcome).  
4. **Potential for Merging**: The structured nature of key attributes (e.g., breed, intake_reason) makes it easier to incorporate external data if needed.

---

## 3. The Two Research Questions

1. **Question 1**: How does the location (latitude, longitude) relate to the type of animal?  
   - **Motivation**: Determine if certain species (e.g., cats vs. dogs) cluster in specific areas.  
   - **Key Variables**:  
     - **latitude**, **longitude** (numerical)  
     - **animal_type** (categorical)

2. **Question 2**: What factors influence the likelihood of an animal being adopted?  
   - **Motivation**: Discover which attributes are most predictive of successful adoption.  
   - **Key Variables**:  
     - **outcome_type** (filtered for “Adopted”)  
     - **animal_type**, **primary_color**, **sex**, **intake_condition**, **reason_for_intake**

---

## 4. Plan for Answering Each Question

### 4.1. Plan for Question 1: Geographical Correlation with Animal Type

1. **Data Subset/Preparation**  
   - Focus on `latitude`, `longitude`, `animal_type`.  
   - Exclude records missing valid geographical data (or consider an imputation strategy).

2. **Analytical Approach**  
   - **Exploratory Data Analysis (EDA)**:  
     - Scatter plots or heat maps using `latitude` and `longitude` to visualize location clusters.  
     - Color-code or facet by `animal_type` to see if cats/dogs appear in distinct areas.  
   - **Statistical/Clustering Methods**:  
     - Potentially cluster animals by intake location; compare cluster composition by species.

3. **Possible Findings**  
   - Certain species dominating specific neighborhoods.  
   - Insights informing resource allocation, such as targeting spay/neuter campaigns in high-stray areas.

---

### 4.2. Plan for Question 2: Factors Influencing Adoption Likelihood

1. **Data Subset/Preparation**  
   - Filter by `outcome_type` to compare “Adopted” vs. other outcomes (e.g., euthanized, returned to owner).  
   - Include predictors like `animal_type`, `primary_color`, `sex`, `intake_condition`, `reason_for_intake`.

2. **Analytical Approach**  
   - **Descriptive Analysis**: Compute adoption rates for each category of predictor.  
   - **Predictive Modeling**:  
     - **Logistic Regression**: Model adoption (1) vs. non-adoption (0).  
     - Alternatively, tree-based algorithms (e.g., Random Forest) to rank variable importance.

3. **Statistical Tests**  
   - Conduct chi-square or other relevant hypothesis tests for categorical variables.  
   - Examine logistic regression coefficients (sign, p-values) to interpret the direction and significance of each factor.

4. **Visualizations**  
   - Bar charts showing adoption proportions (e.g., by `animal_type`, `intake_condition`).  
   - Coefficient plots highlighting logistic regression results.

5. **Interpretation**  
   - Identify which animal or intake factors (e.g., age, color, reason for intake) correlate strongly with adoption likelihood.  
   - Provide targeted strategies (e.g., marketing campaigns for animals with lower adoption probabilities).

---

## 5. Possible External Data for Merging

- **Breed Popularity Data**: Publicly available breed rankings can be joined (if breed details are derivable from `animal_name` or another column) to see if more popular breeds experience quicker adoptions.  
- **Local Event/Campaign Data**: Track adoption events or public awareness campaigns to see if there’s a corresponding surge in adoption rates.

---

### Summary

This proposal outlines the use of **longbeach.csv** to address two main questions about animal shelter data:

1. **Geographical Distributions**: Determine how **location** (latitude, longitude) correlates with **animal type**.  
2. **Adoption Drivers**: Identify which attributes and circumstances (color, sex, intake condition, reason for intake) increase the chances of an animal being adopted.

With detailed animal, intake, and outcome records — plus geographical coordinates — this dataset offers rich opportunities for statistical and predictive analysis.  
