# Predictably Divided: Examining Voter Attitudes

&nbsp;

### Objectives
* Use GradientBoostingClassifier algorithm to build a model to predict whether someone voted for Donald Trump or Joe Biden based on answers to survey questions.
* When the model is sufficiently accurate, interpret it to determine which answers to which questions were the strongest predictors of a vote for Trump or Biden.

### Conclusions
* The data show that the political divide in the U.S. is so complete, at least on certain issues, that just a handful of answers to questions on a range of topics can be used to predict a person's vote in the 2020 presidential election with 85%-95% accuracy. 
* The respondents' positions on the Affordable Care Act, the proposed wall along the Mexican border, the first impeachment of Donald Trump, and the government response to the coronavirus pandemic were the strongest predictors. This perhaps isn't surprising, since we know these are hot button issues? But need they be?
* Consider that only 3.7% of people who said they opposed the border wall also said they voted for Trump. And that only 5.1% of those who said they disapproved of the decade-old ACA also said they voted for Biden. This smacks not merely of divisiveness but of tribalism. 

### Further Consideration
* Given more time, it would be interesting to dig deeper into the data on single issues/questions. I'd also like to determine what areas of agreement might exist between the two sides of the political divide. 

&nbsp;
#### The Data: The American National Election Survey 
* Compiled by American National Election Studies, a collaboration between Stanford University and the University of Michigan.
* Survey of more than 8,000 people before and after the 2020 election. More than 1,300 features in the dataset.
&nbsp;

#### Cleaning the Data
* The features were labeled with codes, and there was no easy way to convert to descriptive labels programmatically. So this was done as needed during presentation of findings. 
* There was a problem with leakage. The first model registered 100% accuracy, due to highly correlated questions. Several dozen were removed manually until obvious correlations were eliminated.
* All of the features were categorical and needed to be encoded.
&nbsp;

#### Initial Model 
* After eliminating data leakage, initial model still scored highly.
* Test 
accuracy: 0.956
* Five-fold cross-validation score: 0.948
&nbsp;
#### Tuned Model
* The model was tuned following a grid search. Performance improved slightly (from an already high level).
* Test 
accuracy: 0.957
* Five-fold cross-validation score (accuracy): 0.951


&nbsp;
#### Confusion Matrix on Full Dataset
&nbsp;
![second_conf_matrix](https://user-images.githubusercontent.com/29707241/114323812-9f452400-9aec-11eb-9dfe-f1f42166eb0f.png)


&nbsp;
### Interpreting the Model
* There is some debate about whether feature importance or permutation feature importance is the most accurate, reliable measure of the importance of individual features to the model's accuracy. I looked at both. 
* NOTE: With both measures, the results deemed most important to the model's accuracy, not necessarily to the survey respondents.
&nbsp;


&nbsp;
#### Feature Importance: Obamacare, border wall, and covid response dominate
&nbsp;
![features_full_data](https://user-images.githubusercontent.com/29707241/114324493-ed0f5b80-9aef-11eb-9fbf-34e57a78e63e.png)

&nbsp;


#### Permutation Feature Importance
* Permutation feature importance returned some odd results on the full dataset. (It is said to struggle to deal with highly correlated features, such as in this dataset.)
* Not necessarily worth further exploration on the full dataset.

![perm_features_full_data](https://user-images.githubusercontent.com/29707241/114324514-0b755700-9af0-11eb-8440-ef03d4d3bd90.png)
&nbsp;



### Narrowing It Down: An Accurate Prediction in Three Questions (Or Fewer)?
* What questions and answers do we need to predict a person's vote?
* Using feature importance as a guide, I somewhat arbitrarily chose 59 questions on seven broad topics.
* I then ran the model on all at once, and on each subdivided dataset.

#### Topics
* Affordable Care Act
* Immigration
* Race
* Border Wall
* Russian Election Interference
* Ukraine/Impeachment
* Government spending on health care


&nbsp;
#### First run of collected "hot button" questions and answers: 
* Accuracy was extremely close to that of run on full dataset.
* Test set accuracy: 0.955
* Five-fold cross_validation score (accuracy): 0.957

&nbsp;
![hotbutton_opt](https://user-images.githubusercontent.com/29707241/114325433-c3f1c980-9af5-11eb-8e02-c3fc0f95b468.png)
&nbsp;


&nbsp;
#### Feature Importance: Trump's First Impeachment, Obamacare, Border Wall

![features_hotbutton_data](https://user-images.githubusercontent.com/29707241/114324986-29908680-9af3-11eb-9a60-756c7e17648c.png)



&nbsp;
#### Permutation Feature Importance: Impeachment, Obamacare, Russia

![perm_features_hotbutton_data](https://user-images.githubusercontent.com/29707241/114325012-59d82500-9af3-11eb-8ec7-ff6af48e5b37.png)


&nbsp;
### Examining Single-Topic Datasets


![Screen Shot 2021-04-10 at 9 55 14 PM](https://user-images.githubusercontent.com/29707241/114325053-a3287480-9af3-11eb-9d1e-18bf704b5c99.png)


#### Confusion Matrix on Ukraine/Impeachment Questions
&nbsp;
![impeachment_confmat](https://user-images.githubusercontent.com/29707241/114325133-21851680-9af4-11eb-89e6-2b44ab30f89d.png)


