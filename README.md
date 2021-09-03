# Taxi-Demand-Prediction

## Conclusion :

<h3>Steps Followed to solve</h3>

1.)Firstly it is discovered that our End customer is Taxi Driver.    
2.)Problem statement can be framed as, At the given location(NewYorkCity) in the next coming 10 mins, predict the number of pickups.     
3.)Next we defined the constraints such as latency requirement,interpretability and relative errors.    
4.)We defined the performance metric as Mean Absolute Percentage Error(MAPE)     
5.)We are taking Train data as March 2016 data and Test data as May 2016.    
6.)Here we are dealing with large csv files thus we need to use dask library instead of pandas and similarly we tried using new libraries for efficient computatuion.   
7.)Next we converted the date and time format to unix timestamp by defining the function.   
8.)We Performed data cleaning by focusing on the new york city on features such as latitude and longitude,Trip duration,speed and fare.   
9.)Next we moved to section of Data preparation where we cluster the new york city into more than one regions by maintaining inter cluster distance not less than 2.0 miles.     
10.)Based on the Timestamp for each cluster we are doing time binning for every 10 mins followed by smoothing.smoothing meaning for time bins with zero pickups,we are performing aggregation by considering previous timebins.                 
11.)We decided to go with 25 clusters through following contraint which states that the inter cluster distance should not be greater than 2.5 miles     
12.)We are performing feature engineering using ratios, simple moving averages, weighted moving averages, exponential weighted moving averages by considering the data of 25 clusters.   
13.)We computed a MAPE values of random model by considering above features.          
14.)Then we started predictions using the tree based regression models we take 2 months of 2016 pickup data and split it such that for every region we have 75% data in train and 25% in test, ordered date-wise for every region.           
15.)We trained and tested with Tree based models and Linear regression.lets see the performance table.          
<pre>
<h4>Error Metric Matrix Without Fourier Features(Tree Based Regression Methods) -  MAPE</h4>
--------------------------------------------------------------------------------------------------------
Baseline Model -                                   Train:  0.11491981263942216           Test:  0.11701440975       
Exponential Averages Forecasting -                 Train:  0.11127073147075771           Test:  0.112832317911       
Linear Regression -                                Train:  0.11060675388099978           Test:  0.11247471980020741    
Random Forest Regression -                         Train:  0.0754644362922688            Test:  0.1104681970661784
<h4>XgBoost Regression -                           Train:  0.10617662328771031           Test:  0.11026989265916094 </h4>
--------------------------------------------------------------------------------------------------------
</pre>
we can observe that XgBoost Regression performs well.<br/>
16.)We added features from Fourier Transforms of time series data.we took top 3 amplitude and frequency values corresponding to each cluster and merged with orginal data frame. <br/>                                  
17.) Lets see the results after adding the fourier transform features.        
<pre>
<h4>Error Metric Matrix With Fourier Transforms(Tree Based Regression Methods) -  MAPE</h4>
--------------------------------------------------------------------------------------------------------
Baseline Model -                               Train:  0.11491981263942216       Test:  0.117014409759033
Exponential Averages Forecasting -             Train:  0.11127073147075771       Test:  0.112832317911222
Linear Regression -                            Train:  0.11061976186265168       Test:  0.11251011840109576
Random Forest Regression -                     Train:  0.07705540373237789       Test:  0.1101459975560517
<h4>XgBoost Regression -                       Train:  0.10598846397416659       Test:  0.11022149049059932</h4>
--------------------------------------------------------------------------------------------------------
</pre>
18.)We can observe that performances not improved significantly but improved very minutely.XgBoost Regression performance improved from 0.10617 to 0.10598.<br/>                                    
19.) we performed Hyperparameter tuning with GRIDSEARCH Technique lets see the observations.         
<pre><h4>Error Metric Matrix GRID SEARCH Technique(Tree Based Regression Methods) -  MAPE</h4>
--------------------------------------------------------------------------------------------------------
Baseline Model -                             Train:  0.11491981263942216       Test:  0.11701440975903304
Exponential Averages Forecasting -           Train:  0.11127073147075771       Test:  0.11283231791122247
Linear Regression -                          Train:  0.5991386205834194       Test:  0.540503765435867
Random Forest Regression -                   Train:  0.10384260342201201      Test:  0.11060545694717408
<h4>XgBoost Regression -                     Train:  0.10968957706943865       Test:  0.11163526726485486</h4>
--------------------------------------------------------------------------------------------------------</pre>
20.)Next we performed Hyperparameter tuning with RANDOMSEARCH technique lets see the observation.         
<pre><h4>Error Metric Matrix RANDOM SEARCH Technique (Tree Based Regression Methods) -  MAPE</h4>
--------------------------------------------------------------------------------------------------------
Baseline Model -                             Train:  0.11491981263942216       Test:  0.11701440975903304
Exponential Averages Forecasting -           Train:  0.11127073147075771       Test:  0.11283231791122247
Linear Regression -                          Train:  0.7289427591754765       Test:  0.7328702377593985
Random Forest Regression -                   Train:  0.10497874792471346      Test:  0.11129861934620229
<h4>XgBoost Regression -                         Train:  0.10797959800772491       Test:  0.11072068300516784</h4>
--------------------------------------------------------------------------------------------------------</pre>
