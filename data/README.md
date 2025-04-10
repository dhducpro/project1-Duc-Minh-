# Metadata Summary

## Provenance:
- **Source**: The dataset is presumably provided by a local authority or animal welfare organization within the Long Beach area. The details on animal types, intake conditions, and outcomes suggest that this dataset is used to monitor and manage the intake, health, and eventual outcomes for animals in the region.
- **Creation Date**: The dataset contains various dates spanning from 2013 to 2023, with the most recent data recorded in 2023.
- **Data Collection Method**: Data appears to have been gathered through observations and records of animals brought in, tracked by their IDs and associated conditions.
- **Update Frequency**: The dataset includes animal intake and outcome data, suggesting regular updates as animals are rescued, treated, and released or euthanized.

## Codebook:

### Columns:

1. **animal_id**: Unique identifier for the animal (e.g., A693708).
2. **animal_name**: Name of the animal (if available, e.g., *charlien). Some entries are missing names.
3. **animal_type**: The species or type of animal (e.g., dog, reptile, bird, cat).
4. **primary_color**: The primary color of the animal's coat (e.g., white, brown, green).
5. **secondary_color**: A secondary color of the animal, if applicable.
6. **sex**: The sex of the animal (e.g., Female, Unknown).
7. **dob**: Date of birth of the animal (if known).
8. **intake_date**: Date the animal was admitted to the facility.
9. **intake_condition**: Condition of the animal at intake (e.g., ill, injured, normal).
10. **intake_type**: Type of intake (e.g., stray, wildlife).
11. **age_upon_intake**: The age of the animal at intake (e.g., Young, Adult).
12. **breed**: The breed or type of the animal (e.g., Pit Bull, Siamese).
13. **color**: A combination of the primary and secondary color information.
14. **outcome_date**: Date when the animal’s outcome was recorded.
15. **crossing**: Location or address where the animal was found (may contain partial or full addresses).
16. **jurisdiction**: The jurisdiction that managed the animal's case (e.g., Long Beach).
17. **outcome_type**: The type of outcome for the animal (e.g., euthanasia, rescue, transfer).
18. **outcome_subtype**: More detailed description of the outcome (e.g., ill severe, littlelion).
19. **latitude**: The geographic latitude where the animal was found or rescued.
20. **longitude**: The geographic longitude where the animal was found or rescued.
21. **outcome_is_dead**: Boolean indicator showing if the animal is deceased (True/False).
22. **was_outcome_alive**: Boolean indicator showing if the animal survived the outcome (True/False).
23. **geopoint**: The combination of latitude and longitude in a single point format (e.g., 33.8047935, -118.1889261).
