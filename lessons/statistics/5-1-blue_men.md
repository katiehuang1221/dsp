[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)
In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters μ = 178 cm and σ = 7.7 cm for men, and μ = 163 cm and σ = 7.3 cm for women.
In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use scipy.stats.norm.cdf.

```
import scipy.stats
```

Create the normal distribution representing the male height in the U.S.
```
mu = 178
sigma = 7.7
dist = scipy.stats.norm(loc=mu, scale=sigma)
```

Convert 5'10" and 6'1" into cm:
```
# 5'10" = 177.8cm
# 6'1" = 185.4cm
```

Use ```.cdf``` to find how many percents of people are between 177.8 and 185.4cm:
```
dist.cdf(185.4)- dist.cdf(177.8)
```
0.3420946829459531
So it's about 34%.
