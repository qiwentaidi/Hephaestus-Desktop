<div align="center">
<a href="https://github.com/qiwentaidi/Hephaestus-Desktop"><img src="assets/appicon.png" width="120"/></a>
</div>
<h1 align="center">Hephaestus Desktop</h1>

<div align="center">
  <a href="README.md">中文</a> •
  <a href="README_EN.md">English</a>
</div>
<br />

Hephaestus Desktop 是 [Hephaestus](https://github.com/qiwentaidi/Hephaestus) 的桌面客户端，集成攻击面评估、AI 渗透对话、资产与漏洞管理，以及本地工具启动器等能力。内置本地服务，默认使用 SQLite，适合单机安全测试和本地工具整合。

本项目由原 [Slack](https://github.com/qiwentaidi/Slack) v3 版本演进而来。本仓库提供桌面客户端介绍与发布下载。

- 桌面客户端下载：[Releases](https://github.com/qiwentaidi/Hephaestus-Desktop/releases)
- Web 服务与平台介绍：[Hephaestus](https://github.com/qiwentaidi/Hephaestus)
- 扫描节点与命令行工具：[Hephaestus-Agent](https://github.com/qiwentaidi/Hephaestus-Agent)
- 许可证注册：[官网](http://47.97.59.120)

## 核心亮点

- **本地运行**：内置服务与 SQLite 数据库，单机使用无需另外部署 Web 服务或 PostgreSQL。
- **组合扫描**：按需组合网站、端口、目录、子域名及 JS/API 扫描，在同一任务中查看进度与结果。
- **AI 渗透对话**：围绕授权目标调用工具开展测试，支持记录发现、复现步骤与证据，方便后续复核。
- **远程执行**：可连接共享 PostgreSQL，使用远程 Agent 执行扫描，在平台中集中查看任务与结果。

## 主要功能

| 模块 | 功能 |
| --- | --- |
| 攻击面评估 | 网站指纹与漏洞、端口与服务、弱口令、目录、子域名及 JS/API 扫描 |
| 任务管理 | 并发控制、暂停与恢复、取消、扫描历史、计划任务与参数模板 |
| AI 工作台 | 项目与会话、工具调用、图片输入、测试过程记录与证据查看；支持批量任务 |
| 资产与漏洞 | 资产中心、拓扑与地图，查看扫描与 AI 发现，跟踪人工处置状态 |
| 报告管理 | 集中查看扫描报告，支持导出与合并导出 |
| 请求与 PoC | HTTP 请求编辑与响应查看，Nuclei 模板检索、编辑、润色与调试 |
| 信息收集 | FOFA、Hunter、Quake 查询及聚合搜索，企业与关联资产收集 |
| 分析与凭据 | 编解码、JWT、API 文档测试、文本比较、数据库连接与密钥管理 |

完整平台功能与 Web 部署说明见 [Hephaestus 仓库](https://github.com/qiwentaidi/Hephaestus)。

## 桌面专属功能

- **本地启动器**：集中管理本地工具及 JDK 配置，启动工具、打开所在目录或终端。
- **独立设置窗口**：通过顶部齿轮单独打开设置，配置扫描参数、AI、外观和语言。
- **小程序反编译**：提供桌面端的小程序反编译入口。
- **系统集成**：下载文件时使用系统保存对话框，外部链接通过系统默认浏览器打开。

## 快速开始

### 1. 下载并安装

从 [Releases](https://github.com/qiwentaidi/Hephaestus-Desktop/releases) 下载与操作系统和 CPU 架构匹配的安装包，安装后打开客户端。

客户端会自动启动内置服务。默认 SQLite 单机模式无需准备外部数据库。

### 2. 完成激活与账户初始化

1. 在 [官网](http://47.97.59.120) 注册并获取许可证 Key，按客户端页面提示完成在线激活；内网环境可按页面提示导入离线许可证。
2. 激活后，首次使用会进入管理员账户创建页面；已初始化的实例直接登录。

### 3. 准备扫描资源与 AI 配置

登录后，根据需要完成以下配置：

- **扫描资源**：进入「系统设置 → 系统更新」，通过「配置文件更新」下载或更新 PoC、目录字典和弱口令字典等资源。
- **空间引擎**：使用 FOFA、Hunter、Quake 等服务前，在「系统设置 → API密钥」填写对应 Key。
- **AI 工作台**：在「系统设置 → AI 配置」填写渠道、API 地址、Key 和模型，并测试连接。
- **本地工具**：打开启动器，配置工具路径及需要使用的 JDK。

完成所需配置后，即可创建扫描任务，或在 AI 工作台中新建会话并说明授权目标与测试范围。

## 配置与数据

下列路径中的 `~` 表示当前运行用户的家目录。

| 项目 | 默认值或说明 |
| --- | --- |
| 配置文件 | `~/.config/hephaestus/config-desktop.yaml` |
| 本地数据库 | `~/.config/hephaestus/data/hephaestus.db`（SQLite） |
| 内置服务 | `127.0.0.1:38456`；端口被占用时使用临时端口 |
| 首选服务端口 | 通过 `HEPHAESTUS_DESKTOP_BACKEND_PORT` 指定 |
| 配置基础目录 | 通过 `HEPHAESTUS_CONFIG_DIR` 指定 |

桌面端和 Web 服务使用不同的配置文件，但默认配置基础目录相同。需要分别保存配置和本地数据时，可为两端设置不同的 `HEPHAESTUS_CONFIG_DIR`。

如需与 Web 服务或远程 Agent 共用平台数据，将桌面端配置为连接同一个 PostgreSQL。连接配置示例见 [Web 部署说明](https://github.com/qiwentaidi/Hephaestus)。切换数据库类型不会自动迁移已有记录。

## 常见问题

### 桌面端与 Web 端可以共享数据吗？

可以将两端配置为连接同一个 PostgreSQL，以共用数据库中的平台记录。两端仍使用各自的配置文件；共用数据库不会自动同步本地工具路径和会话工作目录中的文件。

### 扫描资源不可用或空间引擎查询失败怎么办？

检查「系统设置 → 系统更新」中的配置资源是否已下载，并确认所用模块的 PoC 或字典可用。空间引擎还需要有效的 API Key 和足够的查询额度。

### 内置服务端口被占用怎么办？

客户端会尝试使用临时端口继续启动。如需指定首选端口，在启动客户端前设置 `HEPHAESTUS_DESKTOP_BACKEND_PORT`。

## 联系方式

添加联系时请备注来意。

<img src="assets/image-20231006124944803.png" alt="联系信息" width="100" />
