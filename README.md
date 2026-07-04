# LLM Zoomcamp 2026: RAG Application

A comprehensive RAG (Retrieval Augmented Generation) application demonstrating various approaches to building intelligent systems with language models. This project showcases implementations ranging from basic chat to multi-agent research systems.

**Learning Progress**: This repository documents my learning journey through [LLM Zoomcamp 2026](https://github.com/DataTalksClub/llm-zoomcamp/tree/main), an open-source course on building LLM applications.

## 📋 Overview

This project explores:
- **RAG Fundamentals**: Understanding how retrieval augmented generation improves LLM responses
- **Vector Search**: Implementing semantic search with embeddings
- **Workflow Automation**: Using Kestra for orchestrating LLM-powered workflows
- **Agent Systems**: Building autonomous agents for research and problem-solving
- **Multi-Agent Collaboration**: Coordinating multiple specialized agents

## 🏗️ Project Structure

### Core Python Modules

- **`rag_helper.py`**: Core RAG implementations
  - `RAGBase`: Base class for RAG systems with search, context building, and prompt engineering
  - `RAGVector`: Vector-based RAG using embeddings for semantic search
  - Customizable instructions, prompt templates, and model configuration

- **`ingest.py`**: Data ingestion utilities
  - Loads FAQ data from remote sources
  - Builds searchable indexes with minsearch
  - Supports course-based document filtering

### Workflow Orchestration

The `flows/` directory contains Kestra workflows demonstrating progressive complexity:

1. **`1_chat_without_rag.yaml`**: 
   - Basic LLM chat without context retrieval
   - Demonstrates limitations of training data-only approaches

2. **`2_chat_with_rag.yaml`**: 
   - Implements RAG with document ingestion
   - Retrieves relevant context before generating responses
   - Shows how RAG improves accuracy

3. **`3_rag_with_websearch.yaml`**: 
   - Combines RAG with web search capabilities
   - Enables responses with current, real-time information

4. **`4_simple_agent.yaml`**: 
   - Basic agentic loop with tool calling
   - Introduces autonomous decision-making

5. **`5_web_research_agent.yaml`**: 
   - Specialized agent for web research tasks
   - Multi-step reasoning for complex queries

6. **`6_multi_agent_research.yaml`**: 
   - Multiple coordinated agents
   - Task specialization and collaboration

### Jupyter Notebooks

- **`01_agentic_rag.ipynb`**: Agentic RAG implementation and experimentation
- **`02_vector_search.ipynb`**: Vector search and semantic similarity exploration

## 🚀 Getting Started

### Prerequisites

- Docker and Docker Compose
- Python 3.8+
- API Keys for:
  - Google Gemini (or your preferred LLM provider)
  - Tavily API (for web search)
  - OpenAI API (optional)

### Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/divakartika/llm-zoomcamp-2026.git
   cd llm-zoomcamp-2026
   ```

2. **Configure environment variables**
   Create a `.env` file with your API keys:
   ```bash
   export SECRET_GEMINI_API_KEY=your-gemini-key
   export SECRET_TAVILY_API_KEY=your-tavily-key
   export SECRET_OPENAI_API_KEY=your-openai-key
   ```

3. **Start Kestra with Docker Compose**
   ```bash
   docker-compose up -d
   ```
   This will start:
   - **Kestra Server**: http://localhost:8080
   - **PostgreSQL Database**: For storing workflows and execution history
   
   Default credentials:
   - Username: `admin@kestra.io`
   - Password: `Admin1234!`

4. **Install Python dependencies**
   ```bash
   pip install -r requirements.txt
   ```
   Required packages:
   - `requests`: HTTP client for API calls
   - `minsearch`: Lightweight search library
   - `jupyter`: For notebook environments

### Running Workflows

1. Access Kestra UI at `http://localhost:8080`
2. Navigate to the flows in the dashboard
3. Execute workflows in order (1 → 2 → 3) to understand progression
4. Monitor execution and view results in real-time

### Using Jupyter Notebooks

```bash
jupyter notebook 01_agentic_rag.ipynb
```

Or for vector search experimentation:

```bash
jupyter notebook 02_vector_search.ipynb
```

## 🔧 Key Concepts

### RAG (Retrieval Augmented Generation)

RAG enhances LLM responses by:
1. **Retrieval**: Finding relevant documents/context for a query
2. **Augmentation**: Combining retrieved context with the user query
3. **Generation**: Using the LLM to synthesize a response grounded in context

### Vector Search

The `RAGVector` class implements semantic search:
- Encodes queries and documents as embeddings
- Finds semantically similar results regardless of exact keyword matches
- Supports filtering by metadata (e.g., course)

### Agents & Multi-Agent Systems

Agents operate in loops:
1. Observe the current state
2. Decide what action to take
3. Execute the action
4. Repeat until goal is achieved

Multi-agent systems coordinate multiple specialized agents for complex tasks.

## 📊 Architecture

```
┌─────────────────┐
│  User Query     │
└────────┬────────┘
         │
    ┌────▼─────┐
    │ Retrieval │ ◄─── Search Index / Vector DB
    └────┬─────┘
         │
    ┌────▼──────────┐
    │ Context + LLM  │ ◄─── Language Model
    └────┬──────────┘
         │
    ┌────▼──────────┐
    │ Generated      │
    │ Response       │
    └───────────────┘
```

## 🔌 API Integrations

- **Google Gemini**: LLM and embedding models
- **Tavily**: Web search API for real-time information
- **OpenAI**: Alternative LLM provider support

## 📝 Example Usage

### Basic RAG with Vector Search

```python
from rag_helper import RAGVector
from ingest import load_faq_data, build_index

# Load data
documents = load_faq_data()
index = build_index(documents)

# Initialize RAG with vector search
rag = RAGVector(
    embedder=your_embedder,
    index=index,
    llm_client=your_llm_client,
    course="llm-zoomcamp"
)

# Get answer
answer = rag.rag("What is RAG?")
print(answer)
```

## 🧪 Experimentation

Use the sandbox notebooks to:
- Test different prompt templates
- Experiment with search parameters
- Evaluate RAG performance
- Develop custom workflows

## 📚 Learning Path

1. Start with flow `1_chat_without_rag` to see LLM limitations
2. Explore `2_chat_with_rag` to understand RAG benefits
3. Progress through flows 3-6 for advanced concepts
4. Use notebooks for hands-on experimentation
5. Modify flows to implement custom logic

## 🤝 Contributing

Feel free to extend this project:
- Add new RAG strategies
- Implement different search backends
- Create specialized agents
- Optimize prompt templates

## 📄 License

This project is part of LLM Zoomcamp 2026.

## 🔗 Resources

- [Kestra Documentation](https://kestra.io)
- [Google Gemini API](https://ai.google.dev)
- [Tavily API](https://tavily.com)
- [RAG Concepts](https://www.deeplearning.ai)
