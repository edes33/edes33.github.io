## This can be your internal website page / project page

**Project description:** This project explores car crash data from Massachusetts in 2020 with the goal of predicting crash severity. The dataset includes information on weather conditions, time of day, road type, and other contributing factors. After cleaning and preprocessing the data, multiple classification models were trained and evaluated, including logistic regression, Naive Bayes, kNN, and random forest. Results offer insights that could support traffic safety analysis and resource planning.  

### 1. Identify the problem

Motor vehicle crashes can result in outcomes ranging from minor property damage to severe injuries or fatalities. Predicting the severity of a crash based on environmental and situational factors can help inform public safety initiatives, emergency response planning, and infrastructure improvements. This project aims to develop a predictive model using Massachusetts 2020 crash data to classify crash severity based on features such as season, time of day, and road characteristics.

### 2. Data Understanding

The dataset contains 140 columns, meaning there are 139 potential features to use in models to predict our response variable of crash severity.  Crash severity has 5 different classes: Fatal Injury, Non-fatal Injury, Not Reported, Property Damage, and Unkown.

```{r}
crash2020 %>%
ggplot() +
  geom_point(aes(x=X, y=Y, color=CRASH_SEVERITY_DESCR))
```
<img src="images/crashes1.png?raw=true"/>

### 3. Support the selection of appropriate statistical tools and techniques

<img src="images/dummy_thumbnail.jpg?raw=true"/>

### 4. Provide a basis for further data collection through surveys or experiments

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
