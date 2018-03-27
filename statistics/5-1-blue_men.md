[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

Exercise 1   In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters µ = 178 cm and σ = 7.7 cm for men, and µ = 163 cm and σ = 7.3 cm for women.

In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use scipy.stats.norm.cdf. 


scipy.stats contains objects that represent analytic distributions

```import scipy.stats```

For example scipy.stats.norm represents a normal distribution.

```mu = 178

sigma = 7.7

dist = scipy.stats.norm(loc=mu, scale=sigma)

type(dist)
```

scipy.stats._distn_infrastructure.rv_frozen


A "frozen random variable" can compute its mean and standard deviation.

```dist.mean(), dist.std()```

(178.0, 7.7)

It can also evaluate its CDF. How many people are more than one standard deviation below the mean? About 16%

```dist.cdf(mu-sigma)```

0.15865525393145741

How many people are between 5'10" and 6'1"?
```

#5'10 = 60 + 10 inches = 70 inches

#6'1 = 72 + 1 inches = 73 inches

low_bound = 70 * 2.54

high_bound = 73 * 2.54

print(low_bound, '<>', high_bound)
```

177.8 <> 185.42000000000002
```

low_p = dist.cdf(low_bound)

high_p = dist.cdf(high_bound)

print('Low: ', low_p)

print('High: ',high_p)

Low:  0.48963902786483265
High:  0.8323858654963072
```

For a N(178,7.7) distribution, there is a 48.96% chance of a value falling *below* our low bound of 177.8 CM (5'10"). There is also a 83.24% chance of a value falling *below* our high bound of 185.42 CM (6'1"). So, to get the answer as to what is the P(177.8 < x < 185.42), we have to substract the two

```
print('The P(177.8 < x < 185.42) is equal to:', round(high_p-low_p,4))
```
The P(177.8 < x < 185.42) is equal to: 0.3427. So, 34.27% of US men fall within Blue Man Group's accepted range for trying out.
