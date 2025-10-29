# A股市场智能分析系统

通过AI自动分析A股市场并通过机器人推送消息。

## 🌟 功能特性

- **实时市场数据**：获取上证指数、深证成指、创业板指数最新行情
- **市场情绪分析**：统计涨停股票数量，评估市场活跃度
- **热门板块识别**：自动识别当前最热门的5个板块
- **智能投资建议**：基于多维度数据生成投资建议
- **机器人推送**：自动推送分析报告到机器人

## 🏗️ 技术架构

本项目基于 MCP (Model Context Protocol) 服务器架构：

- **mcp-aktools**：AKShare数据接口，提供A股市场数据
- **mcp-notify**：飞书通知服务，支持消息推送

## 📋 前置要求

1. Python 3.8+
2. Claude Code CLI
3. 已配置的 MCP 服务器（见 `.mcp.json`）

## 🚀 快速开始

### 1. 安装依赖

```bash
uv sync
```

### 2. 配置 MCP 服务器

确保 `.mcp.json` 文件已正确配置：

```json
{
  "mcpServers": {
    "mcp-aktools": {
      "command": "uvx",
      "args": ["mcp-aktools"],
      "env": {
        "OKX_BASE_URL": "${OKX_BASE_URL}",
        "BINANCE_BASE_URL": "${BINANCE_BASE_URL}"
      }
    },
    "mcp-notify": {
      "command": "uvx",
      "args": ["mcp-notify"],
      "env": {
        "WEWORK_BOT_KEY": "${WEWORK_BOT_KEY}",
        "WEWORK_APP_CORPID": "${WEWORK_APP_CORPID}",
        "WEWORK_APP_SECRET": "${WEWORK_APP_SECRET}",
        "WEWORK_APP_AGENTID": "${WEWORK_APP_AGENTID}",
        "WEWORK_APP_TOUSER": "${WEWORK_APP_TOUSER}",
        "WEWORK_BASE_URL": "${WEWORK_BASE_URL}",
        "DING_BOT_KEY": "${DING_BOT_KEY}",
        "DINGTALK_BOT_KEY": "${DINGTALK_BOT_KEY}",
        "DINGTALK_BASE_URL": "${DINGTALK_BASE_URL}",
        "FEISHU_BOT_KEY": "${FEISHU_BOT_KEY}",
        "FEISHU_BASE_URL": "${FEISHU_BASE_URL}",
        "LARK_BOT_KEY": "${LARK_BOT_KEY}",
        "LARK_BASE_URL": "${LARK_BASE_URL}",
        "BARK_DEVICE_KEY": "${BARK_DEVICE_KEY}",
        "BARK_BASE_URL": "${BARK_BASE_URL}",
        "TELEGRAM_BOT_TOKEN": "${TELEGRAM_BOT_TOKEN}",
        "TELEGRAM_DEFAULT_CHAT": "${TELEGRAM_DEFAULT_CHAT}",
        "TELEGRAM_BASE_URL": "${TELEGRAM_BASE_URL}"
      }
    }
  }
}
```

### 3. 运行分析

```bash
curl -fsSL https://claude.ai/install.sh | bash
uv run analyze_market.py
```

或使用 Claude CLI 直接运行：

```bash
claude -p '分析A股市场总结投资建议推送到飞书机器人'
```

## 📊 分析报告示例

```
📊 A股市场分析报告
⏰ 时间：2025-10-29 14:30:00

一、市场概况
• 上证指数：3,245.67 (+1.23%)
• 深证成指：10,234.56 (+1.45%)
• 创业板指：2,123.45 (+1.67%)

二、市场情绪
• 涨停家数：65家
• 市场活跃度：活跃

三、热门板块TOP5
1. 人工智能 +3.45%
2. 半导体 +2.89%
3. 新能源 +2.34%
4. 医药生物 +1.98%
5. 5G通信 +1.67%

四、市场分析
今日三大指数集体上涨，市场情绪较为乐观...

五、投资建议
建议：稳健操作，关注人工智能和半导体板块机会
```

## 🔧 配置说明

### 飞书机器人配置

1. 在飞书群聊中添加自定义机器人
2. 获取 Webhook 密钥
3. 更新 `.mcp.json` 中的 `FEISHU_BOT_KEY`

### 市场数据源

- 默认使用 AKShare 接口
- 可通过配置环境变量使用代理：
  - `OKX_BASE_URL`：OKX交易所代理地址
  - `BINANCE_BASE_URL`：币安交易所代理地址

## 📝 自定义分析

您可以修改 `analyze_market.py` 中的分析逻辑来满足特定需求：

- 调整分析维度
- 修改推送格式
- 添加更多技术指标
- 设置定时任务

## ⏰ 定时任务

使用 cron 设置定时分析（每个交易日15:30）：

```bash
30 15 * * 1-5 cd /path/to/ak-auto && python analyze_market.py
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

MIT License

## 🙏 致谢

- [AKShare](https://github.com/akfamily/akshare) - 提供A股数据接口
- [Claude Code](https://claude.ai/code) - AI驱动的代码助手
- [MCP AKTools](https://github.com/aahl/mcp-aktools) - 提供A股数据接口
- [MCP Notify](https://github.com/aahl/mcp-notify) - 提供消息推送服务
- [MCP](https://modelcontextprotocol.io/) - Model Context Protocol

---

💡 **提示**：本系统仅供学习和参考，投资有风险，决策需谨慎！
