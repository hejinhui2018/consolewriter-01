# ConsoleWriter 单题评测仓库

本仓库提供生产级 Go 结构化日志与控制台渲染组件。本题只评测 `ConsoleWriter` 的字段顺序与排除语义，不涉及业务系统、桌面工具或前端页面。

## 工具链

- `go.mod`：Go 1.23
- Docker：`golang:1.23.12`
- `GOTOOLCHAIN=local`
- `CGO_ENABLED=0`

## 标准验证

专项命令：

```bash
go test . -run '^TestConsoleWriterConfiguration/PartsOrder_custom_fields_are_not_duplicated$' -count=1 -v
```

完整验收：

```bash
go test ./... -count=1
go vet ./...
go build ./...
```

Docker 双架构入口：

```bash
./build_benzhi_docker.sh linux/amd64
./build_benzhi_docker.sh linux/arm64
```
