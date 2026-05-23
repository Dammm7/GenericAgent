# GenericAgent 启动指南

## 环境说明

- 项目目录：`d:\Apps\GenericAgent\GenericAgent`
- 虚拟环境：`.venv\`（已构建完成）
- 配置文件：`mykey.py`（API Key 已配置）

---

## 启动命令

### 1. 桌面 GUI（推荐）

```powershell
cd d:\Apps\GenericAgent\GenericAgent
.venv\Scripts\python.exe launch.pyw
```

### 2. 终端 UI (TUI)

```powershell
cd d:\Apps\GenericAgent\GenericAgent
.venv\Scripts\python.exe frontends/tuiapp_v2.py
```

### 3. 命令行直接运行

```powershell
cd d:\Apps\GenericAgent\GenericAgent
.venv\Scripts\python.exe agentmain.py
```

### 4. IM Bot 接口（可多选同时启用）

```powershell
cd d:\Apps\GenericAgent\GenericAgent
.venv\Scripts\python.exe launch.pyw --tg --qq --feishu --wechat --dingtalk
```

| 参数 | 平台 |
|------|------|
| `--tg` | Telegram |
| `--qq` | QQ |
| `--feishu` / `--fs` | 飞书 |
| `--wechat` / `--wx` | 微信 |
| `--wecom` | 企业微信 |
| `--dingtalk` / `--dt` | 钉钉 |

### 5. 定时任务调度

```powershell
cd d:\Apps\GenericAgent\GenericAgent
.venv\Scripts\python.exe launch.pyw --sched --llm_no 0
```

---

## 一键启动脚本

如需快速启动，可创建批处理文件 `启动GenericAgent.bat`：

```batch
@echo off
cd /d d:\Apps\GenericAgent\GenericAgent
call .venv\Scripts\activate.bat
python launch.pyw
```

---

## 模型配置说明

当前配置了 3 个模型：

| 索引 | Session 类型 | 模型 | 说明 |
|:---:|:---|:---|:---|
| 0 | MixinSession | minimax-oai | 默认使用，支持故障转移 |
| 1 | LLMSession | siliconflow-qwen3-vl | 文本协议工具 |
| 2 | LLMSession | minimax-oai | 备用 |

### 切换模型

在对话中输入 `/llm 0`、`/llm 1` 或 `/llm 2` 切换模型。

---

## 常见问题

### Q: 启动后显示 "MixinSession/minimax-oai"

这是正常的，显示的是当前加载的模型配置。

### Q: 硅基流动模型无法使用工具

已修复：将 `native_oai_config_siliconflow` 改为 `oai_config_siliconflow`，使用文本协议工具。

### Q: 如何查看日志

日志文件位于 `temp/model_responses/` 目录下。