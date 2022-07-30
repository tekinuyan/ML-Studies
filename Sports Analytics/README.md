![Figure 0](https://github.com/tekinuyan/ML-Studies/blob/main/Sports%20Analytics/Sports%20Analytics%20Reoport_pics/image001.png)
# Expected Goals in Football

## Data Exploaration

We will focus exclusively on analyzing Shots in football, we begin by exploring some characteristics about this event of the game.
First, let's see how the outcomes differs by various leagues. Below table shows the percentage of the shots ended up goal or no goal. One can see that the between national leagues Italy has the least and Spain has the most goals scored. This is mainly a reason of the tactical plays which remained as traditional characteristic of the countries’ football style. Italian teams are the famous with their defensive playing whilst Spanish teams play offensive. On the other hand the world cup and European cup leagues have the least scores. As the graph indicates there is not much big of a difference between the percentages. We have conducted all of the datasets collected from the leagues in to one main dataframe. 

![Figure 1](https://github.com/tekinuyan/ML-Studies/blob/main/Sports%20Analytics/Sports%20Analytics%20Reoport_pics/image002.png)

Further, let's see how the different goals are distributed below. The red dots are on the left pitch indicates the coordinates of the goals. The right side is Karnel Density Plot of Goal Events which the dark green area is the most dense region where goals are happened. 

![Figure 2](https://github.com/tekinuyan/ML-Studies/blob/main/Sports%20Analytics/Sports%20Analytics%20Reoport_pics/image004.png)
![Figure 2](https://github.com/tekinuyan/ML-Studies/blob/main/Sports%20Analytics/Sports%20Analytics%20Reoport_pics/image006.png)

Moreover, below plot helps us to see the density of the shot distribution across the 2 axes of the pitch. On the right side the mean and standard deviation values of the axes are reprented to show the shots and goal event.

![Figure 3](https://github.com/tekinuyan/ML-Studies/blob/main/Sports%20Analytics/Sports%20Analytics%20Reoport_pics/image008.png)
![Figure 3](https://github.com/tekinuyan/ML-Studies/blob/main/Sports%20Analytics/Sports%20Analytics%20Reoport_pics/image010.png)

## xG Model (Expected Goals Model)

Let's prepare X and Y sets. Y will simply include every shot in the database and whether it was a goal or not (1 or 0). It is our target variable. X will include all the relevant information about the shot that we have in our data. That would be:

Location: X axis and Y axis in percentage(later converted to meter) to represent the length and width respectively.

Bodypart: right foot, left foot, head. 

Situation: open play, free kick

Time: Time as seconds and Period as 1st and 2nd half of the match.

Opportunity(Hot): 1 represents the shooting event was high probability to score or 0 as a surprising goal.

Out of 40658 total shots, there were 4629 goals. For each shot, we have 7 different characteristics mentioned above to describe it. Now we will divide our X and y into two different sets for training and testing. I will use 70% of them for training our model and 30% for  testing it. 

Before the feature selection, a correlation description would be helpful for us to eliminate some of the futures and focus on the more important ones. Below, the heatmap of the all of the features with linear correlation factors. The darker squares show a negative correlation and the brighter is positive correlation. From that we can see that the opportunity(“hot”) and x axes has positive correlation with scoring while the time feature had quite low factor compare to others and excluded in the further steps. There was not much significant correlation with the other parameters. Therefore, a machine learning model could help us to get more insight of a Goal event.

![Figure 4](https://github.com/tekinuyan/ML-Studies/blob/main/Sports%20Analytics/Sports%20Analytics%20Reoport_pics/image012.png)


## Gradient Boosting Classifier[1]

Since our aim to predict whether a shot is goal or not. The model can be clearly set as a binary classification problem. The possible methods are logistic regression and decision trees classifiers.

We will first train a Gradient Boosting Classifier, which is a very powerful algorithm. It consists of an ensemble of decision trees. Because these trees tend to overfit to the training data, developing thousands of different trees making use of different predictors and samples each time helps us reduce the variance of our predictions within the famous bias vs variance tradeoff.

We use hyperopt to learn the best hyperparameters for tuning our model. It tries different settings all over the ranges that we give to it, and then sticks to the most promising ones. Below are the first five hyperparameter combination. Almost all of them resulted the same. This indicates, there are no overfitting as our predictions are equally good for training and testing samples.

![Figure 4](https://github.com/tekinuyan/ML-Studies/blob/main/Sports%20Analytics/Sports%20Analytics%20Reoport_pics/image014.png)

The confusion matrix summarizes all of the predictions below. It tells us that, from all the shots that were not goal, our model correctly identified **12160 as no-goals**, and made a mistake in **1218** cases in which it predicted that the shot would not be a goal, but it was. From the other column, we see that it correctly predicted 73 goals, but failed to predict 136 successful shots as goals. From the report we can see the model has excellent numbers when it comes to predict class 0 (no-goal), but not that good for predicting class 1 (goals). With the latter, we have a precision of **65%**, and a recall of **10%**, resulting in an F1 score of 0.17. These are **not really good numbers.

![Figure 4](https://github.com/tekinuyan/ML-Studies/blob/main/Sports%20Analytics/Sports%20Analytics%20Reoport_pics/image016.png)

 
Predicting whether a shot will be goal and being right is extremely more difficult than correctly predicting it will not be a goal. This is particularly true if you have no idea who the player shooting the ball is or who the goalkeeper is and goalkeepers location as well as other defense players, which is the situation in which the algorithm is in. However while putting the hot column which indicates an opportunity index defined by the humans. **4602 goals** out of 4629 was considered as a high probability of a goal by just 27 surprise goals with **99.5%** accuracy. While humans made mistake by marking 27185 shots as “hot” but there was still no goal in contrast to machine learning model’s 91% precision for forecasting the non-goal shots. ** One can conclude that machines are predicting the non- goal shots better than humans while human can decide better which shot has high probability of scoring a goal**. 

Let's take a look at which of our features are more relevant for our model to make the decisions whether each shot is a goal or not.

![Figure 4](https://github.com/tekinuyan/ML-Studies/blob/main/Sports%20Analytics/Sports%20Analytics%20Reoport_pics/image017.png)

We see that most of the shot-location stand among the most relevant, as expected. The human interaction is also playing a significant role by determining whether the shot was a opportunity for a  goal or not.

## XGBoost Classifier
As a second XG model, I have used notorious XG boost algorithm to improve the recall and compare the current results with Gradient Boost. We get almost exactly the same results as with Gradient Boosting. When this is the case, one should usually prefer the simpler model, the Gradient Boosting. However, there are 5 goals that were correctly recognized as such by the Gradient Boosting that were not captured by the XGBoost. Even though this is not a huge difference, I will choose the Gradient Boosting because of it.

The feature selection of XG Boost is slightly differs from the GBC. It indicates after header the situation (FreeKick ), 1st period and bodypart replaced (FreeKick and  Right Foot). 

On the other hand, the decision tree represented below by XGBoost model indicates that if a shot is marked as hot, it is a goal. If not, if the x axis distance from the goal is smaller than 109 meters, than it is a goal, else missed. 

![Figure 4](https://github.com/tekinuyan/ML-Studies/blob/main/Sports%20Analytics/Sports%20Analytics%20Reoport_pics/image019.png)

As a conclusion, managers should advice the players to take as much shots as possible from the optimum angles that model indicates, which would increase the probability to score and encourage players to take a header if necessary. On the other hand, the model suggests that during the first period the goal probability is low. Coaches, can advice the strikers to save more energy to the second period and try to get closer to the opponent goal and more shots accordingly. 




## References
[1] https://www.kaggle.com/gabrielmanfredi/expected-goals-player-analysis
