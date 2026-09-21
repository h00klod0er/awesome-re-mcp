# Awesome Reverse-Engineering MCP & Tools

专门收集**逆向工程相关 MCP**与**AI 辅助逆向工具**的精选清单。欢迎 PR 补充最新项目。

> 范围：二进制逆向 / 反汇编 / 反编译 / 调试 / 动态插桩 / 符号执行相关的 MCP Server、Agent 插件与配套工具。  
> 不含：通用编程助手、与 RE 无关的安全扫描器。

> **统计说明（2026-09-21 06:18 UTC）**：`★` = GitHub Stars；`更新` = 仓库最近一次 `pushed_at`（推送）日期。由 [GitHub Actions](.github/workflows/update-stats.yml) 每周一自动刷新；也可手动 `workflow_dispatch`。PyPI-only 包无独立 star，会注明对应源码仓。

## 目录

- [主工具介绍](#主工具介绍)
- [MCP · x64dbg / x32dbg](#mcp--x64dbg--x32dbg)
- [MCP · IDA](#mcp--ida)
- [MCP · Ghidra](#mcp--ghidra)
- [MCP · Binary Ninja](#mcp--binary-ninja)
- [MCP · radare2 / 多后端](#mcp--radare2--多后端)
- [MCP · WinDbg](#mcp--windbg)
- [MCP · Frida](#mcp--frida)
- [MCP · angr](#mcp--angr)
- [相关工具与框架](#相关工具与框架)
- [收录规范](#收录规范)

---

## 主工具介绍

先弄清「宿主工具」是什么，再选对应 MCP。

### [x64dbg](https://x64dbg.com/) / x32dbg

开源 **Windows 用户态调试器**（由 [mrexodia](https://github.com/mrexodia) 等维护）。  
`x64dbg` 调试 64 位目标，`x32dbg` 调试 32 位目标；界面与插件体系相同，插件分别是 `.dp64` / `.dp32`。  
强项：动态调试、断点、内存/寄存器、脚本与庞大插件生态；弱项：静态反编译不如 IDA/Ghidra/BN。  
源码：[x64dbg/x64dbg](https://github.com/x64dbg/x64dbg) · ★49,566 · 更新 2026-09-19

### [IDA Pro](https://hex-rays.com/ida-pro/)

Hex-Rays 商业 **反汇编 / 反编译** 平台，行业默认之一。  
强项：反编译质量、交互式分析、处理器覆盖、IDC/IDAPython；动态调试也有，但很多人更爱配 x64dbg/WinDbg。  
MCP 多依赖 **IDA 9+ / idalib**；官方与社区实现并存，同时开多个 IDA MCP 容易让 Agent 工具冲突。

### [Ghidra](https://ghidra-sre.org/)

NSA 开源的 **软件逆向套件**（反汇编、反编译、脚本、协作项目）。  
强项：免费、多架构、可无头/批处理；弱项：部分架构体验与商业工具有差距。  
MCP 常见两条路：GUI 插件（边看边聊）与 **pyghidra 无头**（Agent / CI）。

### [Binary Ninja](https://binary.ninja/)

Vector 35 的商业（也有云/个人档）**反汇编平台**，以中间语言（IL）与 API 设计出名。  
强项：现代化 UI、脚本/插件、分析流水线；有 GUI 插件 MCP 与无头 MCP。  
配套：[WARP](https://github.com/vector35/warp)（★67 · 更新 2025-11-05）等函数匹配 / 迁移能力。

### [radare2](https://www.radare.org/) / [rizin](https://rizin.re/)

开源 **命令行向** 逆向框架（反汇编、调试、补丁、取证脚本）。  
强项：脚本化、跨平台、可嵌入；弱项：学习曲线陡。官方有 `radare2-mcp`（可用 `r2pm` 装）。

### [WinDbg](https://learn.microsoft.com/windows-hardware/drivers/debugger/) / DbgEng

微软 **Windows 调试器**（用户态 + 内核 KDNET、TTD 等）。  
强项：内核调试、驱动/崩溃转储、时间旅行调试（TTD）；弱项：交互与学习成本高。  
MCP 通常封装 DbgEng / dbgsrv / Preview 工具链。

### [Frida](https://frida.re/)

跨平台 **动态插桩** 框架（JS API hook、改内存、跟踪调用）。  
强项：运行时改行为、跨 OS/移动端；弱项：不是静态反编译器，常与 IDA/Ghidra/调试器联用。

### [angr](https://angr.io/)

开源 **二进制分析 / 符号执行** 框架（CFG、约束求解、路径探索），常配合 angr-management GUI。  
强项：自动化路径、漏洞研究向分析；弱项：大规模程序成本高、需会建约束。

---

## MCP · x64dbg / x32dbg

> 主工具：[x64dbg / x32dbg](#x64dbg--x32dbg)。多数方案同时提供 `.dp64` + `.dp32`，同一套 MCP 桥接两端。

| 项目 | ★ | 更新 | 说明 | 备注 |
|------|--:|------|------|------|
| [Wasdubya/x64dbgMCP](https://github.com/Wasdubya/x64dbgMCP) | 559| 2026-06-05| 早期流行方案：插件 + Python MCP，40+ SDK 工具 | 同时支持 x64/x32；Claude / Cursor 常用 |
| [SetsunaYukiOvO/x64dbg-mcp](https://github.com/SetsunaYukiOvO/x64dbg-mcp) | 480| 2026-08-21| 完整 MCP（约 79 tools + resources + prompts） | Streamable HTTP `/mcp` + 旧版 SSE；`.dp64`/`.dp32` |
| [bromoket/x64dbg_mcp](https://github.com/bromoket/x64dbg_mcp) | 124| 2026-06-08| C++ 插件 REST（约 153 端点）+ npm stdio MCP | 默认 `127.0.0.1:27042`；`npx -y x64dbg-mcp-server` |
| [john-mayhem/x32dbgMCP](https://github.com/john-mayhem/x32dbgMCP) | 11| 2025-11-09| 偏 x32dbg 的 MCP（48+ tools） | 架构类似：Python MCP ↔ 插件 HTTP |
| [ouonet/x64dbg-mcp](https://github.com/ouonet/x64dbg-mcp) | 5| 2026-05-30| Node MCP：stdio / Streamable HTTP，可自动拉起调试器 | 按 PE 架构选 x32/x64；`npm i -g x64dbg-mcp` |

---

## MCP · IDA

> 主工具：[IDA Pro](#ida-pro)

| 项目 | ★ | 更新 | 说明 | 备注 |
|------|--:|------|------|------|
| [jtsylve/re-mcp](https://github.com/jtsylve/re-mcp) (`re-mcp-ida`) | 159| 2026-09-18| 无头多后端 MCP；IDA/Ghidra 共用工具面 | 原 `ida-mcp`；IDA Pro 9+ / idalib |
| [HexRaysSA/ida-mcp](https://github.com/HexRaysSA/ida-mcp) | 26| 2026-09-20| Hex-Rays 官方实验性 IDA MCP | IDA 9.4+；建议关掉其它 IDA MCP |
| [AriusII/ida-pro-mcp](https://github.com/AriusII/ida-pro-mcp) | 0| 2026-06-25| 静态分析 + 可选 live debugger（`?ext=dbg`） | 工具分 READ/WRITE/EXECUTE 安全级别 |

---

## MCP · Ghidra

> 主工具：[Ghidra](#ghidra)

| 项目 | ★ | 更新 | 说明 | 备注 |
|------|--:|------|------|------|
| [LaurieWired/GhidraMCP](https://github.com/LaurieWired/GhidraMCP) | 10,135| 2025-06-23| 社区热门 Ghidra MCP（插件 + HTTP） | 交互式 GUI 工作流常用 |
| [bethington/ghidra-mcp](https://github.com/bethington/ghidra-mcp) | 3,932| 2026-09-19| 大规模工具集（约 110 tools） | LaurieWired 生态相关扩展 |
| [jtsylve/re-mcp](https://github.com/jtsylve/re-mcp) (`re-mcp-ghidra`) | 159| 2026-09-18| Ghidra 无头后端（pyghidra）；PyPI: `re-mcp-ghidra` | Ghidra 12+、JDK 21+ |
| [themixednuts/GhidraMCP](https://github.com/themixednuts/GhidraMCP) | 81| 2026-06-12| 分析 + Trace RMI 调试相关能力 | 需较新 Ghidra（文档写 12.1） |
| [wooyunsec/ghidra-headless-mcp](https://github.com/wooyunsec/ghidra-headless-mcp) | 0| 2026-07-25| 无头 Ghidra MCP（大量工具组） | 适合 Agent / CI |

---

## MCP · Binary Ninja

> 主工具：[Binary Ninja](#binary-ninja)

| 项目 | ★ | 更新 | 说明 | 备注 |
|------|--:|------|------|------|
| [fosdickio/binary_ninja_mcp](https://github.com/fosdickio/binary_ninja_mcp) | 438| 2026-04-05| BN 插件 + MCP bridge | Cursor / Claude / Cline 等可自动配置 |
| [mrphrazer/binary-ninja-headless-mcp](https://github.com/mrphrazer/binary-ninja-headless-mcp) | 244| 2026-09-19| 无头 BN MCP（约 180+ tools） | Agent 深度分析 |
| [symgraph/BinAssistMCP](https://github.com/symgraph/BinAssistMCP) | 50| 2026-09-20| BN 插件 MCP（SSE / Streamable HTTP） | 原 `jtang613/BinAssistMCP`；多 binary 会话 |

---

## MCP · radare2 / 多后端

> 主工具：[radare2](#radare2--rizin)

| 项目 | ★ | 更新 | 说明 | 备注 |
|------|--:|------|------|------|
| [radareorg/radare2-mcp](https://github.com/radareorg/radare2-mcp) | 308| 2026-09-16| 官方 radare2 MCP | `r2pm` 安装；stdio / HTTP |
| [jtsylve/re-mcp](https://github.com/jtsylve/re-mcp) | 159| 2026-09-18| IDA + Ghidra 统一接口 | 后续后端可扩展 |

---

## MCP · WinDbg

> 主工具：[WinDbg / DbgEng](#windbg--dbgeng)

| 项目 | ★ | 更新 | 说明 | 备注 |
|------|--:|------|------|------|
| [hzmslx/windbg-mcp](https://github.com/hzmslx/windbg-mcp) | 0| 2026-05-19| DbgEng + 可选 Frida / dbgsrv / TTD / VM 控制 | 用户态 + 内核；约 29 tools |

---

## MCP · Frida

> 主工具：[Frida](#frida)

| 项目 | ★ | 更新 | 说明 | 备注 |
|------|--:|------|------|------|
| [majimboo/rexd-frida-mcp](https://github.com/majimboo/rexd-frida-mcp) | 1| 2026-04-05| Frida 动态插桩 MCP（attach/hook/读写内存） | stdio；偏 Windows 研究向工作流 |

---

## MCP · angr

> 主工具：[angr](#angr)

| 项目 | ★ | 更新 | 说明 | 备注 |
|------|--:|------|------|------|
| [sandbornm/angr_mcp](https://github.com/sandbornm/angr_mcp) | 5| 2026-06-23| angr-management 插件内嵌 MCP | CFG / 符号执行 / 与 GUI 同步 |

---

## 相关工具与框架

| 项目 | ★ | 更新 | 说明 |
|------|--:|------|------|
| [x64dbg/x64dbg](https://github.com/x64dbg/x64dbg) | 49,566| 2026-09-19| x64dbg / x32dbg 本体 |
| [vector35/warp](https://github.com/vector35/warp) | 67| 2025-11-05| Binary Ninja WARP（函数匹配 / 迁移） |
| [MCP](https://modelcontextprotocol.io/) | — | — | Model Context Protocol 规范 |

---

## 收录规范

提交 PR 时请尽量提供：

1. **链接**（GitHub / PyPI / 官方文档）
2. **宿主工具**（x64dbg / IDA / Ghidra / BN / r2 / WinDbg / Frida / angr…）
3. **传输方式**（stdio / HTTP / SSE）与大致能力
4. **维护状态**（stars / 最近推送，若已知）
5. **许可与依赖**（是否需要商业 License）

优先收录：活跃维护、文档清晰、可被 Cursor / Claude Code / 其它 MCP Client 直接接入的项目。

### 建议条目格式

```md
| [org/name](https://github.com/org/name) | ★N | YYYY-MM-DD | 一句话说明 | 关键备注 |
```

---

## 免责声明

本仓库仅作**工具与项目索引**。请遵守当地法律与软件许可；仅在你有权分析的样本 / 二进制上使用。

---

## License

清单内容采用 [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/)（条目描述可自由复用；所列第三方项目保留各自许可证）。
