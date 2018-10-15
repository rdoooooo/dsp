[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

Exercise 3.1 Something like the class size paradox appears if you survey
children and ask how many children are in their family. Families with many
children are more likely to appear in your sample, and families with no children
have no chance to be in the sample.
Use the NSFG respondent variable NUMKDHH to construct the actual distribution
for the number of children under 18 in the household.
Now compute the biased distribution we would see if we surveyed the children
and asked them how many children under 18 (including themselves) are in
their household.
Plot the actual and biased distributions, and compute their means. As a
starting place, you can use chap03ex.ipynb

'''

'''
  def UnbiasPmf(pmf, label):
  
      new_pmf = pmf.Copy(label=label)
      for x, p in pmf.Items():
          new_pmf[x] *= 1/x
      new_pmf.Normalize()
      return new_pmf
  def BiasPmf(pmf, label):
      new_pmf = pmf.Copy(label=label)
      for x, p in pmf.Items():
          new_pmf.Mult(x, x)
      new_pmf.Normalize()
      return new_pmf
 '''
 
# Code
import nsfg
import thinkstats2
import thinkplot
df = nsfg.ReadFemResp() 
pmf_unbiased = thinkstats2.Pmf(df.numkdhh, label='unbiased')
pmf_biased = BiasPmf(pmf=pmf_unbiased, label='biased')

thinkplot.Pmfs([pmf_unbiased, pmf_biased])
thinkplot.Config(xlabel='Number of children', ylabel='PMF')

print('Unbiased mean is ',pmf_unbiased.Mean() )
print('Biased mean is ',pmf_biased.Mean() )

# Answer
Unbiased mean is 1.024
Biased mean is 2.403

(Plot is generated if code is ran)
