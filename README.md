#  Basic Charts and Visual Encoding
##  Theory
### What is Data Visualization?
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

### Libraries Used

| Library | Purpose |
|---------|---------|
| `matplotlib` | Core plotting library for creating static charts |
| `seaborn` | Statistical data visualization built on matplotlib |
| `pandas` | Data manipulation and DataFrame creation |

### Types of Charts Covered

#### 1. Line Chart
A line chart connects data points with lines to show trends over time or ordered categories. It is ideal for visualizing continuous data and trends.

#### 2. Bar Chart
A bar chart uses rectangular bars to represent categorical data. The height/length of each bar is proportional to the value it represents. Useful for comparisons across categories.

#### 3. Histogram
A histogram divides continuous data into intervals (bins) and shows the frequency of data within each bin. It is used to understand the distribution of a dataset.

#### 4. Scatter Plot
A scatter plot uses dots to represent the values of two variables. It is used to observe relationships or correlations between two numerical variables.

#### 5. Conditional Scatter Plot
An enhanced scatter plot where data points are color-coded based on a categorical condition (e.g., Pass/Fail), making it easier to identify patterns within groups.

### Visual Encoding
Visual encoding refers to mapping data attributes to visual properties such as:
- **Position** (x/y axis)
- **Color** (to differentiate categories)
- **Size** (to indicate magnitude)
- **Markers/Shapes** (to distinguish series)

---

##  Dataset
```python
Days = {
    "Days": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"],
    "Study_Hours": [2, 3, 4, 5, 6, 7, 4],
    "Marks": [20, 30, 40, 50, 60, 70, 30],
    "Attendence": [70, 70, 60, 50, 70, 60, 80],
    "sleep_hours": [6, 7, 8, 6, 7, 8, 4]
}
df = pd.DataFrame(Days)
```
##  Code

### 1. Import Libraries

```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
```

> **Explanation:** Imports the three essential libraries — `matplotlib.pyplot` for plotting, `seaborn` for advanced statistical charts, and `pandas` for creating and managing DataFrames.

---

### 2. Basic Line Chart

```python
# Line chart
plt.plot(df["Days"], df["Study_Hours"], marker="o", color="green")

# X-Axis and Y-Axis label
plt.xlabel("Days")
plt.ylabel("Study Hours")

# Title for the chart
plt.title("Study Hour")
```

> **Explanation:** Plots a simple green line chart showing Study Hours across each day. The `marker="o"` adds circular markers at each data point. Axis labels and a title are added for clarity.

---

### 3. Advanced Line Chart (Multiple Lines)

```python
# Advance line chart
plt.figure(figsize=(10, 5))

# Study Hours line
plt.plot(df["Days"], df["Study_Hours"], marker="^", color="green", label="Study Hours")

# Marks line
plt.plot(df["Days"], df["Marks"], marker=">", color="red", label="Marks")

plt.title("Study Hours and Marks")
plt.xlabel("Days")
plt.ylabel("Study Hours and Marks")
plt.legend()
```

> **Explanation:** Draws two lines on the same chart — one for Study Hours (green, triangle-up markers) and one for Marks (red, triangle-right markers). `figsize=(10,5)` sets a wider canvas. `plt.legend()` adds a legend to distinguish the two series.

---

### 4. Basic Bar Chart

```python
# Bar Chart
plt.figure(figsize=(10, 5))
plt.bar(df["Days"], df["Attendence"], color="lightblue")
plt.title("Attendence vs Days")
```

> **Explanation:** Creates a simple bar chart comparing Attendance percentages for each day of the week. Each bar is colored light blue for easy readability.

---

### 5. Advanced Bar Chart (with Value Labels)

```python
# Advanced bar charts
plt.figure(figsize=(10, 5))
bars = plt.bar(df["Days"], df["Marks"], color="lightblue", label="Attendence")

for bar in bars:
    y = bar.get_height()
    plt.text(bar.get_x() + bar.get_width() / 2, y, str(y),
             ha="center", va="bottom")

plt.title("Marks vs Days")
plt.xlabel("Days")
plt.ylabel("Marks")
plt.legend()
plt.grid(axis="y")
plt.show()
```

> **Explanation:** Creates an enhanced bar chart for Marks. A `for` loop iterates over each bar and uses `plt.text()` to annotate the top of every bar with its exact value. `plt.grid(axis="y")` adds horizontal grid lines for better readability.

---

### 6. Histogram (Matplotlib)

```python
# Histogram
data = {'Marks': [50, 60, 55, 70, 80, 85, 90, 45, 68, 72, 77, 82, 88]}
df = pd.DataFrame(data)
plt.hist(df['Marks'], bins=3)
plt.title('Marks Distribution')
plt.xlabel('Marks')
plt.ylabel('Frequency')
plt.show
```

> **Explanation:** Creates a histogram from a new marks dataset using 3 bins to show the distribution (frequency) of marks across different ranges. The data is split into 3 equal-width intervals automatically.

---

### 7. Scatter Plot (Basic)

```python
# Scatter Plot (Relationship)
import matplotlib.pyplot as plt
plt.scatter(df['Study_Hours'], df['Marks'])
plt.title('Study Hours vs Marks')
plt.xlabel('Study Hours')
plt.ylabel('Marks')
plt.show()
```

> **Explanation:** Creates a scatter plot to visualize the relationship between Study Hours (x-axis) and Marks (y-axis). Each dot represents one day's data point.

---

### 8. Conditional Scatter Plot (Color-Coded)

```python
# Conditional Scatter Plot
# Example Category
df['Results'] = ['Fail', 'Pass', 'Fail', 'Pass', 'Pass', 'Pass', 'Fail']
colors = ['red' if r == 'Fail' else 'green' for r in df['Results']]
plt.scatter(df['Study_Hours'], df['Marks'], c=colors)
plt.title('Study Hours vs Marks')
plt.xlabel('Study Hours')
plt.ylabel('Marks')
plt.show()
```

> **Explanation:** Adds a `Results` column to label each day as Pass or Fail. A list comprehension generates a color list — red for Fail, green for Pass. The `c=colors` argument applies these colors to the scatter plot, making it easy to visually distinguish outcomes.
--- 

### 9. Seaborn Histogram with KDE

```python
# Histogram (Seaborn)
sns.histplot(df['Marks'], kde=True)
plt.title('Marks Distribution')
plt.xlabel('Marks')
plt.ylabel('Frequency')
plt.show()
```

> **Explanation:** Uses Seaborn's `histplot()` to draw a histogram with a KDE (Kernel Density Estimate) curve overlay (`kde=True`). The KDE curve shows the smooth probability distribution of the marks, providing a cleaner alternative to matplotlib's histogram.

---

## Conclusion
 **Line Charts** are effective for visualizing trends over ordered categories (e.g., daily study hours).
 **Bar Charts** provide clear comparisons across categories; annotating bars with values adds precision.
 **Histograms** reveal the frequency distribution of continuous data using bins.
- **Scatter Plots** help identify relationships between two numerical variables; adding color encoding enhances categorical differentiation.
- **Seaborn** simplifies the creation of statistically informative charts (like KDE-overlaid histograms) with minimal code.
- Overall, the choice of chart type and visual encoding method significantly impacts how effectively data patterns are communicated.
