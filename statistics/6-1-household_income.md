[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)
Exercise 1  

The distribution of income is famously skewed to the right. In this exercise, we’ll measure how strong that skew is.

The Current Population Survey (CPS) is a joint effort of the Bureau of Labor Statistics and the Census Bureau to study income and related variables. Data collected in 2013 is available from http://www.census.gov/hhes/www/cpstables/032013/hhinc/toc.htm. I downloaded hinc06.xls, which is an Excel spreadsheet with information about household income, and converted it to hinc06.csv, a CSV file you will find in the repository for this book. You will also find hinc2.py, which reads this file and transforms the data.

The dataset is in the form of a series of income ranges and the number of respondents who fell in each range. The lowest range includes respondents who reported annual household income “Under $5000.” The highest range includes respondents who made “$250,000 or more.”

To estimate mean and other statistics from these data, we have to make some assumptions about the lower and upper bounds, and how the values are distributed in each range. hinc2.py provides InterpolateSample, which shows one way to model this data. It takes a DataFrame with a column, income, that contains the upper bound of each range, and freq, which contains the number of respondents in each frame.

It also takes log_upper, which is an assumed upper bound on the highest range, expressed in log10 dollars. The default value, log_upper=6.0 represents the assumption that the largest income among the respondents is 106, or one million dollars.

InterpolateSample generates a pseudo-sample; that is, a sample of household incomes that yields the same number of respondents in each range as the actual data. It assumes that incomes in each range are equally spaced on a log10 scale.

Compute the median, mean, skewness and Pearson’s skewness of the resulting sample. What fraction of households reports a taxable income below the mean? How do the results depend on the assumed upper bound? 

```
mean_income = Mean(sample)
median_income = Median(sample)

print(mean_income)
print(median_income)
```

Median is substantially lower than mean, as you can see above. Mean is $74,278.71, while Median is almost 25K less at $51,226.45. This, before we view the Skewness statistics, implies that there is a substantial skew to the right with this income data.
```
#Skewness
Skewness(sample), PearsonMedianSkewness(sample)
```

The Skewness statistics back this skew inference up - both Skewness and Pearson's Median Skewness are positive which aligns with our idea above.


What fraction of households report an income below the mean?
```
#From Chapter 4: Cdf provides Prob, which evaluates the CDF;
#that is, it computes the fraction of values less than or equal to the given value. 
income_below_mean = cdf.Prob(mean_income)
income_below_mean
```

income_below_mean reflects that 66% of respondants (households) report an income below the mean of $74,278.

# All of this is based on an assumption that the highest income is one million dollars, but that's certainly not correct.  What happens to the skew if the upper bound is 10 million?Without better information about the top of this distribution, we can't say much about the skewness of the distribution.

We'd certainly expect the skew to go further to the right if the upper bound is increased from 1 million to 10 million, that is to say that we can reasonably expect some respondants to make more than 1 million. Between hedge fund managers, CEOs and other high earners, it is fair to expect that 1 million is not a realistic top bound.
```
log_sample_10 = InterpolateSample(income_df, log_upper=7.0)
log_cdf_10 = thinkstats2.Cdf(log_sample_10)
thinkplot.Cdf(log_cdf_10)
thinkplot.Config(xlabel='Household inc (log $ - max 10MIL)',
               ylabel='CDF')


sample_10 = np.power(10, log_sample_10)

mean_10mil = Mean(sample_10)
median_10mil = Median(sample_10)

print(mean_10mil, median_10mil)
#Skewness
print(Skewness(sample_10), PearsonMedianSkewness(sample_10))
```

When bound is increased to 10Mil:
* Mean = 124267.39722164685
* Median = 51226.45447894046
* Standard Skewness = 11.603690267537793
* Pearson Skewness = 0.39156450927742087

Unsurprisingly, when we increased the upper bound to log(7) (10Million) mean increased by a lot - from 74K to 124K. Median stayed the same, which is to be expected. Though the higher numbers are larger, there are still the same number of higher and lower values above the median. Standard Skewness increased by almost a factor of 3, indicating major skewness to the right. However, the Pearson coefficient got smaller. This must mean that the increase in the standard deviation was larger than the gain we had in mean. But as the above comment mentioned, without detailed information about the top range of this data, we cannot really draw many conclusions about the true skewness of this data.

