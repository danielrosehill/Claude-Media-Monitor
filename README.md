# Claude News Fetcher - Media Monitoring System

A comprehensive workspace for conducting media monitoring and gathering articles into a well-defined structured data format.

## Purpose

This repository serves two primary use cases:

1. **Media Monitoring**: Track coverage about specific subjects across various publications
2. **Research Data Collection**: Gather and organize source materials for research projects

## Quick Start

### After Cloning This Repository

**IMPORTANT**: If you're using this repository for media monitoring, run the setup command first:

```
/setup-monitoring
```

This interactive command will:
- Gather details about what you're monitoring (person, company, topic, etc.)
- Understand your monitoring objectives and scope
- Identify key topics, publications, and relevance criteria
- Update the repository's CLAUDE.md file with this context

Running this setup ensures Claude understands your monitoring goals and can better assist with article fetching, classification, and analysis throughout your project.

### Basic Usage

Once setup is complete, you can start fetching articles:

**Fetch a single article:**
```
/fetch [URL]
```

**Fetch multiple articles:**
```
/batch [URL1] [URL2] [URL3]
```

**Analyze your collection:**
```
/analyze
```

## Features

### Article Organization

- **Date-based structure**: Articles organized by year and month (`/articles/YYYY/MM_MonthName/`)
- **Consistent naming**: `article_theme_DDMMYY_publication.md` format
- **Rich metadata**: Publication info, dates, authors, keywords, summaries
- **JSON schema validation**: Ensures data quality and consistency

### Available Commands

| Command | Description |
|---------|-------------|
| `/setup-monitoring` | Configure monitoring context (run this first!) |
| `/fetch` | Fetch and save a single article |
| `/batch` | Process multiple articles at once |
| `/analyze` | Generate statistics and insights about your collection |
| `/search` | Search articles by keyword, publication, or date |
| `/stats` | Show collection statistics |
| `/validate` | Validate articles against schema |
| `/export` | Export articles in various formats (CSV, JSON) |
| `/profile-pub` | Research and profile a publication |

### Specialized Agents

Located in `.claude/agents/`:

- **article-fetcher**: Fetch and save individual articles with metadata
- **batch-fetch**: Process multiple articles efficiently
- **article-analyzer**: Analyze trends and generate reports
- **publication-profiler**: Research publication metadata and bias
- **archive-organizer**: Maintain archive quality and consistency

## Directory Structure

```
/articles/              # All fetched articles (organized by date)
  /YYYY/               # Year folders
    /MM_MonthName/     # Month folders
      article_*.md     # Individual article markdown files
/schemas/              # Data schemas and validation rules
  /fetched-article/
    fetch-schema.json       # JSON schema for article data
    fetch-instructions.md   # Detailed fetching guidelines
/.claude/              # Claude Code configuration
  /agents/             # Specialized subagents
  /commands/           # Slash commands
/exports/              # Exported data (CSV, JSON, etc.)
/reports/              # Generated analysis reports
/publication-profiles/ # Publication metadata and profiles
```

## Article Data Schema

Each article includes:

**Required fields:**
- Title, publication name, URL
- Full text content and word count
- Claude-generated summary
- Classification (coverage/op-ed/by-subject)
- Keywords (5 tags)
- Display summary

**Optional enrichment:**
- Author information (name, title, bio)
- Publication details (summary, editorial leaning)
- Comment analysis (if article has comments)

See `/schemas/fetched-article/fetch-schema.json` for complete schema.

## Workflow Examples

### Single Article Fetch
```
User: "Fetch this article: https://economist.com/example"
Claude: [Fetches, extracts, validates, saves to correct date folder]
```

### Batch Processing
```
User: "Fetch these 10 articles about climate policy"
Claude: [Processes all articles, provides summary report]
```

### Analysis
```
User: "/analyze the last month"
Claude: [Generates statistics, trends, topic breakdown]
```

### Search
```
User: "/search climate policy"
Claude: [Returns matching articles with metadata]
```

## Quality Standards

- **Content Quality**: Clean extraction, proper markdown formatting
- **Metadata Quality**: Accurate dates, authors, classifications
- **Organizational Quality**: Consistent naming and structure
- **Schema Compliance**: All articles validated against JSON schema

## Error Handling

The system gracefully handles:
- Paywall-protected articles
- Invalid URLs
- Missing metadata (uses sensible defaults)
- Publication date ambiguity
- Schema validation issues

## Integration

Works with Daniel's ecosystem:
- **MCP Servers**: Context7, Resend, Time
- **Notion**: Export summaries and reports
- **Obsidian**: Reference in notes
- **Analytics**: Export for visualization

## Best Practices

1. **Run `/setup-monitoring` first** - Establishes monitoring context
2. **Use batch operations** - More efficient for multiple articles
3. **Validate regularly** - Run `/validate` to check data quality
4. **Analyze periodically** - Generate insights with `/analyze`
5. **Profile publications** - Build metadata with `/profile-pub`
6. **Export for backup** - Use `/export` for data preservation

## Technical Details

- **Language**: Markdown for articles, JSON for schemas
- **Validation**: JSON Schema compliance checking
- **Organization**: Date-based hierarchical structure
- **Automation**: Specialized agents for complex workflows
- **Extensibility**: Add custom agents and commands as needed

## Getting Help

- Check `CLAUDE.md` for comprehensive system documentation
- Review `/schemas/fetched-article/fetch-instructions.md` for fetching guidelines
- Use `/stats` to understand your current collection
- Ask Claude for help with any command or workflow

## Version Control

This repository is designed to be version controlled. Commit logical groups of articles with clear messages:

```bash
git add articles/2025/11_Nov/
git commit -m "Add 15 climate policy articles from Nov 2025"
git push
```

---

**Ready to start?** Run `/setup-monitoring` to configure your media monitoring workspace.
