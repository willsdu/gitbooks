# goxorm工具反转数据库，生成代码

## 引入
使用 golang 操作数据库的同学都会遇到一个问题 —— 根据数据表结构创建对应的 struct 模型。因为 golang 的使用首字母控制可见范围，我们经常要设计 struct 字段名和数据库字段名的对应关系。久而久之，这是一个非常繁琐的过程。事情变得繁琐了，我们都会想，有没有好的办法自动生成 model 呢？今天，记录一种自动生成代码的方法 —— xorm 工具

关于xorm的更多信息，可以浏览：http://www.xorm.io/

## 安装 
首先我们要下载该工具 
```
go get github.com/go-xorm/cmd/xorm
```

同时根据需要，安装对应的 driver 
```
go get github.com/go-sql-driver/mysql  //MyMysql
go get github.com/ziutek/mymysql/godrv  //MyMysql
go get github.com/lib/pq  //Postgres
go get github.com/mattn/go-sqlite3  //SQLite
```

还需要下载 xorm
```
go get github.com/go-xorm/xorm
```

## 使用
在项目目录下建立templates/goxorm 文件夹，在这个文件夹下面建立config和struct.go.tpl文件。模板的内容可以自己修改
config
```
lang=go
genJson=0
prefix=cos_
ignoreColumnsJSON=
created=
updated=
deleted=
```

struct.go.tpl
```
package {{.Models}}

{{$ilen := len .Imports}}
{{if gt $ilen 0}}
import (
	{{range .Imports}}"{{.}}"{{end}}
)
{{end}}

{{range .Tables}}
type {{Mapper .Name}} struct {
{{$table := .}}
{{range .ColumnsSeq}}{{$col := $table.GetColumn .}}	{{Mapper $col.Name}}	{{Type $col}} {{Tag $table $col}}
{{end}}
}
{{end}}
```
最后执行
```
xorm reverse mysql root:123456@(localhost:3306)/gaodun_tag?charset=utf8 ./templates/goxorm
```
然后在templates/models文件下面会生成所有表的struct


## 参考

[使用xorm工具，根据数据库自动生成 go 代码](https://my.oschina.net/u/3626804/blog/2967310)
[golang xorm cmd xorm工具使用 reverse 反转一个数据库结构，生成代码](https://blog.csdn.net/fenglailea/article/details/80213833)
