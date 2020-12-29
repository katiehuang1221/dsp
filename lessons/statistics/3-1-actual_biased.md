[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)
Use the NSFG respondent variable ```NUMKDHH``` to construct the actual distribution for the number of children under 18 in the household.
```
resp = nsfg.ReadFemResp()
```
Use the Pmf class provided by thinkstats2.
```
pmf = thinkstats2.Pmf(resp.numkdgg, label='numkdhh')
```

Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.
```
biased_pmf = pmf.Copy(label='biased')
for x, p in pmf.Items():
  biased_pmf.Mult(x,x)

biased_pmf.Normalized()
```


Use thinkplot to plot the distribution:
```
thinkplot.Pmfs([pmf,biased_pmf])
thinkplot.Show(xlabel='number of kids', ylabel='probability')
```
![Plot actual vs biased]
(ThinkStats2/img/Exercise3_1.png)



Plot the actual and biased distributions, and compute their means.

>> REPLACE THIS TEXT WITH YOUR RESPONSE
