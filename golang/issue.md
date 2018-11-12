# ISSUE

## tag

```go
type Mini struct {
    Addr string `yaml:"addr"`  // 这里如果修改为 `yaml: "addr"` 这种格式会出错，拿不到想要的内容
    Port int    `yaml:"port"`
}
```