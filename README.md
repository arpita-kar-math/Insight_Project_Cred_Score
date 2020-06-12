## Credibility Score Calculator

In the last decade, the direct-to-consumer (DTC) category has exploded. And venture capital firms have jumped at the opportunity to place their bets in the burgeoning space. This is however not the only reason why one would like to investigate the growth of these firms.
Maybe you want to start your own clothing store and are looking to stock up on the trendiest outfits! Or maybe you are a shipping company looking to attract new clients whose warehouses you want to manage. The needs to understand and predict the growth scores of these DTC brands are endless.

My project, which is a consulting project for a company called Charm Analytics is a part of this intrinsic analysis towards this end goal. Charm analyzes various DTC brands to see which ones are poised for success. This success/growth of the brands is measured via a metric called 'growth score'. A growth score is calculated based on time series data, obtained by analyzing the activities of these brands on social media platforms like Facebook, Instagram etc over a period of time. Key word to notice here is ‘period of time’. This is a key component missing when we are considering a new brand which just got into the market. We do not have enough time series data to make this analysis to estimate growth score. We thus need a new dimension to do this analysis. This dimension is considering the people leading the brand, defining a metric to measure how credible they are.

# Data

Two datasets, one of 1.5 million brands and one of their employees. The employee data is very tiny. We have their job tiles and their working since and working until info (half of this is missing data). 

# Data Cleaning and Feature Engineering

We fill in the time info meaningfully, and calculate the time ratio per person = (time a person spends with a brand)/(total lifespan of the brand). We also investigate the job titles (there are ~90000 unique of those!) and classify them based on their responsiblity. A Manager's position weight is 2 and a Founder /Chairman of Board in a brand has a position weight of 10. The rest of the heirarchy in between gets a position weight incremented, the higher their position is. 

Next, for each person, weight_per_brand = (position weight)x(time ratio)x(growth score of that brand)
If the person is associated to just one brand : his credibility score equals his weight_per_brand.
If a person is associated to more than 1 brand : his credibility score equals the mean of the weight_per_brand.

# Validation of Definition of Credibility Score 

Okay, so we have this definition, how do we validate this? Is it good enough? Will these credibility scores help estimate the growth scores of new brands when those emerge?
To answer this question, we train various regression models to check whether the features related to the person (his credibility score, which employee status, his role) and some basic brand features (if it is a physical products brand or a brick and mortar brand) can predict the growth score of the brand. 

The regression techniques we use are Linear models like Linear Regression, Ridge Regression and Lasso Regression. These do not perform well in terms of R^2 metric as well as the mean absolute error metric. 

Next we implemented tree based methods like Random Forest Regressor and Gradient Boosting Regressor and these perform way considerably well. 

Finally, it is artificial neural networks which give the best model with a mean absolute error of +11.5 or -11.5. The growth score is on a range of -100 to +100, which thus imply that we can predict the growth score with an error of about + or -11.5.


# Implementation 

Charm has decided to integrate the model in their web interface where this model will predict the growth scores of new brands which Charm currently has difficulty in predicting, due to lack of time series data.

# Acknowledgement

I am very thankful to Insight Data Science, Toronto for giving me this opportunity to work with Charm Analytics on this project. Also, I am very grateful to all my Fellows and alumnni at Insight and Chris and Niall for for always giving such valuable insights on my ideas.



