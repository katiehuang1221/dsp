[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)
The distribution of income is famously skewed to the right. In
this exercise, we’ll measure how strong that skew is.

The data comes from the Current Population Survey (CPS):
```
import hinc
income_df = hinc.ReadData()
```
The dataset is in the form of a series of income ranges and the number of respondents who fell in each range. The lowest range includes respondents who reported annual household income “Under $5000.” The highest range includes respondents who made “$250,000 or more.”

To estimate mean and other statistics from these data, we have to make some assumptions about the lower and upper bounds, and how the values are distributed in each range. We can use the function ```InterpolateSample```:
```
def InterpolateSample(df, log_upper=6.0):
    """Makes a sample of log10 household income.

    Assumes that log10 income is uniform in each range.

    df: DataFrame with columns income and freq
    log_upper: log10 of the assumed upper bound for the highest range

    returns: NumPy array of log10 household income
    """
    # compute the log10 of the upper bound for each range
    df['log_upper'] = np.log10(df.income)

    # get the lower bounds by shifting the upper bound and filling in
    # the first element
    df['log_lower'] = df.log_upper.shift(1)
    df.loc[0, 'log_lower'] = 3.0

    # plug in a value for the unknown upper bound of the highest range
    df.loc[41, 'log_upper'] = log_upper

    # use the freq column to generate the right number of values in
    # each range
    arrays = []
    for _, row in df.iterrows():
        vals = np.linspace(row.log_lower, row.log_upper, int(row.freq))
        arrays.append(vals)

    # collect the arrays into a single sample
    log_sample = np.concatenate(arrays)
    return log_sample
```

It takes a DataFrame with a column, income, that contains the upper bound of each range, and freq, which contains the number of respondents in each frame.
It also takes log_upper, which is an assumed upper bound on the highest range, expressed in log10 dollars. The default value, log_upper=6.0 repre- sents the assumption that the largest income among the respondents is one million dollars.
```InterpolateSample``` generates a pseudo-sample; that is, a sample of house- hold incomes that yields the same number of respondents in each range as the actual data. It assumes that incomes in each range are equally spaced on a log10 scale.

Create the log sample:
```
log_sample = InterpolateSample(income_df, log_upper=6.0)
```
And plot the CDF:
```
log_cdf = thinkstats2.Cdf(log_sample)
thinkplot.Cdf(log_cdf)
thinkplot.Config(xlabel='Household income (log $)',
               ylabel='CDF')
```
<img src = "https://github.com/katiehuang1221/dsp/blob/master/img/Exercise6_1_1.png" width =100>


Convert the log sample back with unit of ($):
```
sample = np.power(10, log_sample)
```
And plot the CDF:
```
cdf = thinkstats2.Cdf(sample)
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Household income ($)',
               ylabel='CDF')
```
<img src = "https://github.com/katiehuang1221/dsp/blob/master/img/Exercise6_1_2.png" width =100>

Compute the median, mean, skewness and Pearson’s skewness of the resulting sample.
```
Median(sample), Mean(sample),Skewness(sample), PearsonMedianSkewness(sample)
```
The results are (51226, 74278, 4.94, 0.74). Indeed it is skewed to the right.
However, all of this is based on an assumption that the highest income is one million dollars. But that's certainly not correct.

What happens to the skew if the upper bound is 10 million?
```
log_sample = InterpolateSample(income_df, log_upper=7.0)
sample = np.power(10, log_sample)
```
Then the CDF plot looks like this:
<img src = "https://github.com/katiehuang1221/dsp/blob/master/img/Exercise6_1_3.png" width =100>

And the statistics are:
```
Median(sample), Mean(sample),Skewness(sample), PearsonMedianSkewness(sample)
```
(51226, 124267, 11.6, 0.4)
