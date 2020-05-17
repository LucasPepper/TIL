# MatPlotLib: Scatter Plot

It is very useful and easy for visualizing relationships in the dataset. 

For example, imagine 3 lists containing the **GDP per Capita** [in USD], **Life Expectancy**[in years] and **Country's Population**[in millions].

A scatter plot can relate these 3 lists, putting the **GDP in X axis**,  **Life Exp. in Y** and  **Country's Pop as the dot size**.

```
import numpy as np
import matplotlib.pyplot as mlp

np_pop = np.array(pop)
np_pop = np_pop *** 2

plt.scatter(gdp_cap, life_exp, s = pop)     # s = Size of the dot

# Previous customizations
plt.xscale('log') 
plt.xlabel('GDP per Capita [in USD]')
plt.ylabel('Life Expectancy [in years]')
plt.title('World Development in 2007')
plt.xticks([1000, 10000, 100000],['1k', '10k', '100k'])

# Display the plot
plt.show()
```