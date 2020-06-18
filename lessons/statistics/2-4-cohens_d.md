[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

Thanks to the code set out in Think Stats, this is a relatively simple exercise. The sample is already divided into the groups labeled 'firsts' and 'others,' which gives us an easy way to show this effect. 
Think stats sets out a simple function to return Cohen's d, which works as follows:
```
def CohenEffectSize(group1, group2):
    """Computes Cohen's effect size for two groups.
    
    group1: Series or DataFrame
    group2: Series or DataFrame
    
    returns: float if the arguments are Series;
             Series if the arguments are DataFrames
    """
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / np.sqrt(pooled_var)
    return d
```

Then, with the two samples already separated, we can simply run:
```
CohenEffectSize(firsts.totalwgt_lb,others.totalwgt_lb)
```
Which gives us:
```
-0.088672927072602
```
**Which implies that the second group (others, i.e. non-first-pregnancies) tend to be heavier. By how much? Interpreting Cohen's d implies that the mean weight of non-first-pregnancy births is 0.09 standard deviations heaver than first-pregnancy births' mean weight. This effect is roughly three times as significant as the effect in lengths of pregnancies.**


