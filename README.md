# Module_14_Challenge
> This module challenge compares the perfomance of different machine learning models of algorithmic trading strategies for a given dataset.  The final performance evaluation metric for each iteration of models is the overall cumulative return for the given period.

>The analysis notebook is entitled: machine_learning_trading_bot.ipynb and is found in the main repo.

> The images folder of the repo houses the different analysis plots for the strategies and models examined in the analysis.
***
# Evaluation Report

### Baseline Model/Strategy
* Baseline model used a simple DMAC strategy with short window being a 4 period SMA and the long window a 100 period SMA on a dataset of 15min intervals. 
* A predictive model was analyzed using a SVM classifier with a training data set of 3 months from the start of the provided data.
* This model produced overall accuracy of 0.55 (55%). Precision for the short/long signals was 0.43 and 0.56 respectively.  Recall saw the greatest difference of 0.04 for the short signal and 0.96 for the long signal.  The great difference in recall leads us to think that the data set is imbalanced and we could possibly be overfitting the data.
* The final performance metric of cumulative returns for the strategy/model indicated a positive outcome in that the strategy outperformed the underlying instrument 1.55X vs 1.4X.  See baseline png in images folder.

### Tune the Baseline (Training data set variation) 
* To tune the baseline model we examined increasing the training data set from 3 months (initial baseline model) to 1yr, 2y and 4yr. The strating point for all training data sets remained constant as the begining of the provided data (2015-04-02).
* What impact resulted from increasing or decreasing the training window? 
    - Interestingly, using 1yr and 2yr of train data resulted in the overall final best performance based on cumulative returns, see eval_training plot where red and green lines converge post the large drawdown in returns and return ~1.7X. 
    - On the whole, the 1yr training set (red line) performed consistently the best for the time period in examination. The 4 year training period resulted in the worst performance when looking at cumulative returns. This leads me to think that the data could be imbalanced and possibly overfit.

### Tune the Baseline (Adjust SMA periods)
* For this adjustment we changed both the short SMA (from 4 to 2) and long SMA (from 100 to 50) windows and reran the initial model/experiment (baseline) to see what changed wrt to the cumulative performance.
* What impact resulted from increasing or decreasing either or both of the SMA windows?
    - In this case, changing the windows to shorter periods adversly impacted the overall performance of the strategy as it did not performa better than actual returns of the underlying instrument (Actual Returns). 
    - Furthermore, it performed worse than using a 4 and 100 period SMA as signal. In this case (using 2 & 50 period SMA's) the final cumulative return for the period was ~1.2 or 20% increase vs when we used a 4 and 100 period SMA signal we saw final cumulative returns of slightly better than 1.5X or 50%. See plot sma_change in images folder.

### Choose the set of parameters that best improved the trading algorithm returns
* At this point it seems the best overall performance is achieved when using a 4 and 100 period SMA signal and 1yr training period on the provided data. See the plot entitled eval_training, the 1yr line consistently outperforms with the lowest drawdown and ends up approximately 1.7X or 70% return.

### Evaluate a New Machine Learning Classifier
* For this portion of analysis we will use the stochastic gradient descent classifer (SGDC) model.
* The model change was applied to the original baseline experiment, replacing the SVM model with SGDC model and examining results.
* Did this new model perform better or worse than the provided baseline model? Did this new model perform better or worse than your tuned trading algorithm?
    - As compared to the baseline model the stochastic gradient descent model (SGDC) performed worse at aproximately 1.35X then the original baseline SVM model at approximately 1.55X when looking at cumulative returns.
    - This model (SGDC) also performed worse than the best tuned model as well. (1.35X vs 1.7X)