
Matplotlib is a Python library used to create graphs, charts, and other visualizations from data.

**Important exam areas:**

- Basic plotting syntax
    
- Line plots, bar charts, scatter plots, histograms, and pie charts
    
- Titles, labels, legends, axes, and grid lines
    
- Subplots and saving figures
    
- Choosing the correct chart for a dataset
    
- Distributions, trends, relationships, and misleading visualizations
    

## 1. Introduction to Matplotlib

The `pyplot` module provides simple functions for creating plots.

```
import matplotlib.pyplot as plt
```

- `matplotlib` is the library.
    
- `pyplot` provides plotting functions.
    
- `plt` is the conventional alias.
    

### Basic plotting syntax

```
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [10, 20, 15, 30]

plt.plot(x, y)
plt.show()
```

Here:

- `x` contains the horizontal-axis values.
    
- `y` contains the vertical-axis values.
    
- `plt.plot()` creates a line plot by default.
    
- `plt.show()` displays the figure.
    

## 2. Types of Charts

### A. Line plot

A line plot displays data points connected by lines. It is commonly used to show trends over time or changes in a variable.

```
import matplotlib.pyplot as plt

months = ["Jan", "Feb", "Mar", "Apr"]
sales = [20, 35, 30, 50]

plt.plot(months, sales, marker="o")
plt.title("Monthly Sales")
plt.xlabel("Month")
plt.ylabel("Sales")
plt.show()
```

Important functions:

|Function|Purpose|
|---|---|
|`plt.plot(x, y)`|Creates a line plot|
|`plt.title("...")`|Sets the chart title|
|`plt.xlabel("...")`|Labels the horizontal axis|
|`plt.ylabel("...")`|Labels the vertical axis|
|`plt.show()`|Displays the figure|
|`plt.legend()`|Displays a legend for labeled data series|
|`plt.grid(True)`|Displays grid lines|

### B. Bar chart

A bar chart compares values across categories.

```
import matplotlib.pyplot as plt

subjects = ["CS", "Maths", "English"]
marks = [85, 90, 75]

plt.bar(subjects, marks)
plt.title("Marks by Subject")
plt.xlabel("Subject")
plt.ylabel("Marks")
plt.show()
```

- `plt.bar()` creates vertical bars.
    
- `plt.barh()` creates horizontal bars.
    

**Exam tip:** Use a bar chart to compare categories, such as marks by subject.

### C. Scatter plot

A scatter plot represents pairs of numerical values as individual points. It helps identify relationships, clusters, and outliers.

```
import matplotlib.pyplot as plt

hours = [1, 2, 3, 4, 5]
marks = [40, 50, 65, 70, 85]

plt.scatter(hours, marks)
plt.xlabel("Study Hours")
plt.ylabel("Marks")
plt.title("Study Hours vs Marks")
plt.show()
```

Unlike a line plot, a scatter plot does not automatically connect the points with lines.

**Exam tip:** Use a scatter plot to study the relationship between two numerical variables.

### D. Histogram

A histogram shows the distribution of numerical data by grouping values into intervals called _bins_.

```
import matplotlib.pyplot as plt

marks = [45, 50, 55, 60, 60, 70, 75, 80, 85, 90]

plt.hist(marks, bins=5)
plt.xlabel("Marks")
plt.ylabel("Frequency")
plt.title("Distribution of Marks")
plt.show()
```

- `bins=5` requests five intervals.
    
- With the default frequency setting, the height of each bar represents the number of observations in that interval.
    

**Exam trap:** A bar chart compares categories, whereas a histogram displays the distribution of numerical values grouped into bins.

### E. Pie chart

A pie chart displays how a total is divided among categories.

```
import matplotlib.pyplot as plt

labels = ["Python", "Java", "C++"]
students = [50, 30, 20]

plt.pie(
    students,
    labels=labels,
    autopct="%1.1f%%"
)
plt.title("Programming Language Preferences")
plt.show()
```

- `labels` names the categories.
    
- `autopct="%1.1f%%"` displays percentages to one decimal place.
    
- Pie charts work best with a small number of categories that make up a meaningful whole.
    

### F. Multiple lines and legends

```
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y1 = [10, 20, 15, 30]
y2 = [15, 18, 25, 28]

plt.plot(x, y1, label="Class A")
plt.plot(x, y2, label="Class B")

plt.xlabel("Test")
plt.ylabel("Marks")
plt.title("Class Comparison")
plt.legend()
plt.grid(True)
plt.show()
```

The `label` argument names each plotted series, and `plt.legend()` displays those names.

### G. Subplots

Subplots allow multiple plots to appear within a single figure.

```
import matplotlib.pyplot as plt

x = [1, 2, 3]
y = [10, 20, 30]

fig, axes = plt.subplots(1, 2)

axes[0].plot(x, y)
axes[0].set_title("Line Plot")

axes[1].bar(x, y)
axes[1].set_title("Bar Chart")

plt.tight_layout()
plt.show()
```

Here, `plt.subplots(1, 2)` creates one row and two columns of plots.

Important distinctions:

- `plt.title()` sets a title using the pyplot interface.
    
- `axes[0].set_title()` sets the title of a particular subplot.
    
- `plt.tight_layout()` adjusts spacing to help prevent labels and titles from overlapping.
    

### H. Saving a plot

```
import matplotlib.pyplot as plt

plt.plot([1, 2, 3], [10, 20, 30])
plt.title("Sample Plot")

plt.savefig(
    "sample.png",
    dpi=300,
    bbox_inches="tight"
)

plt.show()
```

- `plt.savefig()` saves the figure to a file.
    
- `dpi=300` specifies the output resolution.
    
- `bbox_inches="tight"` helps include surrounding labels and content.
    

