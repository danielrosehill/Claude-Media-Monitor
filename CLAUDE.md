# Claude News Fetcher - Media Monitoring System

## Repository Purpose

This repository is a workspace template for conducting media monitoring and gathering articles into a well-defined structured data format. It serves two primary use cases:

1. **Media Monitoring**: Track coverage about specific subjects across various publications
2. **Research Data Collection**: Gather and organize source materials for research projects

## Directory Structure

```
/articles/              # All fetched articles organized by date
  /YYYY/               # Year folders (2000-2025+)
    /MM_MonthName/     # Month folders (01_Jan through 12_Dec)
      article_*.md     # Individual article files
/schemas/              # Data schemas and validation rules
  /fetched-article/    # Article schema and instructions
    fetch-schema.json       # JSON schema for article data
    fetch-instructions.md   # Detailed fetching guidelines
/.claude/              # Claude Code configuration
  /agents/             # Specialized subagents
  /commands/           # Slash commands for quick operations
```

## Article Organization System

### Storage Structure

**All articles MUST be saved in the `/articles/` directory following this hierarchy:**

1. **Year folder**: `/articles/YYYY/` (e.g., `/articles/2025/`)
2. **Month folder**: `/articles/YYYY/MM_MonthName/` (e.g., `/articles/2025/11_Nov/`)
3. **Article file**: Individual markdown files with structured naming

### File Naming Convention

**Format**: `article_theme_DDMMYY_publication.md`

**Components**:
- `article_` - Static prefix for all files
- `theme` - 2-4 keyword description of the article topic (lowercase, underscores between words)
- `DDMMYY` - Publication date (day, month, year in 2 digits each)
- `publication` - Abbreviated publication name (lowercase, simplified)

**Examples**:
- `article_climate_policy_debate_171025_economist.md`
- `article_ai_regulation_europe_030325_ft.md`
- `article_tech_industry_layoffs_280624_nytimes.md`

### Content Structure

Each article file must include:

1. **Metadata Header** (YAML front matter or markdown section):
   - Article title
   - Publication name
   - Publication date
   - Article URL
   - Date fetched
   - Author(s)
   - Keywords/tags

2. **Article Content**:
   - Clean markdown formatting
   - Preserved structure (headings, paragraphs, lists)
   - No advertisements or navigation elements
   - Proper markdown syntax throughout

## JSON Schema Compliance

All fetched articles must conform to the schema defined in `/schemas/fetched-article/fetch-schema.json`.

**Required fields include**:
- title, pub_name, article_url
- full_text, article_word_count
- claude_summary
- is_coverage, is_oped, by_subject
- has_comments
- keywords (array of 5 tags)
- display_summary

**Optional enrichment fields**:
- Author information (name, title, bio)
- Publication details (summary, editorial leaning)
- Comment analysis (summary, sentiment score, count)

See `/schemas/fetched-article/fetch-instructions.md` for detailed fetching guidelines.

## Workflow Overview

### Standard Article Capture Workflow

1. **Receive URL**: User provides article URL to fetch
2. **Invoke Agent**: Use the `article-fetcher` agent or `/fetch` command
3. **Extraction**: Agent fetches content and extracts metadata
4. **Schema Validation**: Content structured according to JSON schema
5. **Organization**: File saved to appropriate date-based folder
6. **Confirmation**: Location and filename reported back

### Batch Processing Workflow

For multiple articles:
1. User provides list of URLs or search criteria
2. Use `batch-fetch` agent to process multiple articles
3. Each article follows standard workflow
4. Summary report generated at completion

## Available Tools

### Subagents

Located in `.claude/agents/`:

1. **article-fetcher**: Primary agent for fetching and saving individual articles
   - Handles complete fetch-to-save workflow
   - Extracts metadata and formats content
   - Ensures schema compliance
   - Organizes by date

2. **batch-fetch**: Process multiple articles in one operation
   - Accepts list of URLs
   - Processes each article systematically
   - Provides progress updates
   - Generates batch summary report

3. **article-analyzer**: Analyze existing articles in the repository
   - Generate statistics and insights
   - Identify trends across articles
   - Create summary reports
   - Export data in various formats

4. **publication-profiler**: Research and profile publications
   - Gather publication metadata
   - Assess editorial bias/leaning
   - Track publication patterns
   - Maintain publication database

5. **archive-organizer**: Maintain and optimize the article archive
   - Validate file naming consistency
   - Check schema compliance
   - Identify duplicates
   - Generate archive reports

### Slash Commands

Located in `.claude/commands/`:

