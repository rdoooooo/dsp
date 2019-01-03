[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77)

---
# -*- coding: utf-8 -*-
"""
Created on Wed Jan  2 18:35:25 2019

@author: rd29722
"""

'''

# -*- coding: utf-8 -*-
"""
Created on Wed Jan  2 18:35:25 2019

@author: rd29722
"""

'''

Exercise 3  
In games like hockey and soccer, the time between goals is roughly 
exponential. So you could estimate a team’s goal-scoring rate by 
observing the number of goals they score in a game. This estimation 
process is a little different from sampling the time between goals,
 so let’s see how it works.

Write a function that takes a goal-scoring rate, lam, in goals per game,
 and simulates a game by generating the time between goals until the total
 time exceeds 1 game, then returns the number of goals scored.

Write another function that simulates many games, stores the estimates of
 lam, then computes their mean error and RMSE.

Is this way of making an estimate biased? Plot the sampling distribution 
of the estimates and the 90% confidence interval. What is the standard
 error? What happens to sampling error for increasing values of lam?
'''
```

import numpy.random as random
import numpy as np 

def game_simulation(lamb=1):
    total_time = 0 
    goals = 0
    while total_time < 1:
        goals += 1
        total_time += random.exponential(1/lamb, size =1)
    return goals-1  


def score_simulation (lam=2, m=100):

    Ls = []
    for i in range(m):
        L = game_simulation(lam)
        Ls.append(L)
    return(Ls)

lam = 4
Ls = score_simulation(lam = lam,m=10000)
Ls = np.array(Ls)
print('Mean Error :', np.mean((Ls- lam)))
print('RMSE :', np.sqrt(np.mean((Ls- lam)**2)))

print('This way of making estimation is unbiased because as m increases'
      'standard error decreases')



```
---
Mean Error : -0.01
RMSE : 2.0176223630798704
This way of making estimation is unbiased because as m increasesstandard error decreases
