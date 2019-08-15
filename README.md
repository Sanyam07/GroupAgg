# GroupAgg
### Author: Karthik Guruswamy

There is a notebook code here, for creating additional columns/features using 'group aggregates'. Groups are identified through categorical variables, with aggregates such as min, max, avg, stddev, median etc., performed on numeric columns at different 'group levels'. 

Currently I dont have code to "detect natural hierarchy" as I'm using cats as somewhat independent vars, but permute on them with some limits set in the code on how many level deep we have to go - otherwise we are going to end up with 1000s of columns.

Any help to make this code, smarter and better is appreciated! Once we have "full frame" support in BYOR, this could be moved there ? Github issue for fullframe support.

https://github.com/h2oai/h2oai/issues/9065

#### So how do we know that creating aggregation columns actually works ?

Just compare models on churn_train/churn_test.csv and churn_train_big_cols.csv/churn_test_big_cols.csv choosing the target col as 'is_churn'. If the settings are high enough, DAI works through >> features in *big_cols* data set to get better accuracy. For small settings, basic cols w/o aggregation yields better results. I will post results on "highly imbalanced" data set soon - because that's where the action is.

### Will it not overfit ?
This is a tricky area. (Discussed in GitHub above) as we are not doing aggregation for train/test separately, instead doing it all at once. For this case, I ran the aggregations "before" splitting up to train/test and it DID NOT overfit obviously. Will confirm more details on how the aggregations work independently on training/test.

Either case, the minimum thing would be do "batch scoring" since the row aggregates are derived from groups it belongs to, which may be ok. So for scoring, it will be transformed first and then scored.