1. **/fetch**: Quick article fetch - provide URL, get article saved
2. **/batch**: Batch process multiple URLs at once
3. **/analyze**: Analyze the article archive and generate reports
4. **/validate**: Validate existing articles against schema
5. **/stats**: Show statistics about the article collection
6. **/search**: Search articles by keyword, publication, or date
7. **/export**: Export articles in various formats (CSV, JSON, etc.)
8. **/profile-pub**: Profile a publication for metadata enrichment

## Quality Standards

### Content Quality
- Remove all advertisements, navigation, and non-article elements
- Preserve article formatting (bold, italics, lists, quotes)
- Maintain paragraph breaks and section structure
- Include image alt-text descriptions where relevant
- Ensure proper markdown syntax

### Metadata Quality
- Accurate publication identification
- Correct date extraction (or current date if unavailable)
- Descriptive theme keywords (2-4 words)
- Complete author information when available
- Proper classification (coverage/op-ed/by-subject)

### Organizational Quality
- Consistent file naming across all articles
- Proper date-based folder structure
- No orphaned files outside the structure
- Regular validation against schema

## Error Handling

**Common scenarios**:

1. **Paywall articles**: Inform user, suggest alternatives or manual intervention
2. **Invalid URLs**: Report issue clearly, request valid URL
3. **Missing publication name**: Use "unknown" as publication identifier
4. **Missing publication date**: Use current date (fetch date)
5. **Ambiguous theme**: Request 2-4 keywords from user
6. **Schema validation failures**: Report specific issues, fix and retry

## Usage Guidelines

### When Working with Articles

1. **Always use the date-based structure** - Never save articles to repository root
2. **Follow naming conventions exactly** - Consistency is critical for searchability
3. **Validate against schema** - Ensure all required fields are populated
4. **Preserve content quality** - Clean extraction with proper formatting
5. **Document fetch context** - Note date fetched, any issues encountered

### When Adding Features

1. **Respect existing structure** - Don't reorganize the archive without explicit approval
2. **Maintain schema compatibility** - Changes should be backward compatible
3. **Update documentation** - Keep this CLAUDE.md synchronized with functionality
4. **Test thoroughly** - Validate with sample articles before batch processing

### Performance Optimization

1. **Batch operations** - Use batch agent for multiple articles
2. **Parallel processing** - Process independent articles concurrently where possible
3. **Cache publication metadata** - Avoid redundant lookups
4. **Index for search** - Maintain search indices for large collections

## Integration Points

### With MCP Servers

This repository can integrate with:
- **Context7**: For API documentation when building analysis tools
- **Resend**: For email notifications about new articles or reports
- **Time**: For accurate date/time stamping

### With External Tools

- **Notion**: Export summaries and reports to Notion workspace
- **Obsidian**: Can reference articles in Daniel's reference notes
- **Analytics platforms**: Export data for visualization and analysis

## Monitoring Subject Context

If this repository is used for media monitoring about a specific subject:

1. Check this CLAUDE.md for subject identification
2. Subject context informs the `by_subject` field in article schema
3. Adjust analysis and tagging based on subject relevance
4. Track sentiment and coverage patterns related to subject

**Current Subject**: [Define subject here if applicable, e.g., "Daniel Rosehill", "DSR Holdings", or "general research collection"]

## Maintenance Tasks

### Regular Maintenance
- Validate file naming consistency across archive
- Check for schema compliance issues
- Remove duplicate articles
- Update publication profiles
- Generate periodic statistics reports

### Data Quality Audits
- Review article summaries for accuracy
- Validate keyword relevance
- Check metadata completeness
- Assess classification accuracy (coverage/op-ed/by-subject)

## Best Practices

1. **Be Systematic**: Follow the established structure and workflows
2. **Validate Early**: Check schema compliance during fetch, not after
3. **Document Thoroughly**: Complete all metadata fields comprehensively
4. **Stay Organized**: Use date-based structure consistently
5. **Quality Over Quantity**: Ensure clean, accurate extractions
6. **Automate When Possible**: Use batch operations and automation tools
7. **Version Control**: Commit logical groups of articles with clear messages

## Getting Started

**To fetch your first article**:
```
User: "Fetch this article: [URL]"
Claude: [Invokes article-fetcher agent, processes, saves to correct location]
```

**To fetch multiple articles**:
```
User: "Fetch these articles: [URL1], [URL2], [URL3]"
Claude: [Invokes batch-fetch agent, processes all, provides summary]
```

**To analyze your collection**:
```
User: "/analyze"
Claude: [Generates statistics and insights report]
```

---

This system is designed to make media monitoring and research data collection systematic, searchable, and maintainable over time. Follow these guidelines consistently to build a valuable article archive.
