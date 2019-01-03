[Think Stats Chapter 8 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77) (scoring)

# -*- coding: utf-8 -*-
"""
Created on Wed Jan  2 17:53:13 2019

@author: rd29722
"""
"""
Exercise 2  
Suppose you draw a sample with size n=10 from an 
exponential distribution with λ=2. Simulate this experiment
 1000 times and plot the sampling distribution of 
 the estimate L. Compute the standard error of the 
 estimate and the 90% confidence interval.

Repeat the experiment with a few different values of n and make a plot of standard error versus n.

"""
```
def mean_confidence_interval(data, confidence=0.9):
    a = 1.0 * np.array(data)
    n = len(a)
    m, se = np.mean(a), scipy.stats.sem(a)
    h = se * scipy.stats.t.ppf((1 + confidence) / 2., n-1)
    return m, m-h, m+h


import numpy as np
import scipy.stats
import matplotlib.pyplot as plt
# Given parameters
n_list=[10,100,1000]
m=1000
lamb=2
standard_error = []
import numpy.random as random

# Loop
for n in n_list:
    L = []
    # Run experiment m times 
    for i in np.arange(m):
        # Generates 10 samples from a exp dist
        xs =random.exponential(scale=1/lamb,size=n)
        # Calculate L
        L.append(1/np.mean(xs))
    L = np.array(L)
    
    # Standard Error
    standard_error_temp = np.sum((L-lamb)**2)/len(L)
    standard_error.append(standard_error_temp)
    
    meanx, lower, upper = mean_confidence_interval(data=L,confidence=.90)
    print('For n = {}'.format(n))
    print('Mean is {}'.format(np.round(meanx,2)))
    print('Confidence interval is {}-{}'.format(np.round(lower,2),np.round(upper,2)))



plt.plot(n_list,standard_error)
plt.xlabel('N')
plt.ylabel('Standard Error')
```
