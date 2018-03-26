[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

Exercise 1   Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample.

Use the NSFG respondent variable NUMKDHH to construct the actual distribution for the number of children under 18 in the household.

Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.

Plot the actual and biased distributions, and compute their means. As a starting place, you can use chap03ex.ipynb. 


# Answer

The first part of the code does the following

* Creates a resp object with the FemResponse Data
* Creates a PMF with the numkdhh column within resp - unbiased as it will take the full column's worth of data
* Then, we plot plot this via thinkplot

```
resp = nsfg.ReadFemResp()

pmf_kids = thinkstats2.Pmf(resp['numkdhh'], label='numkdhh')

thinkplot.PrePlot(2)

thinkplot.Pmf(pmf_kids)

thinkplot.Config(xlabel='Num Kids', ylabel='PMF')

```
# Place unbiased image here

This is the unbiased num kids distribution - i.e. what the actual mean is (population). pmf_kids is going to just be a PMF of the numkdhh found across the whole dataset. Now, if we were to take a sample of the data and plot it, we'll see below that this would be biased and skew towards higher values versus the population data.

```
biased_pmf_kids = BiasPmf(pmf_kids, label='bias Num Kids')

thinkplot.PrePlot(2)

thinkplot.Pmfs([pmf_kids,biased_pmf_kids])

thinkplot.Config(xlabel='Num Kids', ylabel='PMF')
```
# Place biased image here

Then, below, we will calculate the means of the num_kids column (named 'numkdhh') for both the biased and unbiased data. We'd expect the biased mean to be higher than the unbiased mean, as per the Class Size Paradox.

```
num_kids = resp['numkdhh']
population_mean_numkdhh = num_kids.mean()
biased_mean_numkdhh = biased_pmf_kids.Mean()

print('Full population mean for NUMKDHH:',population_mean_numkdhh)
print('Biased sample mean for NUMKDHH:',biased_mean_numkdhh)
```

# Full population mean for NUMKDHH: 1.024205155043831
# Biased sample mean for NUMKDHH: 2.403679100664282

The difference in means is 2.40 - 1.02 = apx 1.38 (children per household)

