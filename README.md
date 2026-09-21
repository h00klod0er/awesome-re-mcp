# Awesome Reverse-Engineering MCP & Tools

专门收集**逆向工程相关 MCP**与**AI 辅助逆向工具**的精选清单。欢迎 PR 补充最新项目。

> 范围：二进制逆向 / 反汇编 / 反编译 / 调试 / 恶意样本分析相关的 MCP Server、Agent 插件与配套工具。  
> 不含：通用编程助手、与 RE 无关的安全扫描器。

## 目录

- [MCP · IDA](#mcp--ida)
- [MCP · Ghidra](#mcp--ghidra)
- [MCP · Binary Ninja](#mcp--binary-ninja)
- [MCP · radare2 / 多后端](#mcp--radare2--多后端)
- [相关工具与框架](#相关工具与框架)
- [收录规范](#收录规范)

---

## MCP · IDA

| 项目 | 说明 | 备注 |
|------|------|------|
| [jtsylve/re-mcp](https://github.com/jtsylve/ida-mcp) (`re-mcp-ida`) | 无头 IDA/Ghidra 多后端 MCP；共用工具接口 | 原 `ida-mcp`，需 IDA Pro 9+ / idalib |
| [HexRaysSA/ida-mcp](https://github.com/HexRaysSA/ida-mcp) | Hex-Rays 官方实验性 IDA MCP | 需 IDA 9.4+；建议关掉其它 IDA MCP 以免工具冲突 |

## MCP · Ghidra

| 项目 | 说明 | 备注 |
|------|------|------|
| [re-mcp-ghidra](https://pypi.org/project/re-mcp-ghidra/) | `re-mcp` 的 Ghidra 后端（pyghidra，无头） | Ghidra 12+、JDK 21+ |
| [LaurieWired/GhidraMCP](https://github.com/LaurieWired/GhidraMCP) | 社区热门 Ghidra MCP（插件 + HTTP） | 交互式 GUI 工作流常用 |
| [bethington/ghidra-mcp](https://github.com/bethington/ghidra-mcp) | 大规模工具集 Ghidra MCP（约 110 tools） | LaurieWired 生态相关分支/扩展 |
| [wooyunsec/ghidra-headless-mcp](https://github.com/wooyunsec/ghidra-headless-mcp) | 无头 Ghidra MCP（大量工具组） | 适合 Agent / CI |

## MCP · Binary Ninja

| 项目 | 说明 | 备注 |
|------|------|------|
| [fosdickio/binary_ninja_mcp](https://github.com/fosdickio/binary_ninja_mcp) | BN 插件 + MCP bridge | 支持 Cursor / Claude / Cline 等自动配置 |
| [mrphrazer/binary-ninja-headless-mcp](https://github.com/mrphrazer/binary-ninja-headless-mcp) | 无头 BN MCP（约 180+ tools） | 适合 Agent 深度分析 |
| [jtang613/BinAssistMCP](https://github.com/jtang613/BinAssistMCP) / BinAssistMCP | BN 插件 MCP（SSE / Streamable HTTP） | 多 binary 会话、prompts |

## MCP · radare2 / 多后端

| 项目 | 说明 | 备注 |
|------|------|------|
| [radareorg/radare2-mcp](https://github.com/radareorg/radare2-mcp) | 官方 radare2 MCP | 可用 `r2pm` 安装 |
| [jtsylve/re-mcp](https://github.com/jtsylve/ida-mcp) | IDA + Ghidra 统一接口 | 后续后端可扩展 |

## 相关工具与框架

| 项目 | 说明 |
|------|------|
| [vector35/warp](https://github.com/vector35/warp) | Binary Ninja WARP（函数匹配 / 迁移相关） |
| [MCP](https://modelcontextprotocol.io/) | Model Context Protocol 规范本身 |

---

## 收录规范

提交 PR 时请尽量提供：

1. **链接**（GitHub / PyPI / 官方文档）
2. **一句话说明**（后端：IDA / Ghidra / BN / r2 / 其它）
3. **传输方式**（stdio / HTTP / SSE）与大致能力（反编译、xref、patch…）
4. **维护状态**（最近提交 / release 时间，若已知）
5. **许可与依赖**（是否需要商业 License，如 IDA / BN）

优先收录：活跃维护、文档清晰、可被 Cursor / Claude Code / 其它 MCP Client 直接接入的项目。

### 建议条目格式

```md
| [org/name](https://github.com/org/name) | 一句话说明 | 关键备注 |
```

---

## 免责声明

本仓库仅作**工具与项目索引**。请遵守当地法律与软件许可；仅在你有权分析的样本 / 二进制上使用。

---

## License

清单内容采用 [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/)（条目描述可自由复用；所列第三方项目保留各自许可证）。
