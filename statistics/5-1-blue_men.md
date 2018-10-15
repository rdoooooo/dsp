[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

Exercise 5.1 In the BRFSS (see Section 5.4), the distribution of heights is
roughly normal with parameters u = 178 cm and sigma = 7.7 cm for men, and
u = 163 cm and sigma = 7.3 cm for women.
In order to join Blue Man Group, you have to be male between 5'10" and
6'1" (see http://bluemancasting.com). What percentage of the U.S. male
population is in this range? Hint: use scipy.stats.norm.cdf.


# Code
```
import scipy.stats as stats

# Initial values of men and woemen normal distribution
men_u = 178 # cm
men_sigma = 7.7 # cm

women_u = 163 # cm
women_sigma = 7.3 # cm

# Height of interest 
height_lower = 5+10/12 #ft
height_upper = 6+1/12 # ft

# Convert height range of interest into cm
# 1 foot = 30.48 cm
ft_cm = 30.48
height_lower_cm = height_lower * ft_cm
height_upper_cm = height_upper * ft_cm

# Calculate probability range
prob_lower = stats.norm.cdf(height_lower_cm, loc=men_u, scale=men_sigma)
prob_upper = stats.norm.cdf(height_upper_cm, loc=men_u, scale=men_sigma)

print('Range of males between 5.10 and 6.1 is ' \
      + str(round(prob_lower,2)) + ' to '  + str(round(prob_upper,2)))
```
>> Range of males between 5.10 and 6.1 is 0.49 to 0.83 respectively
