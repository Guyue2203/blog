---
title: python学习
date: 2025-03-24 00:18:02
tags: 
      - 编程
      - python
      - 持续更新
categories: 学习
---



最近一段时间在学习python，为了便于查找相关信息，我把一些与python有关的内容汇总到了下面，如果你看到了这篇，希望对你有用。

<!-- more -->

## 一 tkinter用法

`tkinter`是 Python 的标准图形用户界面（GUI）库，用于创建简单的桌面应用程序。它简单易用，适合初学者入门 GUI 编程。以下是`tkinter`的一些基本用法和常见组件的介绍。

### 1\.基本框架

在使用`tkinter`时，通常需要以下步骤：


• 导入`tkinter`模块。

• 创建一个主窗口（`Tk`对象）。

• 添加各种组件（如按钮、标签、文本框等）。

• 启动事件循环（`mainloop()`），让窗口保持打开状态。


示例代码


```python
import tkinter as tk

# 创建主窗口
root = tk.Tk()
root.title("Tkinter 示例")  # 设置窗口标题
root.geometry("400x300")  # 设置窗口大小（宽x高）

# 启动事件循环，让窗口保持打开状态
root.mainloop()
```



### 2\.常见组件

#### 2.1 标签（Label）

用于显示文本或图片。


```python
label = tk.Label(root, text="这是一个标签", font=("Arial", 14))
label.pack()  # 使用 pack 布局管理器
```



#### 2.2 按钮（Button）

用于触发事件。


```python
def on_button_click():
    print("按钮被点击了！")

button = tk.Button(root, text="点击我", command=on_button_click)
button.pack()
```



#### 2.3 文本框（Entry）

用于输入单行文本。


```python
entry = tk.Entry(root)
entry.pack()

def on_button_click():
    user_input = entry.get()  # 获取文本框中的内容
    print("输入的内容是：", user_input)

button = tk.Button(root, text="提交", command=on_button_click)
button.pack()
```



#### 2.4 文本区域（Text）

用于输入多行文本。


```python
text_area = tk.Text(root, height=5, width=30)
text_area.pack()
```



#### 2.5 单选按钮（Radiobutton）

用于一组互斥的选项。


```python
var = tk.IntVar()  # 用于存储选中的值

radio1 = tk.Radiobutton(root, text="选项1", variable=var, value=1)
radio2 = tk.Radiobutton(root, text="选项2", variable=var, value=2)
radio1.pack()
radio2.pack()
```



#### 2.6 复选框（Checkbutton）

用于一组可多选的选项。


```python
var1 = tk.IntVar()
var2 = tk.IntVar()

check1 = tk.Checkbutton(root, text="选项1", variable=var1)
check2 = tk.Checkbutton(root, text="选项2", variable=var2)
check1.pack()
check2.pack()
```



#### 2.7 下拉菜单（OptionMenu）

用于选择一个选项。


```python
var = tk.StringVar()
var.set("选项1")  # 默认值

options = ["选项1", "选项2", "选项3"]
option_menu = tk.OptionMenu(root, var, *options)
option_menu.pack()
```



#### 2.8 滑块（Scale）

用于选择一个数值范围。


```python
scale = tk.Scale(root, from_=0, to=100, orient=tk.HORIZONTAL)
scale.pack()
```



#### 2.9 列表框（Listbox）

用于显示一组选项。


```python
listbox = tk.Listbox(root)
listbox.insert(1, "选项1")
listbox.insert(2, "选项2")
listbox.insert(3, "选项3")
listbox.pack()
```



#### 2.10 消息框（Messagebox）

用于显示提示信息。


```python
from tkinter import messagebox

def show_message():
    messagebox.showinfo("提示", "这是一个消息框")

button = tk.Button(root, text="显示消息框", command=show_message)
button.pack()
```



### 3\.布局管理器

`tkinter`提供了三种布局管理器：`pack`、`grid`和`place`。

#### 3.1 pack

自动将组件排列到窗口中。


```python
label1 = tk.Label(root, text="标签1")
label2 = tk.Label(root, text="标签2")
label1.pack()
label2.pack()
```



#### 3.2 grid

以表格形式排列组件。


```python
label1 = tk.Label(root, text="标签1")
label2 = tk.Label(root, text="标签2")
label1.grid(row=0, column=0)
label2.grid(row=1, column=1)
```



#### 3.3 place

通过指定坐标来放置组件。


```python
label = tk.Label(root, text="标签")
label.place(x=50, y=100)
```



### 4\.事件绑定

可以为组件绑定事件，如鼠标点击、键盘输入等。


```python
def on_click(event):
    print("鼠标点击了！")

button = tk.Button(root, text="点击我")
button.pack()
button.bind("<Button-1>", on_click)  # 绑定鼠标左键点击事件
```



