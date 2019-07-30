# ISSUE

## tag

```go
type Mini struct {
    Addr string `yaml:"addr"`  // 这里如果修改为 `yaml: "addr"` 这种格式会出错，拿不到想要的内容
    Port int    `yaml:"port"`
}
```

## 解决被屏蔽的库下载问题

X的源码已经被同步到github，只要找到对应即可, 以下作为参考，其他类似
```
git clone https://github.com/golang/tools.git $GOPATH/src/golang.org/x/tools
git clone https://github.com/golang/lint.git $GOPATH/src/golang.org/x/lint

```

vscode 中的一些需要的golang插件被屏蔽， 可以在安装好上边的源码后，参考如下处理

```
cd $GOPATH
go install golang.org/x/lint/golint // 安装golint
```