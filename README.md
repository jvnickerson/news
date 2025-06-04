# News Feed MCP Server
A Model Context Protocol (MCP) server that enables Claude to query current news from multiple RSS feed sources. This server provides real-time access to news articles from BBC, Reuters, NPR, Associated Press, and Google News without requiring any API keys.
## Features
- 🆓 **Completely Free** - Uses RSS feeds, no API keys required
- 📰 **Multiple News Sources** - BBC, Reuters, NPR, AP, Google News
- 🔍 **Keyword Search** - Filter news by topics of interest
- 🔄 **Real-time Updates** - Fetches current news articles on demand
- 🛡️ **Robust Error Handling** - Graceful handling of network issues
- 📊 **Cross-source Search** - Search across all news sources simultaneously
## Quick Start
### 1. Installation
```bash
# Clone or download this project
cd your-project-directory
# Install dependencies
npm install
```
### 2. Test the Server
```bash
node index.js
```
You should see: `📰 News MCP Server running on stdio transport`
### 3. Configure Claude Desktop
Find your Claude configuration file:
- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
Add this configuration (replace with your actual path):
```json
{
  "mcpServers": {
    "news-feed": {
      "command": "node",
      "args": ["/full/path/to/your/project/index.js"],
      "env": {}
    }
  }
}
```
### 4. Restart Claude Desktop
Close and reopen Claude Desktop completely for the changes to take effect.
## Usage Examples
Once configured, you can ask Claude:
### Basic News Queries
- "What's the latest news today?"
- "Get me the top 10 news stories"
- "What's happening in the world right now?"
### Source-Specific Queries
- "Get the latest news from BBC"
- "Show me Reuters headlines"
- "What's new on NPR?"
### Keyword Searches
- "Search for news about artificial intelligence"
- "Find recent articles about climate change"
- "Look for news about the election"
- "Search all sources for technology news"
### Advanced Queries
- "Search for news about 'space exploration' from multiple sources"
- "Get 5 articles about 'renewable energy' from BBC"
- "What news sources are available?"
## Available Tools
The server provides three tools that Claude can use:
### 1. `get-news`
Fetch latest news from a specific source.
**Parameters:**
- `source` (optional): News source (bbc, reuters, npr, ap, google) - defaults to BBC
- `keywords` (optional): Keywords to search for in articles
- `limit` (optional): Maximum articles to return (1-50, default: 10)
### 2. `search-all-news`
Search for keywords across all news sources.
**Parameters:**
- `keywords` (required): Keywords to search for
- `limit` (optional): Maximum articles per source (1-20, default: 5)
### 3. `list-news-sources`
Display all available news sources and usage tips.
**Parameters:** None
## News Sources
| Source | Description | RSS Feed |
|--------|-------------|----------|
| **BBC** | BBC News - Global coverage | https://feeds.bbci.co.uk/news/rss.xml |
| **Reuters** | Reuters top stories | https://www.reutersagency.com/feed/ |
| **NPR** | NPR News | https://feeds.npr.org/1001/rss.xml |
| **AP** | Associated Press | https://apnews.com/index.rss |
| **Google** | Google News aggregated | https://news.google.com/rss |
## Technical Details
### Architecture
- **Transport**: stdio (most reliable for Claude Desktop)
- **RSS Parsing**: Custom XML parser for cross-feed compatibility
- **Error Handling**: Graceful degradation when feeds are unavailable
- **Rate Limiting**: Built-in limits to prevent overwhelming news sources
### Dependencies
- `@modelcontextprotocol/sdk@1.11.4` - MCP SDK
- `zod` - Input validation and schema definition
### File Structure
