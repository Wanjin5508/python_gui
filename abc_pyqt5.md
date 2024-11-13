
# pyqt5-FigureCanvas
参考: https://blog.csdn.net/m0_74202414/article/details/130815241

 Figure类似于画板，而Canvas类似于画纸

FigureCanvasXAgg就是一个渲染器，渲染器的工作就是drawing，执行绘图的这个动作。渲染器是使物体显示在屏幕上。

1. 通过`matplotlib.backends.backend_qt5agg` 类来连接 PyQt5, 涉及后端概念。

```c++
from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg as FigureCanvas
import matplotlib
matplotlib.use("Qt5Agg")
from matplotlib.figure import Figure
from matplotlib import pyplot
 
pyplot.rcParams['font.sans-serif'] = ['SimHei']
pyplot.rcParams['axes.unicode_minus'] = False
```

2. 实现具体的图形代码, 关键在每次绘图后, 需要 `self.fig.canvas.draw()` 刷新画布

```c++
class Figure_Canvas(FigureCanvas):    
    def __init__(self, parent=None, width=6, height=4, dpi=100):
        fig = Figure(figsize=(width, height), dpi=100)
        FigureCanvas.__init__(self, fig) # 初始化父类
        self.setParent(parent)
        self.axes = fig.add_subplot(111)
    #这里就是绘制图像、示例
    def month(self):
        x,y = month()  #获取x和y
        self.axes.plot(x, y, label='month', marker='o', color='b')       #使用axes进行绘图
        self.axes.set_title('WLG2')
        self.axes.plot(x, y)
    def year(self):
        x,y = year()
        self.axes.plot(x, y, label='year', marker='o',color='b')
        self.axes.set_title('WLG2')
        self.axes.plot(x, y)
 
    def demo(self):
        x, y = month()
        self.axes.plot(x, y, label='month', marker='o', color='b')
        self.axes.set_title('FUYANG-month')
        self.axes.plot(x, y)
 
    def demo2(self):
        x, y = demo2()
        self.axes.plot(x, y,label='23-years-average', marker='o', color='blue')
        self.axes.set_title('FUYANG-year')
        self.axes.plot(x, y)
```

3. GUI上, 通过 `QGraphicsView` 控件呈现matplotlib画出来的图形。
```python
        #获取graphicsView的长和宽单位为像素，Figure的单位是inches，在DPI为100时，除以100转换为inches
        width = self.graphicsView.width()
        height = self.graphicsView.height()
 
        self.myImage = Figure_Bar(width/100, height/100)
        self.myGraphyScene = QGraphicsScene()    #场景
        #取消水平和垂直滚动条
        self.graphicsView.setHorizontalScrollBarPolicy(Qt.ScrollBarAlwaysOff) 
        self.graphicsView.setVerticalScrollBarPolicy(Qt.ScrollBarAlwaysOff)
        self.myQGraphicsProxyWidget = self.myGraphyScene.addWidget(self.myImage)
        self.graphicsView.setScene(self.myGraphyScene)
 
        #每次显示不同图像，只需调用ShowImage方法
        self.myImage.ShowImage(self.axisXcontent, self.axisYcontent)
```

如通过按钮显示第二歩中的year（），将按钮连接即可。

详情见[Matplotlib植入PyQt5 + QT5的UI呈现_第三步,创建一个qgraphicsscene,因为加载的图形(figurecanvas)不能直接放到_CtrlZ1的博客-CSDN博客](https://blog.csdn.net/qq_41076797/article/details/84497381?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522168480624216800227434301%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=168480624216800227434301&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-84497381-null-null.142%5Ev87%5Econtrol_2,239%5Ev2%5Einsert_chatgpt&utm_term=graphicscene.addWidget&spm=1018.2226.3001.4187 "Matplotlib植入PyQt5 + QT5的UI呈现_第三步,创建一个qgraphicsscene,因为加载的图形(figurecanvas)不能直接放到_CtrlZ1的博客-CSDN博客")

```python
    def wlg2_year(self):
        wlg2_year = Figure_Canvas()#实例化类
        wlg2_year.year()#调用类方法，作图
        graphicscene = QtWidgets.QGraphicsScene()#创建一个QGraphicsScene，因为加载的图形（FigureCanvas）不能直接放到graphicview控件中，必须先放到graphicScene，然后再把graphicscene放到graphicview中
        graphicscene.addWidget(wlg2_year)#把图形放到QGraphicsScene中，注意：图形是作为一个QWidget放到QGraphicsScene中的
        self.graphicsView.setScene(graphicscene)#把QGraphicsScene放入QGraphicsView
        self.graphicsView.show()#调用show方法呈现图形
```

```python
if __name__ == '__main__':
    # 添加如下代码
    QtCore.QCoreApplication.setAttribute(QtCore.Qt.AA_EnableHighDpiScaling)
    app = QApplication(sys.argv)
    mainWindow = QMainWindow()
    ui = task.Ui_task()   #task
    ui.setupUi(mainWindow)
    mainWindow.show()
    sys.exit(app.exec_())

```




