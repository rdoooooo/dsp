[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

  import numpy as np
  import hinc
  import thinkplot
  import thinkstats2
  import matplotlib.pyplot as plt

  def InterpolateSample(df, log_upper=6.0):
      """Makes a sample of log10 household income.

      Assumes that log10 income is uniform in each range.

      df: DataFrame with columns income and freq
      log_upper: log10 of the assumed upper bound for the highest range

      returns: NumPy array of log10 household income
      """
      # compute the log10 of the upper bound for each range
      df['log_upper'] = np.log10(df.income)

      # get the lower bounds by shifting the upper bound and filling in
      # the first element
      df['log_lower'] = df.log_upper.shift(1)
      df.log_lower[0] = 3.0

      # plug in a value for the unknown upper bound of the highest range
      df.log_upper[41] = log_upper

      # use the freq column to generate the right number of values in
      # each range
      arrays = []
      for _, row in df.iterrows():
          vals = np.linspace(row.log_lower, row.log_upper, row.freq)
          arrays.append(vals)

      # collect the arrays into a single sample
      log_sample = np.concatenate(arrays)
      return log_sample

  def raw_moment(x,k):
      return 1/len(x) * sum(x**k)
  def central_moment(x,k):
      return 1/len(x)*np.sum((x-np.mean(x))**k)


  def Median(xs):
      cdf = thinkstats2.Cdf(xs)
      return cdf.Value(0.5)


  def PearsonMedianSkewness(xs):
      median = Median(xs)
      mean = raw_moment(xs, 1)
      var = central_moment(xs, 2)
      std = np.sqrt(var)
      gp = 3 * (mean - median) / std
      return gp




  def main():
      df = hinc.ReadData()
      log_sample = InterpolateSample(df, log_upper=6.0)

      xs = 10**log_sample
      #xs = xs[:-1]

      mean = raw_moment(x=xs,k=1)
      var = central_moment(x=xs,k=2)
      skew = central_moment(x=xs,k=3)
      hard = PearsonMedianSkewness(xs=xs)

      print('Mean: {}'.format(mean))
      print('Variance: {}'.format(var))
      print('Skew: {}'.format(skew))
      print('Pearson Skewness: {}'.format(hard))

      # PLots CDF
      #log_cdf = thinkstats2.Cdf(log_sample)
      #thinkplot.Cdf(log_cdf)

      # What fraction reports income lower than the mean
      percent_report = np.sum(xs<mean)/len(xs)
      print('{}% of households report taxable income below the mean'.format(round(percent_report,2)*100))

      # How do the results vary depending on upper bound
      precentage = []
      n_range = np.arange(start=1,stop=10, step= 1)
      for n in n_range:
          log_sample = InterpolateSample(df, log_upper=n)
          xs = 10**log_sample
          mean = raw_moment(x=xs,k=1)
          precentage.append(np.sum(xs<mean)/len(xs)*100)
      plt.figure()
      plt.plot(n_range,precentage)
      plt.xlabel('N Log Upper Bound')
      plt.ylabel('% of household reporting below mean')



  if __name__ == '__main__':
      main()

'''

Compute the median, mean, skewness and Pearson's skewness of the resulting
sample. What fraction of households reports a taxable income below the
mean? How do the results depend on the assumed upper bound?

Mean: 74278.70753118733
Variance: 8826025649.562706
Skew: 4104365035533441.0
Pearson Skewness: 0.736125801914178

66.0% of households report taxable income below the mean

As the upper bound increases, the percentage of households reporting a 
taxable income below the mean increases. Specifically, after 10^5, the percentages
increase exponentially.
'''
