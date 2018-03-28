[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

Exercise 1   Using data from the NSFG, make a scatter plot of birth weight versus mother’s age. Plot percentiles of birth weight versus mother’s age. Compute Pearson’s and Spearman’s correlations. How would you characterize the relationship between these variables? 

```
import first
live, firsts, others = first.MakeFrames()
live = live.dropna(subset=['agepreg', 'totalwgt_lb'])
x_age = live.agepreg
y_weight = live.totalwgt_lb

thinkplot.Scatter(x_age,y_weight,alpha=0.15,s=10)
thinkplot.Config(xlabel="Age of Mother (Yrs)", ylabel="Baby Weight (lbs)",axis=[13,40,2,13])
```
*Scatter Plot Picture

```
SpearmanCorr(x_age,y_weight) #Spearman uses rank - handles outliers better
```
0.09461004109658226

```
np.corrcoef(x_age,y_weight)
```
array([[1.        , 0.06883397],
       [0.06883397, 1.        ]])
       

The Spearman Coefficient is .095, suggesting a small and positive correlation between the Mother's Age at birth and the birthweight of her child. This is higher than the Pearson Coefficient of .069. But both coefficients suggest that there is a small and positive relationship between mother's age and birth weight. Yet the scatter plot above confirms that this relationship is slight.

