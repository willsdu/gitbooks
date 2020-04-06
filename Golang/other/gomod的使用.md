# go mod使用教程
Go mod是golang 1.11的一个新的特性，初衷是为了解决Go糟糕的包管理，但是吧，目前使用来看，还有很多需要解决的问题，不过使用go mod，其他第三方包管理工具可以不使用了

## 命令
go mod的使用很简单，按照帮助文档上的，可以快速入门
```
go help modules

go mod命令

download    download modules to local cache (下载依赖的module到本地cache))
edit        edit go.mod from tools or scripts (编辑go.mod文件)
graph       print module requirement graph (打印模块依赖图))
init        initialize new module in current directory (再当前文件夹下初始化一个新的module, 创建go.mod文件))
tidy        add missing and remove unused modules (增加丢失的module，去掉未用的module)
vendor      make vendored copy of dependencies (将依赖复制到vendor下)
verify      verify dependencies have expected content (校验依赖)
why         explain why packages or modules are needed (解释为什么需要依赖)

初始化mod

go mod init [module]可以创建一个go.mod，只有一行信息module。
```

## 设置

GO111MODULE=off 无模块支持，go 会从 GOPATH 和 vendor 文件夹寻找包。
GO111MODULE=on  模块支持，go 会忽略 GOPATH 和 vendor 文件夹，只根据 go.mod 下载依赖。
GO111MODULE=auto 在 GOPATH/src 外面且根目录有 go.mod 文件时，开启模块支持。

## replace
常用的谷歌包的replace
```
replace (
    golang.org/x/text => github.com/golang/text v0.3.2
    golang.org/x/net => github.com/golang/net v0.0.0-20190724013045-ca1201d0de80
    golang.org/x/crypto => github.com/golang/crypto v0.0.0-20190701094942-4def268fd1a4
    golang.org/x/tools => github.com/golang/tools v0.0.0-20190809145639-6d4652c779c4
    golang.org/x/sync => github.com/golang/sync v0.0.0-20190423024810-112230192c58
    golang.org/x/sys => github.com/golang/sys v0.0.0-20190804053845-51ab0e2deafa
    cloud.google.com/go => github.com/googleapis/google-cloud-go v0.44.0
    google.golang.org/genproto => github.com/google/go-genproto v0.0.0-20190801165951-fa694d86fc64
    golang.org/x/exp => github.com/golang/exp v0.0.0-20190731235908-ec7cb31e5a56
    golang.org/x/time => github.com/golang/time v0.0.0-20190308202827-9d24e82272b4
    golang.org/x/oauth2 => github.com/golang/oauth2 v0.0.0-20190604053449-0f29369cfe45
    golang.org/x/lint => github.com/golang/lint v0.0.0-20190409202823-959b441ac422
    google.golang.org/grpc => github.com/grpc/grpc-go v1.22.1
    google.golang.org/api => github.com/googleapis/google-api-go-client v0.8.0
    google.golang.org/appengine => github.com/golang/appengine v1.6.1
    golang.org/x/mobile => github.com/golang/mobile v0.0.0-20190806162312-597adff16ade
    golang.org/x/image => github.com/golang/image v0.0.0-20190802002840-cff245a6509b
)
```

## 代理
很多包可能无法下载，特别是谷歌的一些包，这里推荐使用代理,第二个可能不好用了，建议使用第一个
```
export GOPROXY=https://athens.azurefd.net
export GOPROXY=https://goproxy.io
```

## 常见问题
1. 如果出现 ```xxx missing module line```等错误，可以参考[issue](https://github.com/bilibili/kratos/issues/231)上的解决办法，将$PATH/pkg/mod下面的缓存删掉，不使用https://goproxy.io ,换个代理

