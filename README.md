<<<<<<< HEAD
# multiagent-
=======
# Multi-MCP Multi-Agent Finance Assistant

一个基于 MCP 和 OpenAI Agents SDK 的多智能体金融咨询示例项目。

项目包含两部分：

- `project1_stock_counselor`：单业务方向的股票分析与预测示例，包含多个 MCP Server。
- `project2_Agent_SDK+MCP_materials`：多智能体协同主项目，包含业务分流、金融咨询、股票投顾、文章审查、转人工等角色。

## 项目能力

- 多个 MCP Server 同时接入
- 多智能体按业务语义进行 handoff 协作
- 支持多轮会话和 session 维持
- 提供 FastAPI 接口与 Gradio 演示页面
- 支持股票趋势查询、未来走势预测、金融知识咨询、文章风险审查、转人工服务

## 目录结构

```text
mcp_lecture_project/
├─ project1_stock_counselor/
│  ├─ stock_sever.py
│  ├─ policy_reply_server.py
│  ├─ turn_human_server.py
│  ├─ multi_sse_mcp_client.py
│  └─ series_predict.py
├─ project2_Agent_SDK+MCP_materials/
│  ├─ multi_user_finance_assistant_main_with_session.py
│  ├─ finance_assistant_main.py
│  ├─ finance_consult_mcp_server.py
│  ├─ stock_predict_mcp_server.py
│  ├─ article_check_mcp_server.py
│  ├─ turn_human_server.py
│  ├─ chat_api.py
│  └─ gradio_demo.py
├─ stock_A_daily_close.csv
├─ stock_B_daily_close.csv
├─ stock_C_daily_close.csv
└─ stock_D_daily_close.csv
```

## 技术栈

- Python
- MCP
- OpenAI Agents SDK
- FastAPI
- Gradio
- Pandas / Numpy / Statsmodels
- ChromaDB
- LiteLLM

## 环境依赖

可以参考上层资料目录里的 `requirements(2).txt`，主要依赖包括：

- `openai-agents`
- `mcp`
- `fastapi`
- `uvicorn`
- `gradio`
- `pandas`
- `numpy`
- `statsmodels`
- `chromadb==1.0.8`
- `litellm`
- `dashscope`

建议使用虚拟环境安装：

```powershell
python -m venv .venv
.venv\Scripts\activate
pip install -r ..\requirements(2).txt
```

## 环境变量

项目运行前需要准备 `.env` 配置，常见项包括：

```env
DEEPSEEK_API_KEY=your_key
API_KEY=your_dashscope_key
server_url=your_server_ip_or_domain
```

说明：

- `DEEPSEEK_API_KEY`：多智能体主流程中使用的模型密钥
- `API_KEY`：部分工具逻辑里调用的其他模型服务密钥
- `server_url`：MCP Server 对外暴露的主机地址

## 运行方式

### 1. 启动各 MCP Server

根据需要分别启动对应服务，例如：

```powershell
cd project2_Agent_SDK+MCP_materials
python finance_consult_mcp_server.py
python stock_predict_mcp_server.py
python article_check_mcp_server.py
python turn_human_server.py
```

### 2. 启动多智能体 API

```powershell
cd project2_Agent_SDK+MCP_materials
python chat_api.py
```

默认启动接口：

- `POST /finance_MultiAgent_MultiMCP`

### 3. 启动 Gradio 演示页面

```powershell
cd project2_Agent_SDK+MCP_materials
python gradio_demo.py
```

## 核心设计

### 1. 多 MCP 连接管理

在 `multi_user_finance_assistant_main_with_session.py` 中通过 `MCPManager` 统一维护多个 MCP Server 的连接状态、健康检查和重连逻辑。

### 2. 多智能体协作

通过 `Switch Agent` 作为总分流入口，将请求移交给：

- `Consult Agent`
- `Investment Agent`
- `Article Check Agent`
- `turn_human Agent`

各业务 Agent 之间也建立了双向 handoff，用于跨业务协作。

### 3. Session 管理

通过 `global_sessions` 维护：

- 当前用户消息历史
- 当前业务处理中的 agent
- 多轮对话上下文

## 适用场景

- 金融智能客服
- 投资顾问辅助问答
- 金融资讯审核
- 多工具协同的业务咨询系统
- 多智能体系统教学或 PoC 演示

## 当前说明

这是一个偏教学和原型验证性质的项目，适合用来展示：

- MCP 工具封装思路
- Agents SDK 多智能体协作模式
- 多轮 session 与 handoff 结合方式

如果要进一步用于生产环境，建议继续补充：

- 更严格的异常处理
- 配置文件收敛
- 日志体系
- 单元测试和集成测试
- 更清晰的依赖管理与部署脚本
>>>>>>> 9f4a36a (Add project README)
