# Exa Search 技能

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

基于 [Exa API](https://exa.ai) 的 Claude Code 语义搜索技能。提供基于嵌入的智能搜索、相似内容发现和结构化研究能力。

## 功能特性

- 🔍 **语义搜索**：神经、快速、深度和自动搜索模式
- 📄 **内容提取**：从搜索结果获取干净的解析 HTML 内容
- 🔗 **相似查找**：基于 URL 发现语义相似的页面
- 💬 **直接问答**：获取问题的即时答案
- 📊 **结构化研究**：使用自定义输出模式的自动化研究
- 🎯 **类别过滤**：按公司、人物、研究论文、新闻、PDF、GitHub、推文等搜索
- 💰 **成本追踪**：每次请求的详细成本明细

## 安装

### 通过 Claude Code 插件管理器

```bash
claude plugin install https://github.com/BenedictKing/exa-search.git
```

### 手动安装

1. 克隆此仓库到 Claude 技能目录：
```bash
cd ~/.claude/skills
git clone https://github.com/BenedictKing/exa-search.git
```

2. 配置 API 密钥：
```bash
cd exa-search/.claude/skills/exa-search
cp .env.example .env
# 编辑 .env 并添加你的 Exa API 密钥
```

## 配置

从 [Exa Dashboard](https://dashboard.exa.ai/) 获取 API 密钥。

两种配置方式：

1. **环境变量**（推荐）：
```bash
export EXA_API_KEY=your_api_key_here
```

2. **`.env` 文件**：
```bash
# 在 .claude/skills/exa-search/.env 中
EXA_API_KEY=your_api_key_here
```

## 使用方法

### 触发技能

使用 `/exa-search` 或让 Claude 在需要时自动调用：
- 语义网页搜索
- 查找相似内容
- 问题直接答案
- 结构化研究

### 示例查询

**语义搜索：**
```
查找关于 transformer 架构的最新研究论文
```

**相似查找：**
```
查找与 https://arxiv.org/abs/1706.03762 相似的页面
```

**直接问答：**
```
GPT-4 和 Claude 的主要区别是什么？
```

**结构化研究：**
```
研究顶级 AI 公司及其关键指标
```

## API 端点

### 1. Search（搜索）
基于嵌入的语义搜索，支持多种模式：
- `neural`：使用嵌入的语义搜索
- `fast`：快速关键词搜索
- `auto`：自动选择最佳方法（默认）
- `deep`：全面深度搜索

### 2. Contents（内容）
从搜索结果 ID 提取完整内容。

### 3. Find Similar（相似查找）
基于给定 URL 发现语义相似的页面。

### 4. Answer（问答）
获取带来源引用的问题直接答案。

### 5. Research（研究）
使用自定义输出模式的自动化深度研究。

## 高级功能

### 类别过滤
在特定内容类型中搜索：
- `company`、`people`、`research paper`、`news`、`pdf`、`github`、`tweet` 等

### 日期过滤
按发布日期或爬取日期过滤：
```json
{
  "startPublishedDate": "2025-01-01",
  "endPublishedDate": "2025-12-31"
}
```

### 域名控制
包含或排除特定域名：
```json
{
  "includeDomains": ["arxiv.org", "github.com"],
  "excludeDomains": ["example.com"]
}
```

### 内容选项
控制要检索的内容：
```json
{
  "contents": {
    "text": true,
    "highlights": true,
    "summary": true
  }
}
```

## 定价

Exa API 定价（截至 2026 年）：
- 神经搜索（1-25 结果）：$0.005
- 神经搜索（26-100 结果）：$0.025
- 深度搜索（1-25 结果）：$0.015
- 深度搜索（26-100 结果）：$0.075
- 内容文本/高亮/摘要：每页 $0.001

每个 API 响应都包含一个 `costDollars` 字段，提供详细的成本明细。

## 架构

此技能使用两阶段架构：
1. **主技能**：理解用户意图，选择端点，组装负载
2. **子技能（exa-fetcher）**：在隔离上下文中执行 HTTP 调用

这种设计最小化了令牌使用，保持对话历史清晰。

## 与 Tavily 的比较

| 功能 | Exa | Tavily |
|------|-----|--------|
| 搜索类型 | 基于嵌入的语义搜索 | 关键词 + AI 增强 |
| 相似查找 | ✅ | ❌ |
| 类别搜索 | ✅（公司、人物、论文等） | ❌ |
| 搜索模式 | neural/fast/deep/auto | basic/advanced |
| 成本追踪 | ✅ 每次请求详细 | ❌ |
| 爬取/映射 | ❌ | ✅ |

**使用 Exa 当：**
- 需要语义/基于嵌入的搜索
- 查找相似内容很重要
- 需要特定类别搜索
- 需要成本追踪

**使用 Tavily 当：**
- 需要网站爬取/映射
- 需要带引用的结构化研究
- 偏好关键词搜索

## 贡献

欢迎贡献！请随时提交 Pull Request。

## 许可证

MIT 许可证 - 详见 [LICENSE](LICENSE) 文件。

## 作者

**BenedictKing**
- GitHub: [@BenedictKing](https://github.com/BenedictKing)

## 链接

- [Exa API 文档](https://exa.ai/docs)
- [Exa Dashboard](https://dashboard.exa.ai/)
- [Claude Code](https://github.com/anthropics/claude-code)
