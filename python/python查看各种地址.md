### 三个版本的路径如下：

*   python2.6的路径为：/System/Library/Frameworks/Python.framework/Versions/2.6
*   python2.7的路径为：/System/Library/Frameworks/Python.framework/Versions/2.7
*   python3.6的路径为：/Library/Frameworks/Python.framework/Versions/3.6 

    * * *

### 查看python路径的两种方法(以python3.6为例)：

*   `which python3.6`
*   使用python的sys库

```
import sys
print(sys.path)
```

* * *

### HomeBrew、Pyenv、OpenCV的注意事项

*   HomeBrew安装的第三方包在 /usr/local/Cellar/ 目录下
*   `brew install opencv` 的时候会下载opencv的依赖库(numpy,python2)
*   HomeBrew会在 /usr/local/lib/python2.7/site-packages 目录下建立 cv2.so -> /usr/local/Cellar/opencv/3.3.0_3/lib/python2.7/site-packages/ 的软链接
*   要在导入模块识别到opencv的话，需要做如下操作： 

    *   `mkdir -p /Users/weisuzhong/.local/lib/python2.7/site-packages`
    *   `echo 'import site; site.addsitedir("/usr/local/lib/python2.7/site-packages")' >> /Users/weisuzhong/.local/lib/python2.7/site-packages/homebrew.pth`

当然我这个是根据HomeBrew安装opencv的提示来的

* * *

### 第三方库的安装路径(pip)

1.  系统自带的python : /System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/
2.  pyenv安装的python : /Users/weisuzhong/.pyenv/versions/2.7.10/lib/python2.7/site-packages/





1、terminal : 

input: which [Python](http://lib.csdn.net/base/11 "undefined")

2、terminal:

input : python  --->import sys  ----> print sys.path

3、mac版Pycharm第三方库路径

/Library/Python/2.7/lib/python/site-packages
