[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

First we can import the data into the dataframe we will call ```nsfg```.

```resp = nsfg.ReadFemResp()```

Then, we form the pmf based on the variable ```numkdhh``` which corresponds to number of children in the household under the age of 18.

```numkdhh_pmf = thinkstats2.Pmf(resp.numkdhh, label = 'numkdhh')```

***This group had a mean of ```1.024``` children per household.***
Forming the biased pmf is slightly more complex. For each observation, we must have the number of children in that observation times of that observation. This replicates the effect of having sampled the children individually. For example, in a 3 child household, instead of getting one observation of a three child household, we would get 3 observations of the same 3-child household. Thereefore, the method supplied in Think Stats Chapter 3 works:
```def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        
    new_pmf.Normalize()
    return new_pmf

bias_pmf = BiasPmf(numkdhh_pmf, 'Biased by Kids')
```
As explained above, this multiplies each probability in the original, unbiased pmf, by the number of children associated with that probability. If the original showed a 25% chance of a 3-child household, the new one will show 75%. Because all the numbers of observations here are integers, we will naturally get a sum of probabilities greater than one, therefore we normalize this new pmf. 
***Under the new pmf the mean was ```2.404```.***

We can plot them together with the follwoing code:
```thinkplot.PrePlot(2)
thinkplot.Pmfs([numkdhh_pmf, bias_pmf])
thinkplot.Show(xlabel='Children per household', ylabel='PMF')
```
Which gives us:
```![](3.1pmfs.png)```
