**Explaining my dataset:** I have a univariate timeseries dataset of energy consumption. Each row of the dataset are half-hourly records of the energy consumption of a consumer. So every `48` lines contain 1 full day of measurements of a single consumer.

*Answer:*
Normalisation is used in order to make things comparable that in original form are not comparable, such as variables with different measurement units. Your measurements to me seem all comparable as they are, so my first guess is that you don't need to do any normalisation (however I would always make such decisions based on full knowledge of the situation, which obviously I don't have).

There may however be reasons to normalise even in situations with comparable measurements. In a classification task the key question is whether certain systematic differences are informative for the class distinction. For example, the fact that one time series has a larger variance or value range than another may or may not involve information about the class membership. If time series are normalised, such information will be removed. This is a bad thing if the information in fact is useful for classification, but if it isn't, it may dominate more important information, and removing it by normalisation may be a good thing. This may also be the case if different time series have a different average level, and this is not informative for classification, but rather only the pattern of relative changes over time.

Note that one can in principle normalise over the time series, but one could also normalise over the time points, which can make sense if there are systematic differences between time points in all series, once more if those differences do not point to information useful for distinguishing the time series. For example once I worked on an application in which larger variance at a certain point in fact meant that what was going on at this point was more important for class discrimination, so it was important not to standardise this information away.

Such things could be deduced from subject matter knowledge, or you could find them out comparing different possibilities using cross-validation (but be careful to avoid information leakage by not doing things based on knowledge of the whole data set when leaving out observations - although a rough peek at the data may reveal a reason to normalise of which you may not be aware otherwise), although there is also a danger in comparing too many things based on the data, as then some things may look good by accident. In a good number of situations it doesn't make much of a difference whether you normalise or not, and in such a situation model selection bias from "overcomparison" may be worse than any option you choose without comparison.

So "no normalisation" would still be the first thing I'd try out with unified measurements in a situation like this, unless any subject matter knowledge would suggest normalisation.