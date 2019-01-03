[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

# -*- coding: utf-8 -*-
"""
Created on Sun Jun  3 14:43:39 2018

@author: rd29722
"""

'''


Exercise 7.1 Using data from the NSFG, make a scatter plot of birth weight
versus mother's age. Plot percentiles of birth weight versus mother's age.
Compute Pearson's and Spearman's correlations. How would you character-
ize the relationship between these variables?

'''


import nsfg
import numpy as np
import matplotlib.pyplot as plt
import thinkstats2
import pandas as pd
df = nsfg.ReadFemPreg() 
df = df[['agepreg','totalwgt_lb']].dropna()
y = df.agepreg
x = df.totalwgt_lb
plt.figure()
plt.scatter(x=x,y=y,alpha=.03)
plt.xlabel('Birth Weight [lbs]')
plt.ylabel('Mothers Age [years]')

#%% Discretize data
bins = np.arange(2,15,1)
indices = np.digitize(x, bins)
groups = df.groupby(indices)

for i, group in groups:
    print(i,len(group))
#%%
ages = [group.agepreg.mean() for i, group in groups ]
cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups]

#%% Plot the percentiles of weight vs height
for percent in [75,50,25]:
    weights = [cdf.Percentile(percent) for cdf in cdfs]
    label = str(percent) + 'th' 
    thinkplot.Plot(weights,ages,label=label)

#%% Definitions

def Cov(xs,ys,meanx=None, meany=None):
    xs = np.asarray(xs)
    ys = np.asarray(ys)
    
    if meanx is None:
        meanx=np.mean(xs)
    if meany is None:
        meany=np.mean(ys)
    
    cov = np.dot(xs-meanx,ys-mean)/len(xs)
    return cov

def Corr(xs,ys):
    xs = np.asarray(xs)
    ys = np.asarray(ys)
    
    meanx = np.mean(xs)
    meany = np.mean(ys)
    varx= np.var(xs)
    vary = np.var(ys)
    
    corr = Cov(xs,ys,meanx,meany)/np.sqrt(varx*vary)
    return corr

def SpearmanCorr(xs,ys):
    xrank = pd.Series(xs).rank()
    yrank = pd.Series(ys).rank()
    return Corr(xrank,yrank)

#%% Calculate Pearson and Spearman's correclation
xs = df['agepreg'].tolist()
ys = df['totalwgt_lb'].tolist()

Spear = SpearmanCorr(xs,ys)
Pearson = Corr(xs,ys)

print('Pearson correlation: {}'.format(Pearson))
print('Spearman correlation: {}'.format(Spear))

print('Correlation is weak and the relationship is nonlinear')

------
Pearson correlation: 0.06883397000238382
Spearman correlation: 0.09461004109658425
Correlation is weak and the relationship is nonlinear
