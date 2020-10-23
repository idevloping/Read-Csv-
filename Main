import csv
import os
import sys
from os.path import dirname, realpath,join
from PyQt5.QtGui import QIcon
from PyQt5.QtWidgets import QApplication, QMainWindow,QVBoxLayout,QAction,QFileDialog
from PyQt5.uic import  loadUiType
from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg as FigureCanvas
from matplotlib.figure import Figure

scriptDir=dirname(realpath(__file__))
From_Main,_= loadUiType(join(dirname(__file__),"main.ui"))

class Sheet(QMainWindow,From_Main):
    def __init__(self):
        super(Sheet, self).__init__()
        QMainWindow.__init__(self)
        self.setupUi(self)
        self.ToolBar()
        self.sc =myCanvas()
        self.l=QVBoxLayout(self.frame)
        self.l.addWidget(self.sc)

    def ToolBar(self):
        AddFile = QAction(QIcon('images.png'),'Add File',self)
        AddFile.triggered.connect(self.open_sheet)
        self.toolBar= self.addToolBar('Add data File')
        self.toolBar.addAction(AddFile)
        AddPlot = QAction(QIcon('Scatter.png'),'Scatter',self)
        AddPlot.triggered.connect(self.Plot)
        self.toolBar.addAction(AddPlot)

    def open_sheet(self):
        #QFileDialog.getOpenFileName((self,'Open CSV',),os.getenv('Home', 'CSV(*.)'))
        path = QFileDialog.getOpenFileName(self, "Open", "", "CSV Files (*.csv);;All Files (*)")
        if path[0]!='':
            self.FileN=path[0]

    def Plot(self):
        f=self.FileN
        index = int(self.lineEdit.text())
        x= []
        y=[]
        with open(f, newline = '') as csv_file:
            my_file = csv.reader(csv_file, delimiter = ',',
                                 quotechar = '|')
            for row in my_file:
                x.append(str(row[0]))
                y.append(str(row[index]))
        self.sc.plot(x, y)


class myCanvas(FigureCanvas):
    def __init__(self):
        self.fig=Figure()
        FigureCanvas.__init__(self,self.fig)

    def plot(self,xarray,yarray):
        self.fig.clear()
        self.ax= self.fig.add_subplot(111)
        self.ax.plot(xarray[1:],yarray[1:])
        self.ax.set_xlabel(xarray[0])
        self.ax.set_ylabel(yarray[0])
        self.draw()

app = QApplication(sys.argv)
sheet= Sheet()
sheet.show()
sys.exit(app.exec_())