### 5\.完整示例

以下是一个完整的示例，结合了多种组件和布局：


```python
import tkinter as tk
from tkinter import messagebox

def on_button_click():
    user_input = entry.get()
    messagebox.showinfo("提示", f"你输入的内容是：{user_input}")

def on_radio_select():
    selection = var.get()
    messagebox.showinfo("提示", f"你选择了：选项{selection}")

# 创建主窗口
root = tk.Tk()
root.title("Tkinter 示例")
root.geometry("400x300")

# 标签
label = tk.Label(root, text="请输入内容：", font=("Arial", 12))
label.pack()

# 文本框
entry = tk.Entry(root)
entry.pack()

# 按钮
button = tk.Button(root, text="提交", command=on_button_click)
button.pack()

# 单选按钮
var = tk.IntVar()
radio1 = tk.Radiobutton(root, text="选项1", variable=var, value=1, command=on_radio_select)
radio2 = tk.Radiobutton(root, text="选项2", variable=var, value=2, command=on_radio_select)
radio1.pack()
radio2.pack()

# 启动事件循环
root.mainloop()
```


这个示例展示了如何创建一个简单的窗口，包含标签、文本框、按钮和单选按钮，并为按钮和单选按钮绑定了事件。


总结

`tkinter`是一个功能强大的 GUI 库，适合创建简单的桌面应用程序。通过掌握基本组件和布局管理器的使用，你可以快速构建出自己的 GUI 应用。如果需要更复杂的界面，可以结合其他库（如`ttk`模块）来实现更现代的外观和功能。

## 二 matplotlib.pyplot图表

**以下来自于kimi**

`matplotlib.pyplot`是 Python 中一个非常强大的绘图库，提供了多种类型的图表来满足不同的数据可视化需求。以下是一些常见的图表类型及其简单介绍：

### 1.折线图（Line Plot）

• 用途：用于展示数据随时间或某个连续变量的变化趋势。

• 函数：`plt.plot()`

• 示例代码：

```python
     import matplotlib.pyplot as plt

     x = [1, 2, 3, 4, 5]
     y = [1, 4, 9, 16, 25]
     plt.plot(x, y)
     plt.title("Line Plot")
     plt.xlabel("X-axis")
     plt.ylabel("Y-axis")
     plt.show()
```



### 2.散点图（Scatter Plot）

• 用途：用于展示两个变量之间的关系，适合观察数据的分布情况。

• 函数：`plt.scatter()`

• 示例代码：

```python
     import matplotlib.pyplot as plt

     x = [1, 2, 3, 4, 5]
     y = [1, 4, 9, 16, 25]
     plt.scatter(x, y)
     plt.title("Scatter Plot")
     plt.xlabel("X-axis")
     plt.ylabel("Y-axis")
     plt.show()
```



### 3.柱状图（Bar Chart）

• 用途：用于比较不同类别的数据大小。

• 函数：`plt.bar()`（垂直柱状图）或`plt.barh()`（水平柱状图）

• 示例代码：

```python
     import matplotlib.pyplot as plt

     categories = ["A", "B", "C", "D"]
     values = [10, 20, 15, 30]
     plt.bar(categories, values)
     plt.title("Bar Chart")
     plt.xlabel("Categories")
     plt.ylabel("Values")
     plt.show()
```



### 4.直方图（Histogram）

• 用途：用于展示数据的分布情况，通常用于连续数据的分组统计。

• 函数：`plt.hist()`

• 示例代码：

```python
     import matplotlib.pyplot as plt
     import numpy as np

     data = np.random.randn(1000)
     plt.hist(data, bins=30)
     plt.title("Histogram")
     plt.xlabel("Value")
     plt.ylabel("Frequency")
     plt.show()
```



### 5.饼图（Pie Chart）

• 用途：用于展示各部分占总体的比例关系。

• 函数：`plt.pie()`

• 示例代码：

```python
     import matplotlib.pyplot as plt

     sizes = [215, 130, 245, 210]
     labels = ["A", "B", "C", "D"]
     plt.pie(sizes, labels=labels, autopct='%1.1f%%')
     plt.title("Pie Chart")
     plt.show()
```



### 6.箱线图（Box Plot）

• 用途：用于展示数据的分布情况，包括中位数、四分位数、异常值等。

• 函数：`plt.boxplot()`

• 示例代码：

```python
     import matplotlib.pyplot as plt
     import numpy as np

     data = np.random.randn(100)
     plt.boxplot(data)
     plt.title("Box Plot")
     plt.ylabel("Value")
     plt.show()
```



### 7.面积图（Area Plot）

• 用途：类似于折线图，但折线下方的区域被填充。

• 函数：`plt.fill_between()`