For best results, save the figure before calling `plt.show()`, because some display workflows may clear or close the figure.

## 3. Basic Plot Customization

Matplotlib supports customization through arguments and functions.

|Feature|Example|Purpose|
|---|---|---|
|Color|`color="red"`|Changes line or plot color|
|Marker|`marker="o"`|Adds circular markers to line data|
|Line style|`linestyle="--"`|Uses dashed lines|
|Line width|`linewidth=2`|Sets line thickness|
|Figure size|`plt.figure(figsize=(8, 4))`|Sets dimensions in inches|
|Grid|`plt.grid(True)`|Adds grid lines|
|X-axis limits|`plt.xlim(0, 10)`|Sets horizontal-axis limits|
|Y-axis limits|`plt.ylim(0, 100)`|Sets vertical-axis limits|

### Example

```
import matplotlib.pyplot as plt

plt.figure(figsize=(8, 4))

plt.plot(
    [1, 2, 3, 4],
    [10, 20, 15, 30],
    color="red",
    marker="o",
    linestyle="--",
    linewidth=2
)

plt.xlim(0, 5)
plt.ylim(0, 40)
plt.grid(True)
plt.show()
```

The exact appearance depends on the chosen settings and Matplotlib configuration.

## 4. Data Visualization Concepts

Data visualization means presenting data graphically so that patterns, trends, comparisons, and relationships are easier to understand.

### A. Types of data

**Categorical data**

Data grouped into categories, such as subject names, cities, or programming languages.

Suitable example: a bar chart comparing student counts by subject.

**Numerical data**

Data expressed as numbers, such as age, marks, salary, or temperature.

Suitable examples:

- A histogram for marks distribution.
    
- A scatter plot for study hours versus marks.
    

**Time-series data**

Measurements recorded over time, such as daily temperature or monthly sales.

A line plot is often suitable for showing trends over time.

### B. Choosing the correct chart

|Purpose|Suitable chart|Example|
|---|---|---|
|Compare categories|Bar chart|Marks by subject|
|Show a trend over time|Line plot|Monthly sales|
|Show a numerical distribution|Histogram|Distribution of exam marks|
|Show a relationship between two numerical variables|Scatter plot|Study hours vs. marks|
|Show parts of a whole|Pie chart|Share of expenses by category|
|Compare multiple trends|Multiple-line plot|Sales of two products over time|

**Important:** Chart choice depends on the question being asked of the data. A pie chart is not always the best choice simply because the data contains percentages.

### C. Axes and scales

- **X-axis:** Usually the horizontal axis.
    
- **Y-axis:** Usually the vertical axis.
    
- **Scale:** The spacing and numerical range used on an axis.
    
- **Axis label:** Explains what the axis measures.
    
- **Title:** Describes the overall subject of the chart.
    
- **Legend:** Identifies different data series or categories when needed.
    

For example, a graph of temperature against time generally places time on the X-axis and temperature on the Y-axis.

### D. Distribution, trends, and relationships

Three common purposes of visualization are:

- **Distribution:** How values are spread, including concentration, variation, and possible outliers.
    
- **Trend:** How values change over time or across an ordered sequence.
    
- **Relationship:** How two variables vary together.
    

A scatter plot may reveal a positive association, a negative association, or no clear association.

**Important concept:** Correlation does not by itself establish causation.

### E. Outliers

An outlier is an observation that is unusually distant from other observations in a dataset.

- A scatter plot can help identify an isolated point.
    
- A box plot is another common visualization for examining spread and potential outliers.
    
- Outliers should be investigated rather than automatically removed; they may reflect data errors or legitimate unusual observations.
    

### F. Misleading visualizations

A graph can misrepresent data even if its underlying numbers are correct.

Common problems include:

- Truncating the Y-axis in a bar chart, making small differences look large.
    
- Using inconsistent scales across comparable graphs.
    
- Omitting axis labels or units.
    
- Using too many colors or categories.
    
- Choosing a pie chart with too many slices.
    
- Confusing correlation with causation.
    

A good visualization should be accurate, readable, appropriately scaled, and suited to the data.

## 5. Important Matplotlib Functions — Revision Table

|Function|Remember|
|---|---|
|`plt.plot()`|Line plot|
|`plt.bar()`|Vertical bar chart|
|`plt.barh()`|Horizontal bar chart|
|`plt.scatter()`|Scatter plot|
|`plt.hist()`|Histogram|
|`plt.pie()`|Pie chart|
|`plt.title()`|Set chart title|
|`plt.xlabel()`|Label X-axis|
|`plt.ylabel()`|Label Y-axis|
|`plt.legend()`|Display legend|
|`plt.grid()`|Control grid display|
|`plt.subplots()`|Create a figure and subplot axes|
|`plt.savefig()`|Save figure to a file|
|`plt.show()`|Display the figure|

## 6. Quick Exam Revision

1. `plt.plot()` creates a line plot by default.
    
2. `plt.bar()` creates vertical bars; `plt.barh()` creates horizontal bars.
    
3. `plt.scatter()` displays individual points without automatically connecting them.
    
4. `plt.hist()` groups numerical observations into bins.
    
5. `plt.pie()` displays parts of a whole.
    
6. `plt.xlabel()` labels the horizontal axis; `plt.ylabel()` labels the vertical axis.
    
7. `plt.legend()` displays labels supplied to plotted series.
    
8. `plt.subplots(1, 2)` creates one row and two columns of plots.
    
9. `plt.savefig()` saves a figure; `plt.show()` displays it.
    
10. Use a line plot for trends, a bar chart for category comparisons, a histogram for distributions, and a scatter plot for relationships between numerical variables.
    
11. Outliers are unusual observations and should be investigated rather than automatically deleted.
    
12. Correlation does not prove causation.