# Exa Search Skill

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

English | [简体中文](./README_CN.md)

Semantic search skill for Claude Code using [Exa API](https://exa.ai). Provides embeddings-based intelligent search, similar content discovery, and structured research capabilities.

## Features

- 🔍 **Semantic Search**: Neural, fast, deep, and auto search modes
- 📄 **Content Extraction**: Get clean, parsed HTML content from search results
- 🔗 **Find Similar**: Discover semantically similar pages based on a URL
- 💬 **Direct Answers**: Get immediate answers to questions
- 📊 **Structured Research**: Automated research with custom output schemas
- 🎯 **Category Filtering**: Search by company, people, research papers, news, PDFs, GitHub, tweets, etc.
- 💰 **Cost Tracking**: Detailed cost breakdown for each request

## Installation

### Option 1: Install via skills CLI (Recommended)

```bash
# Install globally to all detected agents (Claude Code, Cursor, Codex, etc.)
npx skills add -g BenedictKing/exa-search

# Or install to current project only
npx skills add BenedictKing/exa-search
```

The skill will be automatically installed and loaded by Claude Code.

### Option 2: Manual Installation via Git Clone

1. Clone this repository to your Claude skills directory:
```bash
cd ~/.claude/skills
git clone https://github.com/BenedictKing/exa-search.git
```

2. Configure your API key:
```bash
cd exa-search/.claude/skills/exa-search
cp .env.example .env
# Edit .env and add your Exa API key
```

## Configuration

Get your API key from [Exa Dashboard](https://dashboard.exa.ai/).

Two ways to configure:

1. **Environment Variable** (recommended):
```bash
export EXA_API_KEY=your_api_key_here
```

2. **`.env` file**:
```bash
# In .claude/skills/exa-search/.env
EXA_API_KEY=your_api_key_here
```

## Usage

### Trigger the Skill

Use `/exa-search` or let Claude automatically invoke it when you need:
- Semantic web search
- Finding similar content
- Direct answers to questions
- Structured research

### Example Queries

**Semantic Search:**
```
Find latest research papers on transformer architectures
```

**Find Similar:**
```
Find pages similar to https://arxiv.org/abs/1706.03762
```

**Direct Answer:**
```
What are the key differences between GPT-4 and Claude?
```

**Structured Research:**
```
Research the top AI companies and their key metrics
```

## API Endpoints

### 1. Search
Embeddings-based semantic search with multiple modes:
- `neural`: Semantic search using embeddings
- `fast`: Quick keyword-based search
- `auto`: Automatically choose best method (default)
- `deep`: Comprehensive deep search

### 2. Contents
Extract full content from search result IDs.

### 3. Find Similar
Discover semantically similar pages based on a given URL.

### 4. Answer
Get direct answers to questions with source citations.

### 5. Research
Automated deep research with custom output schemas.

## Advanced Features

### Category Filtering
Search within specific content types:
- `company`, `people`, `research paper`, `news`, `pdf`, `github`, `tweet`, etc.

### Date Filtering
Filter by publication date or crawl date:
```json
{
  "startPublishedDate": "2025-01-01",
  "endPublishedDate": "2025-12-31"
}
```

### Domain Control
Include or exclude specific domains:
```json
{
  "includeDomains": ["arxiv.org", "github.com"],
  "excludeDomains": ["example.com"]
}
```

### Content Options
Control what content to retrieve:
```json
{
  "contents": {
    "text": true,
    "highlights": true,
    "summary": true
  }
}
```

## Pricing

Exa API pricing (as of 2026):
- Neural Search (1-25 results): $0.005
- Neural Search (26-100 results): $0.025
- Deep Search (1-25 results): $0.015
- Deep Search (26-100 results): $0.075
- Content text/highlights/summary: $0.001 per page

Each API response includes a `costDollars` field with detailed cost breakdown.

## Architecture

This skill uses a two-phase architecture:
1. **Main skill**: Understands user intent, chooses endpoint, assembles payload
2. **Sub-skill (exa-fetcher)**: Executes HTTP calls in isolated context

This design minimizes token usage and keeps conversation history clean.

## Comparison with Tavily

| Feature | [Exa](https://exa.ai) | [Tavily](https://tavily.com) |
|---------|-----|--------|
| Search Type | Embeddings-based semantic | Keyword + AI-enhanced |
| Find Similar | ✅ | ❌ |
| Category Search | ✅ (company, people, papers, etc.) | ❌ |
| Search Modes | neural/fast/deep/auto | basic/advanced |
| Cost Tracking | ✅ Detailed per request | ❌ |
| Crawl/Map | ❌ | ✅ |

**Claude Code Skills:**
- Exa: [BenedictKing/exa-search](https://github.com/BenedictKing/exa-search)
- Tavily: [BenedictKing/tavily-web](https://github.com/BenedictKing/tavily-web)

**Use Exa when:**
- You need semantic/embeddings-based search
- Finding similar content is important
- You want category-specific searches
- Cost tracking is required

**Use Tavily when:**
- You need site crawling/mapping
- You want structured research with citations
- You prefer keyword-based search

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Author

**BenedictKing**
- GitHub: [@BenedictKing](https://github.com/BenedictKing)

## Links

- [Exa API Documentation](https://exa.ai/docs)
- [Exa Dashboard](https://dashboard.exa.ai/)
- [Claude Code](https://github.com/anthropics/claude-code)