• 示例代码：

```python
     import matplotlib.pyplot as plt

     x = [1, 2, 3, 4, 5]
     y = [1, 4, 9, 16, 25]
     plt.fill_between(x, y, alpha=0.3)
     plt.plot(x, y)
     plt.title("Area Plot")
     plt.xlabel("X-axis")
     plt.ylabel("Y-axis")
     plt.show()
```



### 8.堆叠柱状图（Stacked Bar Chart）

• 用途：用于展示多个类别在不同组中的分布情况。

• 函数：`plt.bar()`（通过堆叠实现）

• 示例代码：

```python
     import matplotlib.pyplot as plt

     categories = ["A", "B", "C"]
     group1 = [10, 20, 30]
     group2 = [15, 25, 35]
     plt.bar(categories, group1, label="Group 1")
     plt.bar(categories, group2, bottom=group1, label="Group 2")
     plt.title("Stacked Bar Chart")
     plt.xlabel("Categories")
     plt.ylabel("Values")
     plt.legend()
     plt.show()
```



### 9.堆叠面积图（Stacked Area Plot）

• 用途：用于展示多个类别在不同时间点的分布情况。

• 函数：`plt.stackplot()`

• 示例代码：

```python
     import matplotlib.pyplot as plt

     x = [1, 2, 3, 4, 5]
     y1 = [1, 4, 9, 16, 25]
     y2 = [2, 5, 10, 17, 26]
     plt.stackplot(x, y1, y2, labels=["Series 1", "Series 2"])
     plt.title("Stacked Area Plot")
     plt.xlabel("X-axis")
     plt.ylabel("Y-axis")
     plt.legend()
     plt.show()
```



### 10.热力图（Heatmap）

• 用途：用于展示二维数据的分布情况，通常用于相关性矩阵等。

• 函数：`plt.imshow()`或`sns.heatmap()`（需要`seaborn`库）

• 示例代码：

```python
     import matplotlib.pyplot as plt
     import numpy as np

     data = np.random.rand(10, 10)
     plt.imshow(data, cmap="hot", interpolation="nearest")
     plt.colorbar()
     plt.title("Heatmap")
     plt.show()
```



### 11.雷达图（Radar Chart）

• 用途：用于展示多个变量的相对大小，适合多维度数据的比较。

• 函数：需要手动绘制

• 示例代码：

```python
     import matplotlib.pyplot as plt
     import numpy as np

     labels = ["A", "B", "C", "D", "E"]
     values = [5, 3, 2, 4, 1]
     angles = np.linspace(0, 2 * np.pi, len(labels), endpoint=False).tolist()
     values += values[:1]  # Close the loop
     angles += angles[:1]  # Close the loop

     fig, ax = plt.subplots(figsize=(6, 6), subplot_kw=dict(polar=True))
     ax.fill(angles, values, color="red", alpha=0.25)
     ax.plot(angles, values, color="red", linewidth=2)
     ax.set_thetagrids(np.degrees(angles[:-1]), labels)
     plt.title("Radar Chart")
     plt.show()
```



### 12.极坐标图（Polar Plot）

• 用途：用于展示角度和半径的关系。

• 函数：`plt.polar()`

• 示例代码：

```python
     import matplotlib.pyplot as plt
     import numpy as np

     theta = np.linspace(0, 2 * np.pi, 100)
     r = np.sin(theta)
     plt.polar(theta, r)
     plt.title("Polar Plot")
     plt.show()
```


这些图表类型只是`matplotlib.pyplot`提供的一部分功能。

## 三 pandas用法

`pandas`是 Python 中一个功能强大的数据分析库，广泛用于数据处理、清洗、分析和可视化。它提供了两个主要的数据结构：`DataFrame`和`Series`。以下是一些基本的`pandas`用法和常见操作的介绍。

### 1\.导入 pandas

在使用`pandas`之前，需要先导入它。通常使用`pd`作为别名：


```python
import pandas as pd
```



### 2\.创建数据结构

#### 2.1 Series

`Series`是一个一维数组，类似于 Python 中的列表，但带有索引。


```python
# 创建一个简单的 Series
data = [1, 2, 3, 4, 5]
series = pd.Series(data)
print(series)
```


输出：

```
0    1
1    2
2    3
3    4
4    5
dtype: int64
```



#### 2.2 DataFrame

`DataFrame`是一个二维表格，类似于 Excel 表格，由多个`Series`组成。


```python
# 创建一个简单的 DataFrame
data = {
    "Name": ["Alice", "Bob", "Charlie"],
    "Age": [25, 30, 35],
    "City": ["New York", "Los Angeles", "Chicago"]
}
df = pd.DataFrame(data)
print(df)
```


输出：

```
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```



### 3\.读取和保存数据

