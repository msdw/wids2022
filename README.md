## First place solution
We would like to first thanks WIDS and all the sponsors and Kaggle for providing us with an interesting use case that might have a big impact on our energy consumption, also in these hard time our support go out to the Ukrainian people fighting against this brutal invasion, we all hope this tragedy will end soon .

## Слава Україні!

We have been participating in Wids since 2019, with the following results: 1st in 2019, 3rd in 2020, 6th in 2021 and 1st in 2022.
The composition of our team is the same since last year, a mix between knowledge of Kaggle and the competition and the world of research to understand the expertise of the subjects to be treated, we will see how we engaged in the second phase .

## Ideas
It was really hard to identify buildings with no clear history in the dataset, so we build our solution with 2 kind of model :

one for all buildings where we tried to leverage past information about the building, in that case bagging, regression or even simple post processing formulae were quite efficient
we then build other models just for the hundreds of building in the test set that didn't had previous information, in that case it is useless to build LAG features so we used other kind of features, we also used some pseudo labeling from the first step in order to add more data in the train.
Thanks to @schopenhacker75 for writting us a bit on her work :

Before presenting the details of our work, we would like to point out that none of our team has a background in the energy field. Therefore, all the constructed variables are fully based on some research, intuitions and especially our expertise in feature engineering.

The keystone of our 1st place winner approach is the mix of past-values based feature engineering, the use of several powerful auto-ml engines. Also use of robust model based on a blend of several Gradient boosting
models mainly from LGB and Catboost

## Feature Engineering
Weather based feature extraction : we extracted other statistical weather related features such as min, max, average and skew of temperature features, also season based features such as min, max, avg temperature in each season each year … other features were extracted by dividing by 12 (months) the year cooling and heating degrees days

Building caracteristics feature extraction :
New building caracteristics were extracted from a linear composition of :

building_area = floor_area * ELEVATION

floor_energy_star_rating = energy_star_rating / ELEVATION

Lag based features : a lagged variable has its value coming from an earlier point in time. This type of features can measure auto-correlation of a given variable and shows up how its past values influence its future values:

Example what was the Energy Usage Intensity of the building the 1, 2 or 3 years ago?

Rolling Based Features: it consists in computing some statistical values (sum/mean..) for our target variables within a rolling window .
This method is called the rolling window method because the window would be different for every data point.
Example: **Moving average, over the last 1/2/3 years of the energy rating of the building
**

Delta based features : Features extracted from the difference / variance / derivative of current value vs previous values were applied; Example : we extracted the evolution rate of the Site Energy Comsumption from year-2 to year-1 then we constructed a new feature by multiplying this rate by the value of year-1.

 GroupBy based features : we applied aggregated functions like mean, min, max, or standard deviation by year and location  of Energy consumption and Energy rating to enrich our training dataset with grouped features statistics

## Notebooks
PART0 : https://www.kaggle.com/schopenhacker75/feature-engineering-catboost

PART1 : We run several autoML solutions like this one : https://www.kaggle.com/jayjay75/part-1-wids2022-model-with-lag

PART2 : It includes some post processing, pseudo labeling and training of new models to predict only the building with no history : https://www.kaggle.com/mathurinache/part2-wids2022-model2-no-lag

Stay safe cheers
