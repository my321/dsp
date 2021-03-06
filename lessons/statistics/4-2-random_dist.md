[Think Stats Chapter 4 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2005.html#toc41) (a random distribution)
<p> Chapter 4, Exercise 2: The numbers generated by random.random are supposed to be uniform between 0 and 1; that is, every value in the range should have the same probability.
Generate 1000 numbers from random.random and plot their PMF and CDF. Is the distribution uniform?</p>
<p> Answer: Using the code below, I constructed a sample of 1000 using random.random(). Then I ploted the pmf and the cdf: </p>

 ![image of pmf](https://github.com/my321/dsp/blob/master/img/pmf_ch4_ex2.png)
 
  ![image of cdf](https://github.com/my321/dsp/blob/master/img/cdf_ch4_ex2.png)

<p> As we can see in the pmf, the distrubution of the sample is uniform since all the values have the same probability. The story continues in the plot of the cdf which is a straight line, this means the distribution is uniform. The bottom x% of values are below the xth percentile, for any x between 0 and 100. </p>


```python
#Chapter 4, Exercise 2
import numpy as np

import first 
import thinkstats2
import thinkplot 
import random

sample=[]
x=0
while x<1000:
    sample.extend([random.random()])
    x+=1
cdf = thinkstats2.Cdf(sample, label='random')
pmf = thinkstats2.Pmf(sample, label='random')

thinkplot.PrePlot(1)
thinkplot.Pmfs([pmf])
thinkplot.Show(xlabel='random',ylabel='PMF')
thinkplot.PrePlot(1)
thinkplot.Cdfs([cdf])
thinkplot.Show(xlabel='random',ylabel='CDF')
```





  
