
在 Matplotlib 中，**Figure** 和 **Axes** 是构建图表的两个核心概念。理解它们的区别及其在图表中的角色对于有效使用 Matplotlib 至关重要。此外，还有一些其他概念和术语也容易引起混淆。以下是详细解释：

## 1. Figure 和 Axes 的定义与区别

### **Figure**

- **定义**：`Figure` 是 Matplotlib 中的顶级容器，代表整个图表窗口或画布。一个 `Figure` 可以包含一个或多个子图（`Axes`）。
    
- **作用**：
    
    - 管理整体布局和大小。
    - 包含所有的 `Axes`、图例、标题等。
    - 可以包含多个 `Axes`，即多个子图，每个子图都可以独立绘制不同的数据。
- **创建方式**：

```python
import matplotlib.pyplot as plt

fig = plt.figure(figsize=(8, 6))  # 创建一个 Figure 对象，指定大小
```

### **Axes**

- **定义**：`Axes` 是 `Figure` 中的一个子区域，表示图表中的一个具体绘图区域。每个 `Axes` 对象包含一个坐标系（包括 X 轴和 Y 轴），用于绘制数据。
    
- **作用**：
    
    - 承载具体的绘图内容，如折线图、散点图、柱状图等。
    - 管理坐标轴、刻度、标签、网格等。
    - 可以包含多个 `Artists`（如 `Line2D`、`Patch` 等），用于绘制具体的图形元素。
- **创建方式**：
```python
ax = fig.add_subplot(1, 1, 1)  # 在 Figure 中添加一个 Axes 对象
 
# 或者使用更简洁的方式
fig, ax = plt.subplots(figsize=(8, 6))
```

### **Figure 和 Axes 的层级关系**

- **层级结构**：

```mathematica
Figure
└── Axes
    ├── Axis（X 轴和 Y 轴）
    ├── Title
    ├── Labels
    └── Artists（如 Line2D、Patch 等）
```

- **一个 Figure 可以包含多个 Axes**，例如一个 2x2 的子图布局包含 4 个 Axes

```python
fig, axs = plt.subplots(2, 2)  # 创建一个包含4个子图的 Figure
```

## 2. 常见混淆点及解释

### **a. Axes 与 Axis 的区别**

- **Axes（复数）**：表示绘图区域或子图，是 `Figure` 的组成部分。
- **Axis（单数）**：表示坐标轴，如 X 轴或 Y 轴，是 `Axes` 的组成部分。

```python
ax = plt.gca()  # 获取当前的 Axes 对象
x_axis = ax.xaxis  # 获取 Axes 的 X 轴
y_axis = ax.yaxis  # 获取 Axes 的 Y 轴
```

### **b. Figure 和 Axes 的数量**

- **Figure**：通常一个 Matplotlib 会话中可以有多个 Figure，每个 Figure 是独立的图表窗口。
    
- **Axes**：一个 Figure 可以包含多个 Axes，一个常见的误解是将整个 Figure 视为一个 Axes，或者认为只有一个 Axes 存在。实际上，Figure 可以包含多个 Axes，具体取决于布局需求。

### **c. 坐标系与数据**

- **数据与坐标系**：`Axes` 对象定义了数据在图表中的坐标系，所有绘制的元素都基于这个坐标系进行定位和缩放。 --> 即, 在子图中的索引位置
```python
ax.plot(x, y)  # 绘制数据，x 和 y 是在 Axes 的坐标系下的值
```

### **d. Artists 的概念**

- **Artists**：Matplotlib 中的所有可视化元素（如线条、文本、补丁等）都是 `Artists` 对象。`Axes` 是一个复杂的 `Artist`，而具体的图形元素（如 `Line2D`、`Text`、`Patch` 等）也是 `Artists`。

```python
line, = ax.plot(x, y)  # Line2D 对象也是一个 Artist
rect = patches.Rectangle((0.1, 0.1), 0.5, 0.5, linewidth=1, edgecolor='r', facecolor='none')
ax.add_patch(rect)  # 添加一个 Patch Artist
```

### **e. 坐标轴刻度（Ticks）和网格（Grid）**

- **Ticks**：坐标轴上的刻度线和标签，用于指示数据的位置。
    
- **Grid**：基于 Ticks 绘制的网格线，帮助用户更好地读取图表中的数据。

