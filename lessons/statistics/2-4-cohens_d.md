[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)
Using the variable ```totalwgt_lb```, investigate whether first babies are lighter or heavier than others. Compute Cohen’s d to quantify the difference between the groups. How does it compare to the difference in pregnancy length?

Select first babies and others using `birthord`.
```
firsts = live[live.nirthord == 1]
others = live[live.nirthord != 1]
```

Use the function ```CohenEffectSize``` to compute Cohen's *d* for the variable ```totalwgt_lb```:
```
CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)
```
-0.088672927072602

For pregnancy length (```prglngth```), the Cohen's effect size for first babies and others is 0.028879044654449883.
