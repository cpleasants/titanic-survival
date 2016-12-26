# Titanic Survival
### Problem Statement:
In most deadly disasters, survival is not completely random; there exist some patterns that can be identified with the right data. For an emergency management company, being able to use these patterns to predict casualties is critical so they know where to focus their limited resources. If one group is less likely to survive than another, additional resources should be focused on ensuring that group's safety. The challenge is creating the right model for the job.
### Goal
The goal of this particular project is to use data from the [RMS Titanic](https://en.wikipedia.org/wiki/RMS_Titanic) to model passenger survival and casualties in order to demonstrate how an emergency management team can model a disaster to predict survival and casualties.
### Methods
I was given access to some data about passengers on the RMS Titanic including age, class, embarcation port, fare, and whether or not they survived the disaster (see Data Dictionary below for more details). After importing the data, cleaning it up, and extracting some features, I imputed missing values for age and fare using an ensemble of four linear regressors. I used this to create three classification models that I then ensembled. I used Recursive Feature Reduction to select features for each model.
### Results
My best model, the ensemble model, was able to predict with around 84% cross-validated accuracy who would survive and who would not. The classification report further specified that:
- this model correctly predicted 90% of the casualties and 72% of the survivors. 
- 84% of the people this model predicted would be casualties were in fact casualties, and 82% of people who the model predicted would survive did in fact survive

This model is, therefore, much better than random guessing, which would be right about 50% of the time. It is also better than guessing the most common outcome (not surviving), which would be right about 61% of the time. This model is 68% better than random guessing and 38% better than always guessing non-survival. This is not a perfect model, but it is quite good all things considered. When working with the client, we may decide to adjust some of the classification thresholds in order to minimize the number of potential casualties we might ignore thinking that they would have survived. For instance, we may only predict that someone will survive if our model suggests they have at least an 80% chance of survival, so that we can reduce the false negative rate.
### Risks and Assumptions:
The big assumption of this dataset is that the data are accurate. Since records were certainly not perfect 100 years ago (in fact, there are a lot of missing data), it is impossible to know exactly how accurate it really is. Another big assumption is that the patterns in these data are consistent with patterns that would exist in a complete dataset of titanic passengers. Since just over 2/3 (67%) of the passengers aboard the day it sank died, and 61% of those in this dataset died, there's a good chance this dataset isn't a perfect random sample of the passenger data and this may imply that there is something special about the data that were included that had an impact on survival (maybe we don't have the information on some of the poorest passengers, for instance, who we know were less likely to survive, and maybe being able to include those poorest of the poor would change our model). Finally, we are assuming that the survival patterns on the RMS Titanic are not completely unique to the RMS Titanic, since we'd like to apply it to other similar disasters (i.e. the patterns would, at least to some extent, hold true to a somewhat similar disaster in the same general time period).
### Data Dictionary (after cleaning):

Column Name|Data Type|Description|Notes
-----------|---------|-----------|-----
Survived|Boolean|Whether or not a passenger survived|
Pclass|String|Passenger class (1st, 2nd, or 3rd class)| proxy for socio-economic status (SES): 1st ~ Upper; 2nd ~ Middle; 3rd ~ Lower
Name|String|Passenger name|
Sex|String|Passenger sex, male of female|
Age|Float|Passenger age|
Sibsp|Integer|Number of siblings and/or spouses aboard|includes brothers, sisters, step-brothers, step-sisters, and married spouses
Parch|Integer|Number of parents and/or children aboard|includes mother, father, son, daughter, step-son, and step-daughters
Fare|Float|Passenger fare (ticket cost)|
Cabin|String|Cabin number(s)|
Embarked|String|Port of embarkation| C = Cherbourg; Q = Queenstown; S = Southampton

information source: https://www.kaggle.com/c/titanic/data
