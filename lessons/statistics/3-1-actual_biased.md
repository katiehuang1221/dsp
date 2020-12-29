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

Plot the actual and biased distributions, and compute their means:
Use thinkplot to plot the distribution:
```
thinkplot.Pmfs([pmf,biased_pmf])
thinkplot.Show(xlabel='number of kids', ylabel='probability')
```
<img src="https://github.com/katiehuang1221/dsp/blob/master/img/Exercise3_1.png" width=500>

The mean for actual distribution is:
```
pmf.Mean()
```
1.024205155043831
```

The mean for biased distribution is:
```
biased_pmf.Mean()
```
2.403679100664282