#### 3.1 读取数据

`pandas`支持多种数据格式，如 CSV、Excel、JSON 等。


• 读取 CSV 文件：


```python
df = pd.read_csv("data.csv")
print(df)
```



• 读取 Excel 文件：


```python
df = pd.read_excel("data.xlsx")
print(df)
```



• 读取 JSON 文件：


```python
df = pd.read_json("data.json")
print(df)
```



#### 3.2 保存数据

同样，`pandas`也支持将数据保存为多种格式。


• 保存为 CSV 文件：


```python
df.to_csv("output.csv", index=False)
```



• 保存为 Excel 文件：


```python
df.to_excel("output.xlsx", index=False)
```



• 保存为 JSON 文件：


```python
df.to_json("output.json", orient="records")
```



### 4\.数据查看和筛选

#### 4.1 查看数据


• 查看前几行数据：


```python
print(df.head())  # 默认显示前 5 行
```



• 查看后几行数据：


```python
print(df.tail())  # 默认显示后 5 行
```



• 查看数据的形状：


```python
print(df.shape)  # 返回 (行数, 列数)
```



• 查看数据的列名：


```python
print(df.columns)
```



• 查看数据的基本信息：


```python
print(df.info())
```



#### 4.2 筛选数据


• 按条件筛选行：


```python
filtered_df = df[df["Age"] > 30]
print(filtered_df)
```



• 按列名筛选列：


```python
selected_columns = df[["Name", "City"]]
print(selected_columns)
```



### 5\.数据处理和转换

#### 5.1 添加新列


```python
df["Salary"] = [50000, 60000, 70000]
print(df)
```



#### 5.2 删除列


```python
df.drop(columns=["Salary"], inplace=True)
print(df)
```



#### 5.3 修改数据


```python
df.loc[0, "Age"] = 26  # 修改第 0 行的 "Age" 列
print(df)
```



####　5.4 数据排序


```python
sorted_df = df.sort_values(by="Age", ascending=False)
print(sorted_df)
```

5.5 数据分组


```python
grouped_df = df.groupby("City").mean()
print(grouped_df)
```



6\.数据清洗


6.1 处理缺失值


```python
# 查看缺失值
print(df.isnull().sum())

# 填充缺失值
df.fillna(value={"Age": df["Age"].mean()}, inplace=True)

# 删除包含缺失值的行
df.dropna(inplace=True)
```



6.2 删除重复数据


```python
df.drop_duplicates(inplace=True)
```



6.3 数据类型转换


```python
df["Age"] = df["Age"].astype(int)
print(df.dtypes)
```



7\.数据分析


7.1 基本统计


```python
print(df.describe())  # 查看数值型列的统计信息
```



7.2 聚合操作


```python
print(df.groupby("City").agg({"Age": ["mean", "max"], "Salary": "sum"}))
```



8\.数据可视化

虽然`pandas`本身主要用于数据处理，但它也支持简单的可视化操作，通常结合`matplotlib`使用。


```python
import matplotlib.pyplot as plt

# 绘制柱状图
df["Age"].plot(kind="bar")
plt.show()

# 绘制折线图
df["Salary"].plot(kind="line")
plt.show()
```



9\.完整示例

以下是一个完整的示例，展示了如何创建一个`DataFrame`，进行数据处理和分析，并保存结果。


```python
import pandas as pd

# 创建一个 DataFrame
data = {
    "Name": ["Alice", "Bob", "Charlie", "David"],
    "Age": [25, 30, 35, 40],
    "City": ["New York", "Los Angeles", "Chicago", "Houston"],
    "Salary": [50000, 60000, 70000, 80000]
}
df = pd.DataFrame(data)

# 查看数据
print(df.head())

# 筛选数据
filtered_df = df[df["Age"] > 30]
print(filtered_df)

# 添加新列
df["Bonus"] = df["Salary"] * 0.1
print(df)

# 删除列
df.drop(columns=["Bonus"], inplace=True)
print(df)

# 数据排序
sorted_df = df.sort_values(by="Salary", ascending=False)
print(sorted_df)

# 数据分组
grouped_df = df.groupby("City").mean()
print(grouped_df)

# 处理缺失值
df.loc[2, "Salary"] = None
print(df.isnull().sum())
df.fillna(value={"Salary": df["Salary"].mean()}, inplace=True)
print(df)

# 保存数据
df.to_csv("output.csv", index=False)
```



总结

`pandas`是一个功能强大的数据分析工具，通过掌握基本的数据结构、数据读取、数据处理和数据分析方法，可以高效地处理各种数据任务。如果需要更高级的数据分析或可视化功能，可以结合其他库（如`numpy`、`matplotlib`、`seaborn`等）来实现更复杂的需求。