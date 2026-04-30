# 软件介绍

AI Agent相关的软件，用于选型。

**核心技术栈：大模型基础 + Funcation Calling + Agent  框架 + 工具集成 + 安全控制（MCP 思想）**



## 一、AI技术演进路线

### 完整路线：GUI → A2A → MCP → CLI

- **GUI（Graphical User Interface）图形界面操作**
  - 技术点
    - 计算机视觉 OCR 识别界面
    - 鼠标 / 键盘自动化
    - 屏幕理解（UI Element Detection）
    - 任务拆解 + 步骤执行
- **A2A（Agent to Agent）智能代理之间通信**
  - 技术点
    - 多智能体协作（Multi-Agent）
    - 标准化通信协议（Agent Protocol）
    - 任务分工、调度、依赖管理
    - 工具共享、能力互通
- **MCP（Model Context Protocol / Model Control Protocol）**
  - MCP = AI 与软件 / 工具安全通信的官方协议，由 Anthropic（Claude）、OpenAI、Google 共同推出
  - 技术点
    - 安全沙箱
    - 最小权限原则
    - 标准化工具调用
    - 上下文实时同步
    - 跨平台统一接口
  - 代表产品
    - Claude 3.7 / Claude Code
    - VS Code + MCP 插件
    - Cursor AI Editor
    - 所有支持 MCP 的 AI 编辑器
  - 定义了三件事
    - AI 能看什么（上下文 content）
    - AI 能做什么（能力/工具skill）
    - AI 能改什么（权限范围）
    - 并且是跨软件、跨模型、跨设备统一
- **CLI（Command Line Interface）命令行 AI**
  - AI 直接操作终端、写命令、执行脚本、管理系统。最轻量化、最高效、最强大的侵入方式。极快、高效、适合开发 / 运维。
  - 技术点
    - Shell 命令生成
    - 环境感知
    - 权限安全控制
    - 自动化脚本执行
    - 日志 / 错误自动修复
  - 代表产品
    - Claude CLI
    - GitHub Copilot CLI
    - AWS CodeWhisperer CLI
    - iTerm2 + AI
    - 终端内置 AI 助手

### AI Agent核心技术总结

- **AI Agent 核心能力**
  - 环境感知（看屏幕 / 读文件 / 读终端）
  - 任务规划（拆步骤）
  - 工具调用（操作软件）
  - 执行验证（检查结果）
  - 异常处理（报错重试）
- **技术栈**
  - 多模态（视觉+文本）
  - 函数调用（Funcation Calling)
  - 自动化控制
  - 协议标准化（MCP）
  - 安全沙箱





## 二、Dify

Dify是一个开源的大语言模型（LLM）应用开发平台，旨在简化和加速生成式AI应用的创建和部署，为开发者提供了一个用户友好的界面和一系列强大的工具，使他们能够快速搭建生产级的AI应用。

应用场景：

聊天助手：基于LLM的对话交互（客服机器人、产品售前机器人）

文本生成：自动化创作、翻译（影视）

Agent：任务分解+工具调用（如论文查询、数据分析、爬虫）

工作流：多节点流程编排（条件分支、API调用）







## 三、MCP

Model Context Protocol / Model Control Protocol



### MCP核心技术点

##### 1. 最小权限原则（最关键）

AI 不能随便删文件、改系统、执行高危命令

MCP 天然带**沙箱 + 权限白名单**

##### 2. 标准化工具暴露

任何软件只要实现 MCP，AI 都能直接用，不需要每个模型单独适配

##### 3. 上下文同步（Context）

AI 知道”当前目录、打开的文件、依赖版本、运行状态、历史命令、报错日志“

##### 4. 安全审计与可解释

AI 每一步操作都会”记录日志、可回放、可中断、可人工确定“，这是企业能接受AI 进入生产环境的前提。



### MCP代表产品与生态

1. **Claude 3.7 / Claude Code（最强落地）**

   - 直接操作 VS Code
   - 直接操作终端
   - 直接读写项目
   - 完整权限控制

2. **Cursor / Windsurf / Zed**

   新一代 AI 编辑器全部基于 MCP 思想重构

3. **VS Code + AI Extension**

   微软正在内置 MCP 协议

4. **GitHub Copilot Workspace**

   完全遵循 MCP 风格的权限与上下文设计





## 四、全栈技术栈地图 + 选型指南

- 所有软件、网站、APP、小程序、AI 系统，本质都是这 4 层
  - 前端（用户看得见、摸得着）
  - 后端（业务逻辑、接口、计算）
  - 数据库（存数据）
  - 运维 / 部署（让项目上线运行）

### 4.1 数据库 & 驱动 / 协议

- 关系型数据库SQL
  - **MySQL：最常用、企业首选、稳定、适合存业务数据**
  - PostgreSQL
  - Oracle
  - SQL Server
- 非关系型数据库NoSQL
  - **Redis：缓存、高速读写、会话、排行榜、限流**
  - MongoDB：存文档、JSON、爬虫数据
  - Elasticsearch：搜索、日志



### 4.2 前端技术栈

- **基础三件套**
  - **HTML**：结构
  - **CSS**：样式
  - **JavaScript**：交互、逻辑
- **现代化前端框架**
  - Vue
    - 简单、易上手
    - 国内中小公司、后台管理系统、小程序、小项目首选
  - React
    - 国外主流、大厂多
    - 复杂 APP、大型项目
    - 难度比 Vue 高
  - 小程序原生
    - 微信小程序、支付宝小程序
    - 直接对接 Flask/FastAPI 后端



### 4.3 后端Web框架

- **Flask**
  - 定位：轻量、小巧、自由
  - 适合：**小项目、学习、API、练手**
  - 优点：简单、灵活、自由
  - 缺点：功能少，很多东西要自己写
- **Django**
  - 定位：大而全、一站式、重型框架
  - 适合：**大型网站、后台管理、CMS、电商**
  - 优点：自带后台、ORM、认证、admin、安全
  - 缺点：重、学习曲线比 Flask 陡
  - 企业中后台系统非常常用
- **FastAPI**
  - 定位：现代、高性能、API 专用
  - 适合：**微服务、API 接口、AI 后端、高并发**
  - 优点：极快、自动生成文档、支持异步
  - 现在最火、AI Agent 首选后端框架



### 4.4 运维 / 部署

- 服务器系统
  - Linux（CentOS / Ubuntu）
- 容器化
  - **Docker**：打包环境，一次打包到处运行
  - **Docker Compose**：一键启动整套项目
- Web 服务器
  - Nginx：接收用户请求、反向代理、负载均衡
  - Gunicorn /uWSGI：Python Web 服务运行

