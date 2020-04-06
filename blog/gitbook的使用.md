
## 安装
gitbook需要[node](https://nodejs.org/#download)环境，真正的安装就是一个命令
```
npm install -g gitbook-cli
```
gitbook -V 
查看gitbook是否安装成功。

## 使用
* README.md

这个文件相当于一本Gitbook的简介，可以手动生成

* SUMMARY.md

这个文件是一本书的目录结构，使用Markdown语法，生成方法和README.md一样

#### 图书结构的生成
在SUMMARY.md中输入下面的内容
```
* [简介](README.md)
* [第一章](chapter1/README.md)
 - [第一节](chapter1/section1.md)
 - [第二节](chapter1/section2.md)
* [第二章](chapter2/README.md)
 - [第一节](chapter2/section1.md)
 - [第二节](chapter2/section2.md)
* [结束](end/README.md)
```

#### 生成图书结构
当这个目录文件创建好之后，我们可以使用Gitbook
的命令行工具将这个目录结构生成相应的目录及文件：
```$ gitbook init```
使用 ```tree .```查看建立的目录和文件
```
├── chapter1
│   ├── README.md
│   ├── section1.md
│   └── section2.md
├── chapter2
│   ├── README.md
│   ├── section1.md
│   └── section2.md
├── end
│   └── README.md
├── README.md
└── SUMMARY.md
```
我们可以看到，gitbook给我们生成了与SUMMARY.md所对应的目录及文件。每个目录中，都有一个README.md文件，相当于一章的说明。

#### 本地预览时自动生成
当你在自己的电脑上编辑好图书之后，你可以使用Gitbook的命令行进行本地预览：
```
gitbook serve .
```
然后浏览器中输入 http://localhost:4000 就可以预览生成的以网页形式组织的书籍。然后在你的图书项目的目录中多了一个名为_book的文件目录，而这个目录中的文件，即是生成的静态
网站内容。

#### 输出为静态网站
使用build参数生成到指定目录，与直接预览生成的静态网站文件不一样的是，使用这个命令你可以将内容输入到你所想要的目录中去
```
mkdir /tmp/gitbook
gitbook build --output=/tmp/gitbook
```

参考资料
* https://blog.csdn.net/xiaocainiaoshangxiao/article/details/46882921