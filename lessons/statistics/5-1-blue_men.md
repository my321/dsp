[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

<p> Chapter 5, Exercise 1: In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters μ = 178 cm and σ = 7.7 cm for men, and μ = 163 cm and σ = 7.3 cm for women. In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use scipy.stats.norm.cdf. </p>

<p> Answer: 13.85% of the U.S. male population falls in the range of 5'10" and 6'1". The code I used is included below. I followed the hint to use scipy.stats.norm.cdf. In  section 5.2, the author mentions that scipy.stats.norm.cdf evaluates a value using the standard normal distribution. The heights provided in BRFSS have a normal distribution; in order to use scipy.stats.norm.cdf, I will have to standardize the values. I convert the lower, 5'10", and upper limit, 6'1", into centimeters. I calculate the mean and standard deviation of the heights provided in BRFSS, and I use them to standardize the the upper and lower limit. Now, I can evaluate the standard upper and lower limit using scipy.stats.norm.cdf. The difference between the upper limit evaluation and lower limit evaluation will be the percentage of U.S. men that fall in that range, 13.85%. </p>

```python 
#Chapter 5, Exercise 1
import numpy as np

import first 
import analytic
import thinkstats2
import thinkplot 
import scipy.stats
import math
import brfss

df = brfss.ReadBrfss()
df.head() #use to determine height variable, double check using brfss.py file 
def convert_to_cm(inches):
    """ convert height in inches to cm
    """
    cm_height = 2.54*inches
    return cm_height

upper_value=convert_to_cm(6*12+1)
lower_value=convert_to_cm(5*12+10)

#calculate mean and var to standardize values to use in scipy.stats.norm 
ht_mean=df['htm3'].mean()
ht_var=df['htm3'].var()
ht_std=math.sqrt(ht_var)

def standard_value(value):
    """ convert height in cm to a standard normal value
    """
    standard_value=(value-ht_mean)/ht_std
    return standard_value

standard_upper=standard_value(upper_value)
standard_lower=standard_value(lower_value)

#calculate the difference between cdf(upper_value) and cdf(lower_value) to find the percentage of men who fall in between
men_between=scipy.stats.norm.cdf(standard_upper)-scipy.stats.norm.cdf(standard_lower)

print(men_between)
```
