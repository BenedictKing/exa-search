# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-01-22

### Added
- Initial release of Exa Search skill
- Support for 5 core Exa API endpoints:
  - `/search` - Semantic search with neural/fast/deep/auto modes
  - `/contents` - Content extraction from result IDs
  - `/findsimilar` - Find semantically similar pages
  - `/answer` - Direct question answering
  - `/research` - Structured research with custom schemas
- Category filtering (company, people, research paper, news, pdf, github, tweet, etc.)
- Date filtering (published date and crawl date)
- Domain control (include/exclude domains)
- Content options (text, highlights, summary)
- Cost tracking for each API request
- Two-phase architecture (main skill + sub-skill)
- Environment variable and .env file support for API key
- Comprehensive documentation in English and Chinese
