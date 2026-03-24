# Car Accident Severity Analysis

## Introduction

Car-centered commuting is highly prevalent in the United States, making it important to understand the factors that influence car accident severity. Drivers vary widely in age, experience, and behavior, which can affect driving patterns such as caution, speed, and risk-taking. Social factors like solo travel vs. carpooling, as well as cultural factors such as commuting patterns, holidays, nightlife, and distracted driving, all contribute to accident risk.

Traffic conditions also vary by location, with differences between urban and rural environments influencing driving behavior. Historically, infrastructure quality, traffic density, and construction patterns have shaped how drivers interact with road systems. Additionally, institutions such as government agencies, law enforcement, and transportation departments regulate roadways and traffic laws, further influencing accident outcomes.

### Data Context

The dataset used in this project was collected through real-time traffic APIs, incorporating data from:
- U.S. and state departments of transportation  
- Law enforcement agencies  
- Traffic cameras and sensors  

The dataset includes accidents across 49 U.S. states (excluding Hawaii) from February 2016 to March 2023.

### Research Questions

- **Primary:** What combination of weather conditions and road infrastructure increases the severity of car accidents in California?  
- **Secondary:** Which road infrastructure is associated with high-severity car accidents?

---

## Methods

### Data Cleaning and Preparation

- Missing categorical values were filled with `"Missing"`
- Missing numerical values were replaced with `0`
- Weather conditions were grouped into categories:
  - CLEAR, CLOUDY, RAIN, SNOW, LOW_VIS, DUST, HAIL, WINDY
- The original **Severity (1–4)** variable was converted into a binary variable:
  - `Severe = 1` if severity ≥ 3  
  - `Severe = 0` otherwise  

### Features Used

#### Weather Variables
- Weather_Condition (categorical)
- Temperature (F)
- Visibility (mi)
- Wind Speed (mph)
- Precipitation (in)

#### Infrastructure Variables
- Bump  
- Crossing  
- Give_Way  
- Junction  
- Railway  
- Roundabout  
- Stop  
- Traffic_Signal  
- Traffic_Calming  
- Turning_Loop  

#### Geographic Scope
- Focused on **California**, which had the highest number of recorded accidents

---

## Modeling Approach

### Logistic Regression

We used logistic regression to model the probability that an accident is severe.

- Categorical variables → OneHotEncoded  
- Numerical variables → Standardized  
- Implemented using a pipeline with ColumnTransformer  

### Model Evaluation

- Used **5-fold cross-validation**
- Performance metric: **Accuracy**
- Average accuracy: **0.83**

### Scenario Simulation

To interpret model results:
- Created hypothetical scenarios combining weather and infrastructure
- Set numerical variables to average values within each weather group
- Computed predicted probabilities using `predict_proba()`

### Secondary Model

- Focused only on infrastructure variables
- Used a sample of 500,000 California accidents
- Interpreted coefficients to determine impact on severity

---

## Results

### Primary Question

Railway infrastructure consistently produced the highest predicted probabilities of severe accidents across multiple weather conditions.

- Example: Under cloudy conditions, probability ≈ **0.36**
- Suggests railway crossings are high-risk environments

Possible reasons:
- Higher travel speeds  
- Complex traffic interactions  
- Reduced reaction time near crossings  

---

### Secondary Question

- **Railway:** strongest positive association (coefficient ≈ 0.8)  
- **Junctions:** second strongest  
- **Stop signs & crossings:** negative association (lower severity risk)

Interpretation:
- Railway crossings → higher risk  
- Traffic control features → reduce severity  

---

## Ethics & Limitations

### Ethical Considerations

This model could be misused in ways that negatively impact communities:

- Insurance companies may increase premiums in high-risk areas  
- Increased policing in certain locations  
- Potential reinforcement of existing inequalities  

These effects could disproportionately impact already disadvantaged communities.

---

### Limitations

- Missing important variables:
  - Driver behavior  
  - Vehicle type  
- Potential **underreporting bias**:
  - Data depends on sensors, reports, and infrastructure
  - Areas with less monitoring may be underrepresented  
- Results are most applicable to:
  - Locations with similar data collection systems  
  - California specifically  

---

## Tools Used

- Python  
- pandas  
- plotnine  
- scikit-learn  
- Google Colab  

---

## How to Run

1. Open the notebook in Google Colab  
2. Install required libraries (if needed)  
3. Run all cells  
