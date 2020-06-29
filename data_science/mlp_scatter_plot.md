# MatPlotLib: Scatter Plot

It is very useful and easy for visualizing relationships in the dataset.

For example, imagine 3 lists containing the **GDP per Capita** [in USD], **Life Expectancy**[in years] and **Country's Population**[in millions].

A scatter plot can relate these 3 lists, putting the **GDP in X axis**,  **Life Exp. in Y** and  **Country's Pop as the dot size**.

```python
import numpy as np
import matplotlib.pyplot as mlp

# Scatter plot
plt.scatter(x = gdp_cap, y = life_exp, s = np.array(pop) * 2, c = col, alpha = 0.8)

# Previous customizations
plt.xscale('log')
plt.xlabel('GDP per Capita [in USD]')
plt.ylabel('Life Expectancy [in years]')
plt.title('World Development in 2007')
plt.xticks([1000,10000,100000], ['1k','10k','100k'])

# Additional customizations
plt.text(1550, 71, 'India')
plt.text(5700, 80, 'China')

# Add grid() call
plt.grid(True)

# Show the plot
plt.show()
```
