# Assessing Clustering Tendency
Before applying nay clustering technique we need to check if the randomness in the data. That is data should be non - uniformly distributed to be clustered. 

## Hopkins Statistic (H)
The Hopkins Statistic is a spatial statistic that tests the spatial randomness of a variable as distributed in a space.

### Use "clustertend" package in R to check the statistics 
* If H is close to 0.5, i.e Data is uniformly distributed, and contains no meaningful clusters => Null Hypothesis 
* If H is close to 0, i.e Data is not uniformly distributed and thus contains clusters => Alternate Hypothesis 
