# MCP Server Configuration

This documentation covers the setup and capabilities of multiple MCP (Model Context Protocol) servers for database and cloud service integrations.

## 1. PostgreSQL MCP Servers Setup

Below is the MCP configuration for connecting to multiple PostgreSQL databases:

```json
{
  "mcpServers": {
    // MCP server for bi_chatbot database - provides SQL query capabilities
    "postgres-bi-chatbot": {
      "command": "npx", // Node package executor to run packages without installing
      "args": [
        "-y", // Auto-confirm prompts, skip interactive installation
        "@modelcontextprotocol/server-postgres", // MCP PostgreSQL server package
        "postgresql://postgres:cikalmerdeka@localhost:5432/bi_chatbot" // Connection string: protocol://user:password@host:port/database
      ]
    },
    // MCP server for airbnb database - provides SQL query capabilities
    "postgres-airbnb": {
      "command": "npx", // Node package executor to run packages without installing
      "args": [
        "-y", // Auto-confirm prompts, skip interactive installation
        "@modelcontextprotocol/server-postgres", // MCP PostgreSQL server package
        "postgresql://postgres:cikalmerdeka@localhost:5432/airbnb" // Connection string: protocol://user:password@host:port/database
      ]
    },
    // MCP server for Google Sheets - provides spreadsheet management capabilities
    "googlesheets": {
      "url": "https://mcp.composio.dev/partner/composio/googlesheets/mcp?customerId=YOUR_CUSTOMER_ID&agent=cursor" // Composio Google Sheets MCP endpoint with OAuth integration
    }
  }
}
```

## 1.1 PostgreSQL MCP Server Setup

The PostgreSQL MCP servers use the official package from the Model Context Protocol:

```json
"postgres-bi-chatbot": {
  "command": "npx", // Node package executor to run packages without installing
  "args": [
    "-y", // Auto-confirm prompts, skip interactive installation
    "@modelcontextprotocol/server-postgres", // MCP PostgreSQL server package
    "postgresql://postgres:cikalmerdeka@localhost:5432/bi_chatbot" // Connection string: protocol://user:password@host:port/database
  ]
}
```

### Configuration Parameters
- **command**: "npx" - Node package executor that runs packages without installing them globally
- **args**: Array containing the package and connection details
- **Connection String Format**: `postgresql://username:password@host:port/database`

### Available Tools

The official PostgreSQL MCP server provides the following capabilities:

#### **Database Schema Exploration**
- `list_schemas` - List all database schemas available in the PostgreSQL instance
- `list_tables` - List database objects (tables, views, sequences) within a specified schema
- `describe_table` - Provides detailed information about a specific table (columns, constraints, indexes)

#### **Query Execution**
- `query` - Execute read-only SQL SELECT queries with optional prepared statement parameters
- `read_query` - Safe read-only query execution with result limiting and timeout controls

#### **Connection Management**
- Automatic connection pooling and management
- Secure credential handling through connection strings
- Support for SSL connections and advanced PostgreSQL features

### Capabilities & Limitations

**✅ What it CAN do:**
- Execute read-only SQL queries (SELECT statements)
- Browse database schemas and table structures
- Inspect table columns, data types, and constraints
- View indexes and foreign key relationships
- Support for complex queries with JOINs, aggregations, and subqueries
- Prepared statement parameter binding for security

**❌ What it CANNOT do:**
- Execute write operations (INSERT, UPDATE, DELETE, DROP)
- Modify database schema or structure
- Create or drop tables, indexes, or other database objects
- Execute stored procedures or functions
- Administrative operations (user management, permissions)

**Best for:** Safe database exploration, data analysis, reporting, and read-only business intelligence queries.

### Advanced Alternative: Postgres MCP Pro

For production environments requiring more advanced capabilities, consider **Postgres MCP Pro** which includes:

- **Database Health Checks** - Analyze index health, connection utilization, buffer cache
- **Index Tuning** - AI-powered index recommendations using optimization algorithms
- **Query Performance Analysis** - EXPLAIN plans and query optimization suggestions
- **Safe SQL Execution** - Configurable read-only and restricted modes
- **Workload Analysis** - Identify slow queries and resource bottlenecks

## 4. Configuration Explanation

- **npx**: Node package executor that runs packages without installing them globally
- **-y**: Auto-confirms prompts and skips interactive installation
- **@modelcontextprotocol/server-postgres**: The official PostgreSQL MCP server package
- **Connection String Format**: `postgresql://username:password@host:port/database`

## 2. LangGraph Documentation MCP Server Setup

The LangGraph documentation MCP server provides access to comprehensive documentation for LangGraph and LangChain:

```json
"langgraph-docs-mcp": {
  "command": "uvx", // Python package runner that executes packages from PyPI
  "args": [
    "--from", // Specify the package to install from
    "mcpdoc", // Package name containing the MCP documentation server
    "mcpdoc", // Command to run from the package
    "--urls", // Documentation sources to index
    "LangGraph:https://langchain-ai.github.io/langgraph/llms.txt LangChain:https://python.langchain.com/llms.txt", // Space-separated list of documentation URLs
    "--transport", // Communication protocol
    "stdio" // Standard input/output transport
  ]
}
```

