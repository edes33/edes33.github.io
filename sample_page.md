## This can be your internal website page / project page

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

Eliminate features based on business understanding as well as those missing a significant amount of data as they will not be useful in our models.
Next we need to change observations from vehicles to crashes.  There is already a feature for the number of vehicles involved, but we will need to investigate features containing vehicle specific data such as driver's age and total occupants in car.  Driver's age and number of occupants are relevant data worth exploring with our models, so we do not want to lose them.  Instead, we will use summary metrics such as min, max, mean, median, or mode to perserve this data at the crash level.
Once the dataset is reduced to crashes as observations, we continue our feature engineering by looking at 

### 4. Data Modeling

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
