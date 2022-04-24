# Song Popularity Predictor (Open IIT Data Analytics 2020-21) 🎵

## Problem Statement 🧠
Predict popularity of music tracks based on features provided in the dataset.
The target variable, **popularity** has five categories: 
1. Very High
2. High
3. Average
4. Low 
5. Very Low

For each category there is an initial bid price (royalties to be paid) and expected revenue collection (in 10k $) as follows:
| Popularity  | Bid Price | Expected Revenue |
| ----------- | --------- | ---------------- |
| Very High   | 5         | 10               |
| High        | 4         | 8                |
| Average     | 3         | 6                |
| Low         | 2         | 4                |
| Very Low    | 1         | 2                |

## Scoring 🥇
Based on predictions, 10,000 (in 10K $) will be invested to place bids on 4,000 music tracks at the cost of a more popular music track. **Vice versa is not possible**.

## Final Model Approach 🎯
* Upon implementing the machine learning models, namely (Random Forest, XG Boost, AdaBoost) we got nearly the same revenue earned, but on analysing the confusion matrix we found out that most of the misclassification was where there was **under-classification**. On top of that bidding will be successful only if we bid on a less popular music track at the cost of a more popular music track, hence it would be desirable to classify the song one class above if not correct. Also, we were not able to maximize our bidding which had a ceiling of **2.5 times the number of datapoints**.

* Thus, we chose three models having nearly the same revenue generated (Random Forest, XGBoost, AdaBoost) and took the **ceiling value of the average of the three predictions**. 
Thereby even if one of the models predicted a certain datapoint to have a class one higher than the other two then we would bid assuming it to be such.

* For example, if the actual category of a song was “high”, if two of the models predicted the song to be of category “average” and the other “high”. Then had we applied a single model we would have got a revenue of **2 * 4 = 8**, on average it would be **$8/3**. But on applying a ceiling function on the predicted output we would have classified it correctly as “high” hence a revenue of **$8**.

* Taking another example if the actual category was “high”, if two of the models predicted the song to be of category “high” and the other “average”. Then if had we applied a single model we would have got a revenue of **2 * (2 * 4) = 16**, on average it would be **$16/3**. But on applying a ceiling function on the predicted output we would have classified it correctly as “high” hence a revenue of **$8**.
