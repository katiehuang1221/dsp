[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77)
In games like hockey and soccer, the time between goals is roughly exponential.
So you could estimate a team’s goal-scoring rate by observing the number of goals they score in a game.
This estimation process is a little di↵erent from sampling the time between goals, so let’s see how it works.
Write a function that takes a goal-scoring rate, lam, in goals per game, and simulates a game by generating the time between goals until the total time exceeds 1 game, then returns the number of goals scored.
```
def SimulateGame(lam):
    """Simulates a game and returns the estimated goal-scoring rate.

    lam: actual goal scoring rate in goals per game
    """
    goals = 0
    t = 0
    while True:
        time_between_goals = random.expovariate(lam)
        t += time_between_goals
        if t > 1:
            break
        goals += 1

    # estimated goal-scoring rate is the actual number of goals scored
    L = goals
    return L
```

Write another function that simulates many games, stores the estimates of lam, then computes their mean error and RMSE.
```
def SimulateGames(m=1000,lam=2):
    estimates = []
    for _ in range(m):
        L = SimulateGame(lam)
        estimates.append(L)

    print('mean error:', MeanError(estimates,lam))
    print('RMSE:',RMSE(estimates,lam))

SimulateGames(m=1000)
```
mean error: 0.001071
RMSE: 1.414905297184232

Is this way of making an estimate biased?
```
SimulateGames(m=1000000)
```
mean error: 0.001071
RMSE: 1.414905297184232

We see that the mean error becomes smaller as ```m``` increases, so according to the calculation this estimator is unbiased.

Plot the sampling distribution of the estimates and the 90% confidence interval.
```
def PlotSimulateGames(m=10000,lam=2):
    estimates = []
    for _ in range(m):
        L = SimulateGame(lam)
        estimates.append(L)

    cdf = thinkstats2.Cdf(estimates)
    ci = cdf.Percentile(5), cdf.Percentile(95)
    stderr = RMSE(estimates, lam)

    pmf = thinkstats2.Pmf(estimates)


    thinkplot.Hist(pmf)
    thinkplot.Config(xlabel='estimate goal score',
                 ylabel='PMF')

    print('90% CI:',ci)
    print('standard error:',stderr)

PlotSimulateGames(m=100000,lam=2)
```
90% CI: (0, 5)
standard error: 1.4162415048288903

<img src="https://github.com/katiehuang1221/dsp/blob/master/img/Exercise8_3_1.png" width=500>

What is the standard error? What happens to sampling error for increasing values of lam?

The standard error of estimating lambda is 1.42. We can test for ```lamnda = 4```:
```
PlotSimulateGames(m=100000,lam=5)
```
90% CI: (2, 9)
standard error 2.2256549597815023
<img src="https://github.com/katiehuang1221/dsp/blob/master/img/Exercise8_3_2.png" width=500>

The sampling error increases as the values of lam increases.
