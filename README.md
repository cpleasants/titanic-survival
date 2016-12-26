# Titanic Survival
### Problem Statement:
In most deadly disasters, survival is not completely random; there exist some patterns that can be identified with the right data. For an emergency management company, being able to use these patterns to predict casualties is critical so they know where to focus their limited resources. If one group is less likely to survive than another, additional resources should be focused on ensuring that group's safety. The challenge is creating the right model for the job.
### Goal
The goal of this particular project is to use data from the [RMS Titanic](https://en.wikipedia.org/wiki/RMS_Titanic) to model passenger survival and casualties in order to demonstrate how an emergency management team can model a disaster to predict survival and casualties in another disaster.
### Methods
I was given access to some data about passengers on the RMS Titanic including age, class, embarcation port, fare, and whether or not they survived the disaster (see Data Dictionary below for more details). After querying these data from a PostgreSQL server and cleaning it up, I created three distinct classification models based on the significant features in the dataset: a Logistic Regression Model, a K-Nearest Neighbors Model, and a Decision Tree model. I tested various parameters for each model to see which would give me the most accurate cross-validated classification score. After finding the best parameters for each model I compared them to each other and noticed that all three performed about the same, so I decided to take an average of the predicted probabilities to create an new classification matrix. This average prediction slightly outperformed all three models, so I decided that this "ensemble" model would be the best model to choose.
### Results
My best model, the ensemble model, was able to predict with around 81% cross-validated accuracy who would survive and who would not. The classification report further specified that:
- this model correctly predicted 89% of the casualties and 69% of the survivors. 
- 82% of the people this model predicted would be casualties were in fact casualties, and 79% of people who the model predicted would survive did in fact survive

This model is, therefore, much better than random guessing, which would be right about 50% of the time. It is also better than guessing the most common outcome (not surviving), which would be right about 61% of the time. This model is 62% better than random guessing and 33% better than always guessing non-survival. This is not a perfect model, but it is quite good all things considered. When working with the client, we may decide to adjust some of the classification thresholds so that we, for instance, only predict that someone will survive if our model suggests they have at least an 80% chance of survival in order to minimize the number of potential casualties we might ignore thinking that they would have survived.
### Risks and Assumptions:
The big assumption of this dataset is that the data are accurate. Since records were certainly not perfect 100 years ago (in fact, there are a lot of missing data), it is impossible to know exactly how accurate it really is. Another big assumption is that the patterns in these data are consistent with patterns that would exist in a complete dataset of titanic passengers. Since just over 2/3 (67%) of the passengers aboard the day it sank died, and 61% of those in this dataset died, there's a good chance this dataset isn't a perfect random sample of the passenger data and this may imply that there is something special about the data that were included that had an impact on survival (maybe we don't have the information on some of the poorest passengers, for instance, who we know were less likely to survive, and maybe being able to include those poorest of the poor would change our model). Finally, we are assuming that the survival patterns on the RMS Titanic are not completely unique to the RMS Titanic, since we'd like to apply it to other similar disasters (i.e. the patterns would, at least to some extent, hold true to a somewhat similar disaster in the same general time period).
### Future Improvements:
I hope to explore this dataset more in the future and try to look at some of the factors a bit differently. Because of the non-linear pattern in survival based on age, there may be other ways to approach including age in each model, like binning or using the square of the age in the model as well. I'd also like to see if the number of family members aboard (summ of parents/children and spouse/siblings) would have a greater impact on the model than each of them alone. I'd also like to try other methods to impute the missing age data, like a Decision Tree method, instead of just using the mean or dropping rows. Finally, I'd like to try to scrape some of the data from the cabin information to see if it provides any more predictive power to my model.
### Data Dictionary (after cleaning):

Column Name|Data Type|Description|Notes
-----------|---------|-----------|-----
survived|Boolean|Whether or not a passenger survived|
p_class|String|Passenger class (1st, 2nd, or 3rd class)| proxy for socio-economic status (SES): 1st ~ Upper; 2nd ~ Middle; 3rd ~ Lower
name|String|Passenger name|
sex|String|Passenger sex, male of female|
age|Float|Passenger age|
sib_spouse|Integer|Number of siblings and/or spouses aboard|includes brothers, sisters, step-brothers, step-sisters, and married spouses
parent_child|Integer|Number of parents and/or children aboard|includes mother, father, son, daughter, step-son, and step-daughters
fare|Float|Passenger fare (ticket cost)|
cabin|String|Cabin number(s)|
embarked|String|Port of embarkation| C = Cherbourg; Q = Queenstown; S = Southampton

information source: https://www.kaggle.com/c/titanic/data
