[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)
Use the NSFG respondent variable ```NUMKDHH``` to construct the actual distribution for the number of children under 18 in the household.
```
resp = nsfg.ReadFemResp()
```
Use the Pmf class provided by thinkstats2.
```
pmf = thinkstats2.Pmf(resp.numkdgg, label='numkdhh')
```
Use thinkplot to plot the distribution:
```
thinkplot.Pmf(pmf)
thinkplot.Config(xlabel='number of kids', ylabel='probability')
```



Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.
Plot the actual and biased distributions, and compute their means.

>> REPLACE THIS TEXT WITH YOUR RESPONSE
