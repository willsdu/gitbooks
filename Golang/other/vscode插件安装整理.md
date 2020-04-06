# VScode Golang 插件安装教程


## 背景 
vscode算是微软出品的比较良心的产品，轻量级，界面漂亮，插件丰富，支持很多语言的开发。我就使用vscode开发Golang，但是由于我们的网络被"qiang"了，没办法和顺滑的安装插件，但是谷歌的大神们还是给出了办法。


## 插件工具
首先安装插件
[安装插件](../image/golang/vscode_plugin.png)

安装插件工具
按组合键```Ctrl + Shift + P```，在输入框中输入```go: install```找到下图红框选项
[安装插件工具](../image/golang/vscode_install.png)

然后选中所有工具
[所有工具](../image/golang/vscode_plugin_tools.png)
即时翻qiang，你也会失败


## 解决
谷歌将代码放到github上了,可以将代码克隆下来再安装
```
git clone https://github.com/golang/sys.git $GOPATH/src/golang.org/x/sys
git clone https://github.com/golang/crypto.git $GOPATH/src/golang.org/x/crypto
git clone https://github.com/golang/text.git $GOPATH/src/golang.org/x/text
git clone https://github.com/golang/tools.git $GOPATH/src/golang.org/x/tools
git clone https://github.com/golang/lint.git $GOPATH/src/golang.org/x/lint
git clone https://github.com/golang/blog.git $GOPATH/src/golang.org/x/blog
git clone https://github.com/golang/exp.git $GOPATH/src/golang.org/x/exp
git clone https://github.com/golang/image.git $GOPATH/src/golang.org/x/image
git clone https://github.com/golang/mobile.git $GOPATH/src/golang.org/x/mobile
git clone https://github.com/golang/net.git $GOPATH/src/golang.org/x/net
git clone https://github.com/golang/review.git $GOPATH/src/golang.org/x/review
git clone https://github.com/golang/sync.git $GOPATH/src/golang.org/x/sync
git clone https://github.com/golang/talks.git $GOPATH/src/golang.org/x/talks
```
安装
```
$ go install github.com/mdempsky/gocode
$ go install github.com/uudashr/gopkgs/cmd/gopkgs
$ go install github.com/ramya-rao-a/go-outline
$ go install github.com/acroca/go-symbols
$ go install golang.org/x/tools/cmd/guru
$ go install golang.org/x/tools/cmd/gorename
$ go install github.com/derekparker/delve/cmd/dlv
$ go install github.com/rogpeppe/godef
$ go install golang.org/x/tools/cmd/godoc
$ go install github.com/sqs/goreturns
$ go install github.com/golang/lint/golint
$ go install github.com/cweill/gotests/gotests
$ go install github.com/fatih/gomodifytags
$ go install github.com/josharian/impl
$ go install github.com/davidrjenni/reftools/cmd/fillstruct
$ go install github.com/haya14busa/goplay/cmd/goplay
```

## Go插件配置
|值|描述|
|--|--|
|go.gopath|配置gopath|
|go.goroot|配置goroot|
|go.autocompleteUnimportedPackages|自动补充没有导入的包|


## 参考
[Linux vscode基本配置以及golang插件安装](https://blog.csdn.net/luckytanggu/article/details/85004725)