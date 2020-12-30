[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)  
<p> Chapter 2 Exercise 4: Using the variable *totalwgt_lb*, investigate whether first babies are lighter or heavier than others. Compute Cohen's d to quantify the difference between groups. How does it compare to the difference in pregnancy length?</p>
<p> Using the code below, I calculate that the difference in means is -.08867 standard deviations, meaning first borns have a mean birth weight that is lower than subsequent births. The absolute value of the Cohen's d statistic for birth weight is higher than the statistic calculated for pregnancy length, but still substantially lower than the 1.7 standard deviation mean difference between male and female height; meaning birth weight is lower for first borns, but not by enough that it is noticeable to a casual observer like the difference between male and female height. For the code, apart from the function, I used the code from Chapter 2 of ThinkStats2. For the function, my code unintentionally follows closely to the code in Chapter 2. Obviously, the semantics are the same, but the syntax is mildly different. </p>

```python

import numpy as np

import math
import nsfg

preg = nsfg.ReadFemPreg()
live = preg[preg.outcome == 1]  ## data includes information on pregancies that did not result in live births, need to focus on pregancies that resulted in live births
first = live[live.birthord == 1] 
others = live[live.birthord != 1]
              
def calc_cohen_d(group_1, group_2):
    """ Calculate the Cohen d statistic, the difference of means as a fraction of the pooled sd
    """
    mean_1=group_1.mean()
    mean_2=group_2.mean()
    var_1=group_1.var()
    var_2=group_2.var()
    n_1=len(group_1)
    n_2=len(group_2)
    pool_var= (n_1*var_1+n_2*var_2)/(n_1+n_2)
    cohen_d = (mean_1-mean_2)/math.sqrt(pool_var)
    return cohen_d

print(calc_cohen_d(first['totalwgt_lb'],others['totalwgt_lb']))
```
