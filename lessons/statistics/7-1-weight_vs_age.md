[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)
Using data from the NSFG, make a scatter plot of birth weight versus mother’s age.
```python
from matplotlib import pyplot as plt
plt.scatter(x='agepreg',y='totalwgt_lb',data=live, s=1)
plt.xlabel('Age of mother (years)')
plt.ylabel('Birth weight (lb)')
```
<img src="https://github.com/katiehuang1221/dsp/blob/master/img/Exercise7_1.png" width=500>

Plot percentiles of birth weight versus mother’s age.

Compute Pearson’s correlation:
```python
# Pearson’s correlation

def Pearson(xs,ys):
    xs = np.asarray(xs)
    ys = np.asarray(ys)

    meanx, varx = np.mean(xs), np.var(xs)
    meany, vary = np.mean(ys), np.var(ys)

    corr = np.sum((xs-meanx)*(ys-meany)) / np.sqrt(varx * vary) / len(xs)

    return corr

Pearson(live.agepreg,live.totalwgt_lb)
```
0.0688339703541091


Compute Spearman’s correlation:
```python
# Spearman’s correlation

def Spearman(xs, ys):
    xrank = pd.Series(xs).rank()
    yrank = pd.Series(ys).rank()
    return Pearson(xrank, yrank)

Spearman(live.agepreg,live.totalwgt_lb)
```
0.09461004109658228

How would you characterize the relationship between these variables?

From the scatter plot we don't see much correlation between mother's age and birth weight.
The correlations (Pearson's ~ 0.07 and Spearman's ~ 0.09) also suggests weak correlation.
The fact that Person's is lower than Spearman's implies the potential of having outliers or a non-linear relationship between the variables.
