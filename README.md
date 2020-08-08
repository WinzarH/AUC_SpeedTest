# AUC_SpeedTest
## Benchmarking Area Under the Curve

## Background

This Notebook is prompted by a recent discussion on [StackOverflow](https://stackoverflow.com/questions/58002702/is-there-a-faster-method-for-making-paired-comparisons-than-expand-grid-in-base), where I asked: 

> I want to estimate the likelihood that a randomly-selected item from one group will have a higher score than a randomly-selected item from a different group. That is, the *Probability of Superiority*, sometimes called the *Common-language Effect Size*. See for example: [https://rpsychologist.com/d3/cohend/](https://rpsychologist.com/d3/cohend/). This can be resolved algebraically if we accept that the data are normally distributed ([McGraw and Wong (1992, Psychological Bulletin, 111](http://dx.doi.org/10.1037/0033-2909.111.2.361)), but I know that my data are not normally distributed, making such an estimate unreliable.

The resulting discussion produced several new alternatives, most of which were a great deal better than my first efforts.
This file runs benchmarking tests to see the relative speed at which each algorithm works with different sample sizes.

# Functions to test

Eight alternative functions are benchmarked against each other and compared using a prespecified number of calculations with 100 iterations. Summary tables are presented for absolute and relative times. We then present these results with violin plots.

## Functions are:

1. My Original For-If-Else function
1. Bring data together with expandgrid 
1. "CJ" (C)ross (J)oin. A data.table is formed from the cross product of the vectors
1. DataTable cartesian product of data.table
1. Wilcox from base R 
1. Modified Wilcox from base R
1. BaseR AUC, taking advantage of properties of matrix outer product
1. AUC from BigStatsR
# Generate some artificial data

## Generating data

In this example, two non-normal data sets are compared, so it's unclear which should have higher probability of superiority. Group Alpha is more platykurtic (spread out), with many large negative and positive values, while group Beta is a $\chi$^2 distribution *(df=1)*, so highly skewed.
So the two distributions should look like this:
![density plots 1](/images/chunk-bigrerun-1.png)

## Simulation with small sample sizes
![violin plot small](/images/PrintResults-1.png)

## Simulation with larger sample sizes
![violin plot large](/images/chunk-rerun-2.png)

## Simulation with very large sample sizes
![violin plot larger](/images/chunk-bigrerun-2.png)

# Conclusion

Base AUC function is the consistent winner, except when sample size is unusually small.

