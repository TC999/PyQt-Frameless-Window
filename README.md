# PyQt Frameless Window

## Features
* Move
* Stretching
* Window animation
* Window DWM shadow
* Win10 acrylic blur
* Win7 Aero blur

## Examples
* Normal frameless window
![Normal Frameless Window](screenshot/normal_frameless_window.gif)
* Acrylic frameless window
![Acrylic Frameless Window](screenshot/Acrylic_window.gif)

## Blogs
* [如何在pyqt中通过调用SetWindowCompositionAttribute实现Win10亚克力效果](https://www.cnblogs.com/zhiyiYo/p/14643698.html)
* [如何在pyqt中给无边框窗口添加DWM环绕阴影](https://www.cnblogs.com/zhiyiYo/p/14644155.html)
* [如何在pyqt中在实现无边框窗口的同时保留Windows窗口动画效果（一）](https://www.cnblogs.com/zhiyiYo/p/14644099.html)
* [如何在pyqt中在实现无边框窗口的同时保留Windows窗口动画效果（二）](https://www.cnblogs.com/zhiyiYo/p/14644180.html)

## Notes
1. `FramelessWindow` provides a custom title bar. If you don't like it, you can rewrite it;
2. The default style of `FramelessWindow` is borderless window with DWM shadow. If you want other special effects, such as acrylic effect, you can rewrite the `__init__()` function of `FramelessWindow`. Here is an example:
    ```python
    def __init__(self, parent=None):
        super().__init__(parent)
        self.monitor_info = None
        self.titleBar = TitleBar(self)
        self.windowEffect = WindowEffect()
        # remove border
        self.setWindowFlags(Qt.FramelessWindowHint | Qt.WindowSystemMenuHint |
                            Qt.WindowMinimizeButtonHint | Qt.WindowMaximizeButtonHint)
        self.setStyleSheet('background:transparent')
        # Add window animation and acrylic blur
        self.windowEffect.addWindowAnimation(self.winId())
        self.windowEffect.setAcrylicEffect(self.winId())
        self.resize(500, 500)
        self.titleBar.raise_()
    ```