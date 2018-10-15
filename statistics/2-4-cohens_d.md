[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

'''
Exercise 2.4 Using the variable totalwgt_lb, investigate whether 
rst ba-bies are lighter or heavier than others. Compute Cohen's d to quantify the
difference between the groups. How does it compare to the difference in
pregnancy length?

'''
    import numpy as np
    def Cohen_d(df1,df2):
        diff = df1.mean() - df2.mean()
        var1 = df1.var()
        var2 = df2.var()
        n1, n2 = len(df1), len(df2)

        pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
        d = diff / np.sqrt(pooled_var)

        return abs(d)

# Looks at baby weight 
import nsfg
df = nsfg.ReadFemPreg() 

## Loads all the birthdata into a DF
preg = nsfg.ReadFemPreg()

## Filters out babies that lived
live = preg[preg.outcome == 1]

## Of th babies that lived how many were 1st vs not 1st borns
firsts = live[live.birthord == 1]
others = live[live.birthord != 1]

## Check if there were any nans for totalweight
firsts_null = firsts.totalwgt_lb.dropna()
others_null = others.totalwgt_lb.dropna()

## Grab the weights of each 
firsts_mean = firsts_null.mean()
others_mean = others_null.mean()

## Calculate components of Cohen d metric
d = Cohen_d(firsts_null,others_null)

print('Cohen statistic d = ' + str(round(d,4)))
print('Total weight between first and not first babies is small since d <0.2')


# Looks at preg length

## Check if there were any nans for pregnancy length
firsts_null = firsts.prglngth.dropna()
others_null = others.prglngth.dropna()

## Grab the weights of each 
firsts_mean = firsts_null.mean()
others_mean = others_null.mean()

## Calculate components of Cohen d metric
d = Cohen_d(firsts_null,others_null)

print('Cohen statistic d = ' + str(round(d,4)))
print('Total pregnancy length difference between first and not first babies is small since d <0.2')


# Answers
Total Weight
Cohen statistic d = 0.0887
Total weight between first and not first babies is small since d <0.2

Pregenancy Length
Cohen statistic d = 0.0289
Total pregnancy length difference between first and not first babies is small since d <0.2

Difference in pregnancy length and total weight difference of first and not first baby 
is 3x in terms of Cohen d metric. However, both values are <0.2 therefore
difference is considered small.