```python
ax.set_xticks([0, 1, 2, 3])
ax.set_xticklabels(['A', 'B', 'C', 'D'])
ax.grid(True)  # 启用网格
``` 

### **f. Subplot 与 Axes**

- **Subplot**：通常指 Figure 中的一个 Axes 对象。`plt.subplot` 或 `plt.subplots` 用于创建多个 Axes。

``` python
fig, axs = plt.subplots(2, 2)  # 创建4个 Subplots，即4个 Axes
``` 

### **g. 索引和引用 Axes**

- **单个 Axes**：
```python
fig, ax = plt.subplots()
``` 
- **多个 Axes**：
```python
fig, axs = plt.subplots(2, 2)
axs[0, 0].plot(x1, y1)
axs[0, 1].plot(x2, y2)
axs[1, 0].plot(x3, y3)
axs[1, 1].plot(x4, y4)
``` 

## 3. 其他容易产生疑问的地方

### **a. 坐标轴共享（Sharex 和 Sharey）**

- **共享坐标轴**：在创建多个 Axes 时，可以设置它们共享同一个 X 轴或 Y 轴，便于比较不同数据集。

```
fig, (ax1, ax2) = plt.subplots(2, 1, sharex=True)
```

### **b. Figure 大小和分辨率**

- **设置 Figure 大小**：使用 `figsize` 参数指定 Figure 的宽度和高度（单位为英寸）。
    
    `fig, ax = plt.subplots(figsize=(10, 6))`
    
- **设置分辨率**：使用 `dpi` 参数指定每英寸的点数，影响图像的清晰度。

    `fig, ax = plt.subplots(figsize=(10, 6), dpi=100)`
    

### **c. 自动调整布局**

- **紧凑布局**：使用 `tight_layout` 或 `constrained_layout` 自动调整子图之间的间距，避免标签重叠。

    `fig, axs = plt.subplots(2, 2, figsize=(10, 8)) fig.tight_layout()  # 自动调整子图布局`
    

### **d. 保存 Figure**

- **保存图表**：使用 `savefig` 方法将 Figure 保存为文件。

    `fig.savefig('my_plot.png', dpi=300, bbox_inches='tight')`
    

### **e. 坐标轴方向和比例**

- **对数坐标**：设置坐标轴为对数尺度。

    `ax.set_xscale('log') ax.set_yscale('log')`
    
- **设置比例**：如等比例（`equal`）、自动比例（`auto`）。

    `ax.set_aspect('equal')`
    

### **f. 标题和标签**

- **Figure 标题**：使用 `fig.suptitle` 设置整个 Figure 的标题。

    `fig.suptitle('Main Title for the Figure')`
    
- **Axes 标题**：使用 `ax.set_title` 设置单个 Axes 的标题。

    `ax.set_title('Subplot Title')`
    

### **g. 注释和文本**

- **添加注释**：使用 `ax.annotate` 在图表中添加注释。

    `ax.annotate('Peak', xy=(x_peak, y_peak), xytext=(x_peak + 1, y_peak + 1),             arrowprops=dict(facecolor='black', shrink=0.05))`
    
- **添加文本**：使用 `ax.text` 在指定位置添加文本。

    `ax.text(0.5, 0.5, 'Center Text', transform=ax.transAxes)`
    

### **h. 图例（Legend）**

- **添加图例**：使用 `ax.legend` 添加图例，帮助区分不同的数据系列。

    `ax.plot(x, y, label='Data 1') ax.plot(x, z, label='Data 2') ax.legend()`
    

### **i. 事件处理和交互**

- **连接事件**：使用 `mpl_connect` 连接 Matplotlib 的事件，如鼠标点击、移动等，实现交互功能。

```python
def on_click(event):
    print(f'You clicked on {event.xdata}, {event.ydata}')

fig.canvas.mpl_connect('button_press_event', on_click)
``` 

## 4. 总结

理解 `Figure` 和 `Axes` 以及它们之间的关系，是掌握 Matplotlib 的基础。以下是关键点的总结：

- **Figure**：整个图表窗口或画布，可以包含多个 `Axes`。
- **Axes**：图表中的单个绘图区域，包含坐标轴、标题、标签等，用于绘制具体的数据。
- **Axis**：具体的坐标轴，如 X 轴或 Y 轴。
- **Artists**：图表中的所有可视化元素，包括 `Figure`、`Axes`、`Line2D`、`Patch` 等。

**常见误区**：

