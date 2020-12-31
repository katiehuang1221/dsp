[Think Stats Chapter 8 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77) (scoring)
Suppose you draw a sample with size n = 10 from an exponential distribution with lambda = 2.
Simulate this experiment 1000 times and plot the sampling distribution of the estimate L.
Compute the standard error of the estimate and the 90% confidence interval.

**Code**
```
def ExponentialExp(n=10,m=1000):
    lam = 2

    estimates=[]
    for _ in range(m):
        xs = np.random.exponential(1.0/lam, n)
        L = 1 / np.mean(xs)
        estimates.append(L)

    cdf = thinkstats2.Cdf(estimates)
    ci = cdf.Percentile(5), cdf.Percentile(95)
    stderr = RMSE(estimates, lam)

    thinkplot.Cdf(cdf)
    thinkplot.Plot([ci[0], ci[0]], [0, 1], color='0.8', linewidth=3)
    thinkplot.Plot([ci[1], ci[1]], [0, 1], color='0.8', linewidth=3)
    thinkplot.Config(xlabel='estimates',
                 ylabel='CDF')

    print('90% CI',ci)
    print('standard error',stderr)

ExponentialExp()
```
90% CI (1.2754324410594688, 3.5001285038798318)  
standard error 0.7829818037243479

<img src="https://github.com/katiehuang1221/dsp/blob/master/img/Exercise8_2_1.png" width=500>

Repeat the experiment with a few different values of ```n```
and make a plot of standard error versus ```n```.

Try ```n=1000```:
```
ExponentialExp(n=1000)
```
<img src="https://github.com/katiehuang1221/dsp/blob/master/img/Exercise8_2_2.png" width=500>

Plot standard error versus ```n```:
```
def ExponentialExp(n=10,m=1000):
    lam = 2

    estimates=[]
    for _ in range(m):
        xs = np.random.exponential(1.0/lam, n)
        L = 1 / np.mean(xs)
        estimates.append(L)

    cdf = thinkstats2.Cdf(estimates)
    ci = cdf.Percentile(5), cdf.Percentile(95)
    stderr = RMSE(estimates, lam)

    return stderr

def PlotStderr_n():
    stderr_list = []
    n_list = [n for n in range(10,1000,10)]
    for n in n_list:
        stderr_list.append(ExponentialExp(n))

    thinkplot.Plot(n_list,stderr_list)
    thinkplot.Config(xlabel='n',
                 ylabel='Standard Error')

PlotStderr_n()
```

<img src="https://github.com/katiehuang1221/dsp/blob/master/img/Exercise8_2_3.png" width=500>

**Observation**
For n=10, the 90% confidence interval is [1.27, 3.5].
For n=1000, the 90% confidence interval is [1.9, 2.1].
The confidence interval becomes narrower but still include the actual lambda.
