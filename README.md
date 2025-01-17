# Discord RAG Pipeline

A full-stack application that enables scraping Discord servers and querying the data using both RAG (Retrieval Augmented Generation) and SQL approaches. The system uses Modal for serverless deployment, FastAPI for the backend, and React with TypeScript for the frontend.

## Architecture Overview

The application consists of two main services:

1. **Backend Service** (Modal/FastAPI)
   - Handles Discord server scraping
   - Manages SQLite database with vector embeddings
   - Processes queries using either RAG or SQL approaches
   - Integrates with OpenAI for embeddings and completions

2. **Frontend Service** (React/TypeScript)
   - Provides user interface for server scraping
   - Enables natural language querying of Discord data
   - Visualizes the query processing pipeline
   - Built with shadcn/ui components

## Prerequisites

- Python 3.8+
- Bun 1.0+
- Modal CLI
- OpenAI API key
- Discord Bot Token with necessary permissions
- uv (Python package installer)

## Environment Setup

1. Clone the repository:
```bash
git clone <repository-url>
cd discord-rag-pipeline
```

2. Create a `.env` file in the root directory:
```bash
OPENAI_API_KEY=your_openai_api_key
DISCORD_TOKEN=your_discord_bot_token
```

3. Create a `.env` file in the `frontend_service` directory:
```bash
VITE_MODAL_URL=http://localhost:8000  # For local development
```

## Backend Setup

1. Navigate to the backend directory:
```bash
cd backend_service
```

2. Install dependencies with uv:
```bash
uv pip install -r requirements.txt
```

3. Deploy to Modal:
```bash
modal deploy src/modal_app/main.py
```

## Frontend Setup

1. Navigate to the frontend directory:
```bash
cd frontend_service
```

2. Install dependencies with Bun:
```bash
bun install
```

3. Start the development server:
```bash
bun dev
```

## Usage

1. **Scraping Discord Data**
   - Enter your Discord server ID in the scraper form
   - Set the desired message limit
   - Click "Scrape Server" to begin data collection

2. **Querying Data**
   - Enter your question in natural language
   - The system automatically determines whether to use RAG or SQL
   - View the complete processing pipeline in the UI

### Query Examples

- RAG-based queries:
  - "What are the main topics discussed in the server?"
  - "Summarize recent conversations about React"

- SQL-based queries:
  - "How many messages were sent today?"
  - "Who are the most active users?"

## Technical Details

### Database Schema

```sql
CREATE TABLE discord_messages (
    id TEXT PRIMARY KEY,
    channel_id TEXT NOT NULL,
    author_id TEXT NOT NULL,
    content TEXT NOT NULL,
    created_at TIMESTAMP NOT NULL
);

CREATE VIRTUAL TABLE vec_discord_messages USING vec0(
    id TEXT PRIMARY KEY,
    embedding FLOAT[1536]
);
```

### Key Features

- **Vector Search**: Uses SQLite-VEC for efficient similarity search
- **Hybrid Query Processing**: Automatically chooses between RAG and SQL approaches
- **Real-time Processing**: Processes Discord messages and generates embeddings on-the-fly
- **Interactive UI**: Visualizes the complete query processing pipeline

## Development

### Backend Development

The backend uses Modal for serverless deployment and includes:
- FastAPI for API endpoints
- SQLite with vector extension for data storage
- OpenAI integration for embeddings and completions
- uv for fast, reliable Python package management

### Frontend Development

The frontend is built with:
- React 18 with TypeScript
- Vite for build tooling
- shadcn/ui for components
- Lucide icons
- Bun for fast JavaScript runtime and package management

## Troubleshooting

1. **Discord Scraping Issues**
   - Ensure bot has necessary permissions
   - Check server ID is correct
   - Verify Discord token is valid

2. **Query Processing Issues**
   - Confirm OpenAI API key is valid
   - Check database contains scraped messages
   - Verify embeddings are being generated correctly

3. **Package Management Issues**
   - For Python: Try `uv pip install --force-reinstall -r requirements.txt`
   - For JavaScript: Try `bun install --force`

## License

MIT

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request
