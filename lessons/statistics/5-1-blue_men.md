[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

First of all, we use some scipy methods, so we need to import it:

```import scipy.stats```

We have the parameters given:

```mu = 178
sigma = 7.7
dist = scipy.stats.norm(loc=mu, scale=sigma)
type(dist)
```
A CDF is a usefull function because the probability of being between x and y, given y > x, will simply be cdf(y)-cdf(x). A simple converions is needed because the distribution is in cm's. 
So, we need only define the upper and lower bounds' cdfs and then compute their difference:
```low = dist.cdf(177.8)
high = dist.cdf(185.4)

print(high-low)
```
***So it is easy to show that the probability of a random person from the sample being between 5'10" and 6'1" 34%.***
