[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

Exercise 1   Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample.

Use the NSFG respondent variable NUMKDHH to construct the actual distribution for the number of children under 18 in the household.

Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.

Plot the actual and biased distributions, and compute their means. As a starting place, you can use chap03ex.ipynb. 


# Answer
# http://localhost:8888/notebooks/metisgh/prework/ThinkStats2/code/chap03ex.ipynb 

resp = nsfg.ReadFemResp()

pmf_kids = thinkstats2.Pmf(resp['numkdhh'], label='numkdhh')

thinkplot.PrePlot(2)

thinkplot.Pmf(pmf_kids)

thinkplot.Config(xlabel='Num Kids', ylabel='PMF')

#This is the unbiased num kids distribution - i.e. what the actual mean is (population)

#pmf_kids is going to just be a PMF of the numkdhh found across the whole dataset

#Now, if we were to take a sample of the data and plot it, we'll see below that this would be biased and 

#skew towards higher values versus the population data

biased_pmf_kids = BiasPmf(pmf_kids, label='bias Num Kids')

thinkplot.PrePlot(2)

thinkplot.Pmfs([pmf_kids,biased_pmf_kids])

thinkplot.Config(xlabel='Num Kids', ylabel='PMF')


#The light blue line here is the biased sample - i.e. what we'd expect should we take a random sample of the num kids data


num_kids = resp['numkdhh']

population_mean_numkdhh = num_kids.mean()
biased_mean_numkdhh = biased_pmf_kids.Mean()

print('Full population mean for NUMKDHH:',population_mean_numkdhh)
print('Biased sample mean for NUMKDHH:',biased_mean_numkdhh)
# #################
Full population mean for NUMKDHH: 1.024205155043831
Biased sample mean for NUMKDHH: 2.403679100664282