1. **混淆 Figure 和 Axes**：记住 `Figure` 是整个图表，`Axes` 是图表中的子图。
2. **单数和复数**：`Axes` 是 `Axis` 的复数形式，`Axes` 表示绘图区域，`Axis` 表示坐标轴。
3. **坐标系理解**：`Axes` 定义了数据在图表中的坐标系，所有数据元素都基于此坐标系进行定位。
4. **事件处理的理解**：在使用交互功能时，清楚事件是如何绑定到 `Figure` 或 `Axes` 的。


## 1. Figure 和 FigureCanvas 的关系
在 Matplotlib 中，`FigureCanvas` 可以包含一个 `Figure` 对象。这是 Matplotlib 与图形用户界面（如 PyQt5）集成的基础。`FigureCanvas` 充当了 Matplotlib 图形在 GUI 中的渲染器，而 `Figure` 则是实际的图形内容。下面将详细解释两者的关系以及如何在 PyQt5 中正确使用它们。
### **Figure**

- **定义**：`Figure` 是 Matplotlib 中的*顶级容器*，表示整个图表或画布。它可以包含多个 `Axes`（子图），以及图例、标题等其他图形元素。
- **作用**：负责管理图表的整体布局、大小以及包含的所有子图和图形元素。

### **FigureCanvas**

- **定义**：`FigureCanvas` 是 Matplotlib 的*后端类*，负责将 `Figure` 渲染到特定的 GUI 框架中。在 PyQt5 中，通常使用 `FigureCanvasQTAgg` 作为 `FigureCanvas` 的实现。
- **作用**：作为一个 *QWidget*，`FigureCanvas` 允许将 Matplotlib 的 `Figure` 嵌入到 PyQt5 的窗口或布局中，从而实现图形的显示和交互。

### **关系**

- **包含关系**：`FigureCanvas` **包含** 一个 `Figure` 对象。`Figure` 通过 `FigureCanvas` 在 GUI 中进行渲染和显示。
- **层级结构**：
```python
PyQt5 Widget
└── FigureCanvas (FigureCanvasQTAgg)
    └── Figure
        └── Axes
            └── 图形元素（线条、文本、补丁等）
``` 

## 2. 如何在 PyQt5 中使用 FigureCanvas 包含 Figure

以下是一个简单的示例，展示如何在 PyQt5 的 GUI 中嵌入 Matplotlib 的 `Figure` 通过 `FigureCanvasQTAgg`。

### **示例代码**
```python
import sys
import numpy as np
from PyQt5.QtWidgets import QApplication, QMainWindow, QVBoxLayout, QWidget
from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg as FigureCanvas
from matplotlib.figure import Figure

class MplCanvas(FigureCanvas):
    def __init__(self, parent=None, width=5, height=4, dpi=100):
        # 创建一个 Figure 对象
        self.fig = Figure(figsize=(width, height), dpi=dpi)
        # 初始化 FigureCanvas，传入 Figure 对象
        super(MplCanvas, self).__init__(self.fig)
        # 添加一个子图
        self.ax = self.fig.add_subplot(111)

class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()

        self.setWindowTitle("Matplotlib in PyQt5 Example")

        # 创建一个主窗口部件
        self.main_widget = QWidget(self)
        self.setCentralWidget(self.main_widget)

        # 创建一个垂直布局
        layout = QVBoxLayout(self.main_widget)

        # 初始化 FigureCanvas（包含 Figure）
        sc = MplCanvas(self, width=5, height=4, dpi=100)
        sc.ax.plot(np.random.rand(10))  # 绘制一些随机数据

        # 将 FigureCanvas 添加到布局中
        layout.addWidget(sc)

        self.show() # 显示窗口

def main():
    app = QApplication(sys.argv)
    window = MainWindow()
    sys.exit(app.exec_())

if __name__ == '__main__':
    main()
```

### **运行效果**

运行上述代码后，将会看到一个包含随机数据折线图的 PyQt5 窗口。这说明 `FigureCanvas` 成功地包含并显示了 `Figure` 对象。

## 3. 常见疑问解答

### **a. `FigureCanvas` 是否必须包含一个 `Figure` 对象？**

是的，`FigureCanvas` 的主要职责是渲染和显示一个 `Figure` 对象。因此，在使用 `FigureCanvas` 时，通常需要创建一个 `Figure` 并将其传递给 `FigureCanvas`。

