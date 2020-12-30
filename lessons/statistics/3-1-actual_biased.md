[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)  
<p> Chapter 3, Exercise 1: Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample.
Use the NSFG respondent variable NUMKDHH to construct the actual distribution for the number of children under 18 in the household.
Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.
Plot the actual and biased distributions, and compute their means. </p>
<p> Answer: Using the code below, I constructed the biased distribution, plotted the distributions, and computed their means. I loaded the data set concerning all female respondents, instead of the one concerning pregnancy. As the latter did not contain the necessary variable. Then I constructed the biased pmf by multiplying the probability of the value by the value. For example, if the probability of five kids was .1, it is now .5. The mean of the actual distribution is 1.024, and the mean of the biased distribution is 2.404. This falls in line with the class size paradox. The survey data contains more children of larger households, so the mean will be higher. Instead of one household reporting 5 children, there are 5 kids reporting a family size of 5 total siblings. The households with no children will not appear in the survey response. The plotted pmfs look like this: </p>

![Image of Plot](https://github.com/my321/dsp/blob/master/img/hist_ch3_ex1.png)

```python 
#Chapter 3, Exercise 1 
import numpy as np

import nsfg
import first 
import thinkstats2
import thinkplot 

resp = nsfg.ReadFemResp() 
pmf = thinkstats2.Pmf(resp["numkdhh"], label='actual')

def Bias_pmf(pmf, label):
    bias_pmf=pmf.Copy(label=label)
    
    for x, prob in bias_pmf.Items():
        bias_pmf.Mult(x,x)
        
    bias_pmf.Normalize()
    return bias_pmf

bias_pmf=Bias_pmf(pmf,label='observed')
thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf,bias_pmf])
thinkplot.Config(xlabel='Number Children', ylabel='PMF')
print(pmf.Mean())
print(bias_pmf.Mean())
```
