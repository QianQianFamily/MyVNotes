# Quick Note

## QMainWindow Layout
QMainWindow objects come with their own customized layout and setting a layout on a the actual main window, or creating a layout with a main window as a parent, is considered an error. You should always set your own layout on the central widget instead. See [Document](http://doc.qt.io/qt-5/qtwidgets-mainwindows-menus-example.html) for detail.
```c++

    QWidget *widget = new QWidget;
    setCentralWidget(widget);

    QWidget* topFiller = new QWidget;
    topFiller->setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding);

    infoLabel = new QLabel(tr("<i>Choose a menu option"));
    infoLabel->setFrameStyle(QFrame::StyledPanel | QFrame::Sunken);
    infoLabel->setAlignment(Qt::AlignCenter);

    QWidget *bottomFiller = new QWidget;
    bottomFiller->setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding);

    QVBoxLayout *layout = new QVBoxLayout;
    layout->setMargin(5);
    layout->addWidget(topFiller);
    layout->addWidget(infoLabel);
    layout->addWidget(bottomFiller);
    widget->setLayout(layout);
    setMinimumSize(160, 160);
    resize(480, 320);

```