### Configuration Parameters
- **command**: "uvx" - Python package runner for executing packages from PyPI without installation
- **args**: Array containing package specification and configuration options
- **--from**: Specifies the source package (mcpdoc)
- **--urls**: Documentation sources in format "Name:URL" separated by spaces
- **--transport**: Communication protocol (stdio for standard input/output)

### Available Tools

The LangGraph documentation MCP server provides the following capabilities:

#### **Documentation Access**
- `list_doc_sources` - List all available documentation sources and their URLs
- `fetch_docs` - Fetch and parse documentation from specific URLs or local files

#### **Content Retrieval**
- Access to comprehensive LangGraph documentation covering:
  - Memory types (short-term, long-term, semantic, episodic, procedural)
  - Agent architectures and multi-agent systems
  - Graph construction and execution
  - Streaming and persistence capabilities
  - Human-in-the-loop workflows
  - Platform deployment options

#### **Search and Navigation**
- Structured access to documentation sections
- Cross-referencing between related topics
- Real-time documentation updates from official sources

### Capabilities & Limitations

**✅ What it CAN do:**
- Provide detailed explanations of LangGraph concepts and features
- Access the latest documentation from official sources
- Explain implementation patterns and best practices
- Offer code examples and tutorials
- Cover both basic and advanced LangGraph usage

**❌ What it CANNOT do:**
- Execute or run LangGraph code directly
- Modify or update the documentation sources
- Provide real-time debugging of LangGraph applications
- Access private or custom documentation sources

**Best for:** Learning LangGraph concepts, understanding implementation patterns, getting detailed explanations of features, and accessing comprehensive documentation for development guidance.

## 3. Google Sheets MCP Server Setup

The Google Sheets MCP server is provided by Composio and requires OAuth authentication:

```json
"googlesheets": {
  "url": "https://mcp.composio.dev/partner/composio/googlesheets/mcp?customerId=YOUR_CUSTOMER_ID&agent=cursor"
}
```

### Configuration Parameters
- **url**: Composio-hosted MCP server endpoint for Google Sheets integration
- **customerId**: Your unique Composio customer identifier (obtained during account setup)
- **agent**: Target application (cursor for Cursor IDE integration)

### Available Tools

#### **Core Sheet Operations**
- `GOOGLESHEETS_ADD_SHEET` - Add new worksheets/tabs to spreadsheet
- `GOOGLESHEETS_DELETE_SHEET` - Remove existing sheets
- `GOOGLESHEETS_GET_SPREADSHEET_INFO` - Get spreadsheet metadata, sheets list, properties

#### **Row/Column Management**  
- `GOOGLESHEETS_INSERT_DIMENSION` - Insert rows/columns at specific positions
- `GOOGLESHEETS_DELETE_DIMENSION` - Delete specified rows/columns
- `GOOGLESHEETS_APPEND_DIMENSION` - Add rows/columns to the end

#### **Filtering & Sorting**
- `GOOGLESHEETS_SET_BASIC_FILTER` - Apply filters and sorting to data ranges
- `GOOGLESHEETS_CLEAR_BASIC_FILTER` - Remove existing filters

#### **Advanced Features**
- `GOOGLESHEETS_SEARCH_DEVELOPER_METADATA` - Find custom metadata entries

#### **Connection Management**
- `GOOGLESHEETS_CHECK_ACTIVE_CONNECTION` - Verify authentication status
- `GOOGLESHEETS_INITIATE_CONNECTION` - Start OAuth authentication process

### Capabilities & Limitations

**✅ What it CAN do:**
- Create and delete sheets/worksheets
- Manage sheet structure (rows, columns)
- Set up filters and sorting
- Handle spreadsheet metadata
- OAuth authentication management

**❌ What it CANNOT do:**
- Read or write cell data/values
- Apply cell formatting (colors, fonts, borders)
- Create charts or pivot tables
- Handle cell formulas
- Batch data operations

**Best for:** Spreadsheet structure management, template creation, and data organization setup.

## 5. Connected Services

### **Databases**
1. **bi_chatbot**: Olist e-commerce dataset with 8 tables (customers, orders, products, etc.)
2. **airbnb**: Airbnb dataset for analysis

### **Cloud Services**
1. **Google Sheets**: Spreadsheet management and structure operations

### **Documentation Services**
1. **LangGraph Documentation**: Comprehensive documentation access for LangGraph and LangChain frameworks

## 6. Usage

After configuration, restart Cursor to enable the MCP servers. Each database will have its own query tool available in the chat interface.

### Authentication Requirements

#### **PostgreSQL Servers**
- **Pre-configured credentials** via connection strings in mcp.json
- **Automatic connection** - No additional setup required after configuration
- **Secure connections** - Supports SSL and advanced PostgreSQL authentication methods

#### **Google Sheets Server**  
- **OAuth authentication required** - One-time browser-based setup
- **Browser authorization** - Opens redirect URL for Google account access
- **Persistent sessions** - Authentication persists across MCP client restarts
