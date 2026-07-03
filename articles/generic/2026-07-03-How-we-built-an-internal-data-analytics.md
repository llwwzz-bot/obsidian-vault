---
url: https://github.blog/ai-and-ml/github-copilot/how-we-built-an-internal-data-analytics-agent/
platform: Web
date: 2026-07-03
tags:
  - LLM
  - Copilot
  - LangChain
  - GPT-4
  - data_analytics
  - internal_tool
  - self-serve_analytics
  - natural_language_to_SQL
source_title: How we built an internal data analytics agent
author: Matteo Vasirani
doc_type: guide
---
# 🧭 How we built an internal data analytics agent

> **操作指南**  |  GitHub 构建了内部数据分析代理 Qubot，允许员工用自然语言查询数据。文章分享了构建过程中的经验教训，包括技术选型、架构设计和实际应用效果。

## 📦 前置条件

- [ ] GitHub Copilot subscription (Enterprise or Business plan)
- [ ] Access to internal data warehouse (e.g., Snowflake, BigQuery, or Redshift)
- [ ] Python 3.8+ with packages: langchain, openai, sqlalchemy, pandas
- [ ] Node.js 18+ (for frontend if applicable)
- [ ] API keys for OpenAI (GPT-4) and GitHub Copilot API
## 🏗️ 架构概览

```mermaid
flowchart TD
    A[User asks question in Copilot] --> B[Backend API receives query]
    B --> C[LangChain SQLDatabaseChain]
    C --> D[LLM generates SQL]
    D --> E[Execute SQL on data warehouse]
    E --> F[Format result as table/chart]
    F --> G[Return to Copilot chat]
```

## 🛠️ 操作步骤

### 1. Define the scope and data sources

Identify which datasets will be queried (e.g., sales, engineering, support). Map out table schemas and relationships. This step ensures the agent only accesses authorized data.
```bash
SELECT table_name, column_name, data_type FROM information_schema.columns WHERE table_schema = 'public';
```


### 2. Set up the LLM backend with LangChain

Use LangChain to create a chain that converts natural language to SQL. The chain includes a prompt template, an LLM (GPT-4), and a SQL database tool.
```bash
pip install langchain openai sqlalchemy pandas
export OPENAI_API_KEY='your-api-key'
export DATABASE_URL='postgresql://user:pass@host:port/db'
```


### 3. Implement the SQL generation chain

Create a LangChain SQLDatabaseChain that takes a question, generates SQL, executes it, and returns the result. Add few-shot examples to improve accuracy.
```bash
from langchain import SQLDatabase, SQLDatabaseChain
from langchain.llms import OpenAI
db = SQLDatabase.from_uri('postgresql://user:pass@host:port/db')
llm = OpenAI(temperature=0, model_name='gpt-4')
chain = SQLDatabaseChain(llm=llm, database=db, verbose=True)
```


### 4. Integrate with GitHub Copilot

Use Copilot's API to allow users to ask questions directly from their editor. Create a custom slash command that sends the query to the backend.
```bash
npm install @github/copilot-api
// Example: register a slash command in your Copilot extension
```


### 5. Add security and access control

Implement row-level security and query validation. Use a whitelist of allowed tables and columns. Log all queries for audit.
```bash
CREATE POLICY user_access ON sales_data FOR SELECT USING (user_id = current_setting('app.current_user')::int);
ALTER TABLE sales_data ENABLE ROW LEVEL SECURITY;
```


### 6. Deploy and test

Deploy the backend as a microservice (e.g., FastAPI) and the frontend as a Copilot extension. Test with sample queries.
```bash
uvicorn main:app --host 0.0.0.0 --port 8000
curl -X POST http://localhost:8000/query -H 'Content-Type: application/json' -d '{"question": "How many active users last month?"}'
```

## ✅ 验证

Run a test query: 'Show me total revenue by product for Q1 2024'. Expected output: a table with product names and revenue sums. Verify that the SQL generated is correct and the result matches a manual query.

## 🐛 踩坑排查

| 问题 | 原因 | 解决 |
|------|------|------|
| LLM generates incorrect SQL (e.g., wrong table name) | Missing or ambiguous schema context in prompt | Add table descriptions and column examples to the prompt template. Use a few-shot prompt with 3-5 examples. |
| Query times out or returns too much data | No limit on rows returned | Add a default LIMIT clause (e.g., LIMIT 100) and warn users if result is large. |
| Copilot extension not responding | API endpoint not reachable or authentication missing | Check network connectivity and ensure the Copilot API token is valid and has correct scopes. |
## 🚀 下一步

- Add support for visualizations (charts) using matplotlib or Plotly
- Implement caching for frequent queries
- Extend to multiple data warehouses (Snowflake, BigQuery)
- Add natural language follow-up questions (conversational context)
## ⚠️ 注意事项

- Always validate SQL before execution to prevent injection or destructive queries (use read-only connections).
- Monitor LLM costs; GPT-4 can be expensive for high-volume usage. Consider caching or using GPT-3.5 for simple queries.
- Productionize with rate limiting and user authentication to avoid abuse.
## 🖼️ 图片

![1](https://rss-collector.liwenzhestudy.workers.dev/img/ad2a1397-a08b-462c-9d92-c079f3808c7b/0)

![2](https://rss-collector.liwenzhestudy.workers.dev/img/ad2a1397-a08b-462c-9d92-c079f3808c7b/1)

![3](https://rss-collector.liwenzhestudy.workers.dev/img/ad2a1397-a08b-462c-9d92-c079f3808c7b/2)
## 📎 原文

[How we built an internal data analytics agent](https://github.blog/ai-and-ml/github-copilot/how-we-built-an-internal-data-analytics-agent/)
