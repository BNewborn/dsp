[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

Exercise 4   
Using the variable totalwgt_lb, investigate whether first babies are lighter or heavier than others. Compute Cohen’s d to quantify the difference between the groups. How does it compare to the difference in pregnancy length? 

# Compute Cohen’s effect size to quantify the difference between the groups. How does it compare to the difference in pregnancy length?

```
#Mean
print(firsts.totalwgt_lb.mean())
print(others.totalwgt_lb.mean())
```
The difference in mean of the 2 groups is apx. 0.12 lbs (others being heavier than first borns, on average)

7.201094430437772
7.325855614973262

```
print(firsts.prglngth.mean())
print(others.prglngth.mean())
```
The difference in mean of the 2 groups' prglngth is apx. 0.08 lbs (with firsts having a slightly longer pregnancy, on average, than others)

38.60095173351461
38.52291446673706

From the above summary mean statistics of prglngth and totalwgt, we can say the following takeaways.

* On the whole, the firsts group (ie first born children) tend to have slightly longer pregnancies (by .08 weeks as a sample average) and slightly smaller weights than their Others counterparts. 
* As we'll illustrate below with our use of Cohen's D, both of these effect sizes seem to be small in magnitude. The below code and explanations will clarify this further.

# Cohen's D

```
CohenEffectSize(firsts.totalwgt_lb,others.totalwgt_lb)
#CohenEffectSize(others.totalwgt_lb,firsts.totalwgt_lb)
#I was just using the 2nd line to confirm that it would be the same as the first, just multiplied by -1
```
-0.088672927072602

The above Cohen's D (-0.0887) reflects that this is a small effect size (some would even say trivial). What this means is that our group statistics are suggesting a very small effect from first/other born status on total weight of the child at birth. This makes sense, as these groups' means are pretty close to being equal with only a small difference of .12/.13 lbs difference.
