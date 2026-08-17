# Bug 复现说明

## 固定基线

正式含 Bug 提交以 `main` 分支最终 SHA 为准；模型修复分支必须从该提交创建。

## 现象

`ConsoleWriter` 会先按 `PartsOrder` 渲染字段，再由 `writeFields` 输出剩余字段。当前剩余字段阶段只排除内置字段，没有排除 `PartsOrder` 已经渲染的自定义字段，也没有完整应用 `PartsExclude`，因此自定义字段可能重复输出或无法被排除。

## 唯一专项命令

```bash
go test . -run '^TestConsoleWriterConfiguration/PartsOrder_custom_fields_are_not_duplicated$' -count=1 -v
```

含 Bug 基线必须失败，修复后必须成功。模型不得修改任何测试文件。

## 通过条件

- `PartsOrder` 中的自定义字段只输出一次。
- `PartsExclude` 能抑制尾部阶段的自定义字段。
- 内置字段、格式化回调、字段排序与颜色行为不回归。
- 全量测试、`go vet ./...` 与 `go build ./...` 通过。
