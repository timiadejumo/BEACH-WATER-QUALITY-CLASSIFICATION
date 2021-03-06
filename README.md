# BEACH WATER QUALITY

![SurfClubLogo](img/SurfClubLogo.jpg)
## TABLE OF CONTENTS
[Business Understanding](#1-business-understanding)

[Goal](#goals)

[Data Understanding](#2-data-understanding)

[Data Preparation](#2a-data-preparation)

[Data Cleaning](#2b-data-cleaning)

[Feature Selection](#2c-feature-selection)

[Modeling](#3-modeling)

[Conclusion](#4-conclusion)

[Future Research](#5-future-research)




## 1. BUSINESS UNDERSTANDING
The city of Chicago, on Lake Michigan, in Illinois has approximately 26 miles of free and open lakefront for leisure activities of Chicago residents and visitors. The Chicago Park District manages the city's lakefront.
The lakefront, besides being a recreational value, is also an economic hub accounting for 4 billion US Dollars in GDP and employing 96,000 workers. This is in spite of the beaches being open for business only six (6) months of the year (NOAA - Office for Coastal Management). 

However, beach-goers, like the stakeholder, Surf Club, face a major problem: swimming restrictions due to high levels of bacteria in the beach water. 
In time past, these swimming bans during the beach season along Lake Michigan's shores were a major, and all too frequent, frustration for Chicago beach-goers, like members of the Surf Club. Swimming bans would be enforced when daily water samples showed very high levels of E. coli, which in itself is not the main danger, but signals that the water could be contaminated with other, more dangerous bacteria. Time lags between sampling and testing often meant that the beaches were open to swimmers while the bacterial levels were high and by the time the results came in and bans were in place, bacterial levels had returned to normal safe levels. The Chicago Park District has moved away from individual samples in favor of buoys and weather stations that transmit data in real time. The buoys measure observations like water temperature, wave movement, and cloudiness, each of which has a hand in high E. coli levels.

The beach water cloudiness, known technically as turbidity, provides a measure of the bacterial levels of the water. Turbidity is measured in Nephelometric Turbidity Units (NTU) is the target variable in this study. 

### Goals
The main goal of this project is to minimize the closure periods due to the time lags between sampling and testing. Using data science techniques, it aims to cut down this time using readings off the buoys and weather stations, and using these readings to presict the bacterial levels of beach water (Beach water quality).

## 2. DATA UNDERSTANDING
The datasets used for this project are all open-sourced and hosted on the City of Chicago Parks and Recreation portal. All observations are readings from weather stations and self-powered buoys located on the beach waters taken between May, 2013 and October, 2017. There are two datasets I am deploying: the first from the buoys located at the beaches records water quality, or turbidity. (Turbidity is the measure of relative clarity of a liquid. It is an optical characteristic of water and is a measurement of the amount of light that is scattered by material in the water when a light is shined through the water sample. The higher the intensity of scattered light, the higher the turbidity. Material that causes water to be turbid include clay, silt, very tiny inorganic and organic matter, algae, dissolved colored organic compounds, and plankton and other microscopic organisms.)

The second dataset contains observations recorded by weather sensors located at the beaches.
Data sources: 
- https://data.cityofchicago.org/Parks-Recreation/Beach-Weather-Stations-Automated-Sensors/k7hf-8y75
- https://data.cityofchicago.org/Parks-Recreation/Beach-Water-Quality-Automated-Sensors/qmqz-2xku

### 2a. Data Preparation
We used a variety of Python libraries to carry-out this project, most especially Pandas v1.1.3, Numpy v1.18.5, SciKit-Learn v0.23.2, Seaborn 0.11.0  and Matplotlib v3.3.1.

The dataset came as 2 separate files: one containing the target variable and other beach water readings and the other had the readings from the beach weather stations. To start, we merged the two files and started the bigger task of cleaning.

### 2b. Data Cleaning
The combined dataframe had 27 columns. 13 of the columns were dropped for one of several reasons: they were identification values, highly multicollinear with other columns or had a high percentage of null values.  We dropped this columns as inputting the wrong data could cause problems further down the line with our models. Categorical variables were OneHotEncoded. Every numerical feature that went into the third and fourth models were scaled.

### 2c. Feature Selection
The dummy model and First Simple Model made use of only numeric variables. Subsequent models incorporated the categorical variables, with oversampling of the minority class of the dependent variable to address the imbalance. For the third model, the numeric variables were standard scaled. The parameters for the decision tree were optimized using gridsearch.
the following charts show the relationship between some of the features selected and the target variable (turbidity level).

![AirTempvsTurbidityLevel](img/AirTemperature(C)vsTurbidityLevel(1).png)

![TotalRainvsTurbidity Level](img/TotalRainvsTurbidityLevel(1).png)

![TurbidityvsWavePeriod](img/Turbidity(NTU)vsWavePeriod(sec)(1).png)

![WaterTemperaturevsTurbidityLevel](img/WaterTemperature(C)vsTurbidityLevel(1).png)



## 3. MODELING
This project makes use of predictive modeling (logistic regression) and inferential modeling (decision trees). The first three models are logistic regression models and the fourth is a decision tree classifier.  I used both models because the target is multi-class. The metric of choice is accuracy because I am concerned about reducing both Type I and Type II errors. A false classification has one of two consequences:
- Swimmers are allowed into infected waters and could fall sick, or
- Beach activities are restricted and leads to economic losses.

All models attained the following accuracy scores on test data:
- Dummy Classifier:    90%
- First Simple Model:   89.9%
- Second Logistic Model:    76.8%
- Third Logistic regression model:    85.6%
- Decision Tree classifier:   95.7%

## 4. CONCLUSION
In conclusion, our model can predict the turbidity level of beach water at an accuracy of 96% using observations from the weather stations and readings from the transducers located at the beaches. The readings at taken hourly, as such, rather than the current 4-hour wait time, this model can give a run the numbers and in a matter of seconds return the current turbidity level of the beach water.

## 5. FUTURE RESEARCH
- Study beaches individually to unravel the relationship between geological/geographical features on water quality at each location
- Study the relationship between human activities at/around each loaction to water quality

For more information on the Beach Water Quality Analysis project see the [Jupyter Notebook](Beach_Water_Quality_NB.ipynb) or [presentation slides](BWQ_Presentation.pdf).
