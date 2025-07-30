## Crash Severity Prediction Project

**Project description:** This project explores car crash data from Massachusetts in 2020 with the goal of predicting crash severity. The dataset includes information on weather conditions, time of day, road type, and other contributing factors. After cleaning and preprocessing the data, multiple classification models were trained and evaluated, including logistic regression, Naive Bayes, kNN, and random forest. Results offer insights that could support traffic safety analysis and resource planning.  

### 1. Identify the problem

Motor vehicle crashes can result in outcomes ranging from minor property damage to severe injuries or fatalities. Predicting the severity of a crash based on environmental and situational factors can help inform public safety initiatives, emergency response planning, and infrastructure improvements. This project aims to develop a predictive model using Massachusetts 2020 crash data to classify crash severity based on features such as season, time of day, and road characteristics.

### 2. Data Understanding

The dataset contains 140 columns, meaning there are 139 potential features to use in models to predict our response variable of crash severity.  Crash severity has 5 different classes: Fatal Injury, Non-fatal Injury, Not Reported, Property Damage, and Unkown.  In the raw dataset, each observation represents a car involved in the crash.  For this analysis, we want each observation to be a crash so we will need to handle this in data preparation.

```{r}
crash2020 %>%
ggplot() +
  geom_point(aes(x=X, y=Y, color=CRASH_SEVERITY_DESCR))
```
<img src="images/crashes1.png?raw=true"/>

It is clear from this map that there is significant class imbalance.  Most crashes result in only property damage.  We will need to find an appropriate way of handling this later.

Because there are so many features, we should use business and understanding and some quick investigation of the features to identify what features to explore with our predictive models.  Keeping too many features would likely result in overfitting of the models to the training data.

### 3. Data Preparation

First we eliminate features based on business understanding as well as those missing a significant amount of data as they will not be useful in our models.

Next we need to change observations from vehicles to crashes. There is already a feature for the number of vehicles involved so we don't need to create this feature, but we will need to investigate features containing vehicle specific data such as driver's age and total occupants in car.  After handling missing data and unreasonable values for these features, we will use summary metrics such as min, max, mean, median, or mode to perserve this data at the crash level.
```{r}
age_summary_data <- crash %>%
  group_by(CRASH_NUMB) %>%
  summarise(MIN_DRVR_AGE=min(DRIVER_AGE, na.rm=TRUE), MAX_DRVR_AGE=max(DRIVER_AGE, na.rm =TRUE), AVG_DRVR_AGE=round(mean(DRIVER_AGE, na.rm=TRUE),3))
```
Now we remove the vehicle specific features
```{r}
crashes <- crash %>%
  dplyr::select(-DRIVER_AGE,-TOTAL_OCCPT_IN_VEHC)
```
And reduce the dataset to the crash level
```{r}
crashes <- distinct(crashes)
```
Finally, join the dataset with our new summary dataset we created
```{r}
crashes <- left_join(crashes,age_summary_data, by = "CRASH_NUMB")
```
Once the dataset is reduced to relevant features and crashes as observations, we continue our data preparation by looking at unreasonable values, outliers, and any remaining missing values.
```{r}
missing <- data.frame(missing_values=apply(crashes,2,function(x) sum(is.na(x))))
missing %>%
  filter(missing_values>0) %>%
  arrange(desc(missing_values))
```
We also explore correlation between features to ensure we address any multicollinearity.

<img src="images/crash_pairspanel.png?raw=true"/>

There is some correlation between speed limit and number of lanes, which makes sense because highways are often more lanes and higher speed.  However, the correlation is not so strong that we need to worry about removing one of these features.  For some of our models we will also need to look closer at the distribution of each feature.

Finally we must handle the class imbalance mentioned earlier.  From the earlier plot showing crash severity by X and Y coordinate, we can see there are 5 classes. However, two of these classes are "Not Reported" and "Unknown." Because this is our dependent variable, we will want to remove observations where the crash severity is listed as unknown or not reported.  This leaves us with 3 classes, but when we look at the number of observations by class, we can see that fatal injury only has 256 observations out of a total of over 87,000. This is not enough data points so we will combine fatal injury with non-fatal injury into one class "injury" (class 0) and consider property damage to be "no injury" (class 1). Thus we have reduced the problem to a binary classification problem.  We still have a significant class imbalance issue though, as the injury to non-injury split is roughly 25/75.  If  a model predicts all "no injury" then it will have ~75% accuracy which is not bad. To avoid this, we use undersampling, in which we reduce the number of observations of property damage randomly.
```{r}
inj_count <- sum(crash_data$CRASH_SEVERITY_DESCR==0)
crash_balanced <- ovun.sample(CRASH_SEVERITY_DESCR ~ ., data = crash_data, method = "under", N = inj_count*2, seed = 1)$data
table(crash_balanced$CRASH_SEVERITY_DESCR)
```

### 4. Data Modeling
#### a. Naive Bayes
#### b. Random Forest
#### c. Logistic Regression with Bagging
#### d. k-Nearest Neighbors (kNN)


For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