### **b. 如何在现有的 `FigureCanvas` 中更改 `Figure`？**

如果需要更改 `Figure`（例如，重新绘制图形），可以直接操作 `Figure` 对象，然后调用 `draw()` 方法刷新显示。例如：

```python
sc.ax.clear()  # 清除当前 Axes
sc.ax.plot(new_data)  # 绘制新数据
sc.draw()  # 刷新 FigureCanvas
``` 

### **c. `FigureCanvas` 和 `Figure` 的生命周期关系如何？**

- **生命周期管理**：`FigureCanvas` 通常负责管理 `Figure` 的生命周期。在创建 `FigureCanvas` 时传入 `Figure`，后者由 `FigureCanvas` 持有和渲染。
- **内存管理**：确保在不需要时适当删除或清理 `FigureCanvas` 和 `Figure`，以避免内存泄漏，尤其是在动态创建和销毁多个图形时。

### **d. 如何在 `FigureCanvas` 中添加多个子图（Axes）？**

可以在 `Figure` 中使用 `add_subplot` 或 `subplots` 方法创建多个 `Axes`。例如：

```python
class MplCanvas(FigureCanvas):
    def __init__(self, parent=None, width=5, height=4, dpi=100):
        self.fig = Figure(figsize=(width, height), dpi=dpi)
        super(MplCanvas, self).__init__(self.fig)
        self.ax1 = self.fig.add_subplot(211)  # 上方子图
        self.ax2 = self.fig.add_subplot(212)  # 下方子图

# 然后在主窗口中分别绘制不同的数据：
sc.ax1.plot(data1)
sc.ax2.plot(data2)
sc.draw()

``` 

### **e. 如何处理交互事件（如点击、拖动）？**

可以使用 Matplotlib 的事件处理机制，通过 `mpl_connect` 方法连接特定事件到回调函数。例如：

```python
def on_click(event):
    if event.inaxes == sc.ax1:
        print("Clicked on ax1")

sc.mpl_connect('button_press_event', on_click)
``` 
在 PyQt5 中，这些事件处理机制与 GUI 的事件循环集成，可以实现复杂的交互功能。

### **f. 如何调整 `FigureCanvas` 的大小以适应窗口调整？**

使用布局管理器（如 `QVBoxLayout`）可以自动调整 `FigureCanvas` 的大小以适应窗口大小变化。确保在创建 `FigureCanvas` 时设置合适的 `sizePolicy`，例如：

```python
from PyQt5.QtWidgets import QSizePolicy

sc = MplCanvas(self, width=5, height=4, dpi=100)
sc.setSizePolicy(QSizePolicy.Expanding, QSizePolicy.Expanding)
sc.updateGeometry()
``` 

这样，当窗口调整大小时，`FigureCanvas` 会自动扩展或收缩以填充可用空间。

## 4. 进一步优化和扩展

### **a. 使用 `NavigationToolbar`**

可以添加 Matplotlib 的导航工具栏，以提供缩放、平移、保存图像等功能。

```python
from matplotlib.backends.backend_qt5agg import NavigationToolbar2QT as NavigationToolbar

toolbar = NavigationToolbar(sc, self)
layout.addWidget(toolbar)
``` 

### **b. 动态更新图形**

如果需要实时更新图形（例如，实时数据监控），可以在定时器中更新 `Figure` 并调用 `draw()`。
```python
from PyQt5.QtCore import QTimer

def update_plot():
    sc.ax.plot(new_data)
    sc.draw()

timer = QTimer()
timer.timeout.connect(update_plot)
timer.start(1000)  # 每秒更新一次
``` 

### **c. 多线程和数据处理**

在处理大量数据或复杂计算时，考虑使用多线程或异步编程，以避免阻塞 GUI 线程。使用 `QThread` 或 `concurrent.futures` 模块来处理后台任务。

## 5. 总结

- **`FigureCanvas` 包含 `Figure`**：在 Matplotlib 与 PyQt5 集成时，`FigureCanvas` 作为渲染器，包含并显示一个 `Figure` 对象。
- **创建和嵌入**：通过创建 `Figure`，将其传递给 `FigureCanvas`，然后将 `FigureCanvas` 添加到 PyQt5 的布局中，实现图形的显示。
- **交互和扩展**：利用 Matplotlib 的事件处理机制和 PyQt5 的布局管理，可以实现丰富的交互功能和动态更新。



