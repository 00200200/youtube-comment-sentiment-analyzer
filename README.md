# 🎭 Emotube: YouTube Comment Sentiment Analyzer

<div align="center">

![Emotube Banner](https://img.shields.io/badge/Emotube-Sentiment_Analyzer-blue?style=for-the-badge&logo=youtube&logoColor=white)

**An experimental web application for analyzing sentiment in YouTube comments**

[![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black)](https://reactjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)](https://www.docker.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat&logo=postgresql&logoColor=white)](https://www.postgresql.org/)

</div>

---

## 🌟 Overview

Emotube fetches YouTube video metadata and top-level comments through the YouTube Data API, classifies comments with a pretrained Hugging Face sentiment model, and stores the results in PostgreSQL. A React interface displays video details, comment filters, and sentiment charts. YouTube is the only implemented platform; replies within comment threads are not fetched.

### ✨ Key Features

- **🎯 Sentiment Classification** - Positive, neutral, negative, and ambiguous labels with model scores
- **📊 Charts** - Sentiment counts over time with date-range selection
- **🐳 Docker Compose** - Frontend, backend, and database services for local development
- **⚡ Background Analysis** - Comment fetching and classification through FastAPI background tasks; the frontend polls every 3 seconds
- **🔍 Comment Filters** - Sentiment, author, minimum likes, text search, and sorting
- **📈 Video Metrics** - View, like, and comment counts plus derived engagement statistics

---

## 🖥️ User Interface Showcase

### 🏠 Home Page & Video Analysis

<div align="center">

**Home Page**
![Home Page](readme_photos/ui_home.png)

**YouTube URL Input and Analysis Initiation**
![Video URL Query](readme_photos/ui_home_query.png)

</div>

### 💬 Comment Analysis Interface

<div align="center">

**Video Information**
![Video Header](readme_photos/ui_video_header.png)

**Interactive Sentiment Analysis Charts**
![Sentiment Charts](readme_photos/ui_video_chart.png)

**Chart Filtering by Time Period**
![Chart Period Filtering](readme_photos/ui_video_chart_period.png)

**Comment Sentiment Labels and Filters**
![Comments Analysis](readme_photos/ui_video_comments.png)

</div>

### ✨ Key UI Features

- **🎨 Interface** - React components styled with Tailwind CSS and ShadCN/UI
- **📊 Charts** - Sentiment visualization with Recharts
- **🔍 Filters** - Comment filtering and sorting
- **⚡ Progress Display** - Periodic polling of analysis status
- **🌙 Theme Support** - A theme provider with dark mode as the default

---

## 🏗️ Architecture

Docker Compose runs a React frontend, a FastAPI backend, and PostgreSQL. Analysis runs inside the backend process; there is no separate worker service or durable job queue.

```
Emotube/
├── 🐳 docker-compose.yml           # Multi-service orchestration
├── 🔧 .env.example                 # Environment configuration template
├── 🌐 frontend/                    # React TypeScript Frontend
│   ├── 🐳 Dockerfile               # Frontend container config
│   ├── 📦 package.json             # Dependencies (Bun runtime)
│   ├── ⚙️ vite.config.js           # Build configuration
│   └── 📁 src/
│       ├── 🎨 components/          # React components
│       │   ├── ui/                 # ShadCN UI components
│       │   ├── VideoDetails.tsx    # Video metadata display
│       │   ├── CommentSection.tsx  # Comment analysis interface
│       │   ├── CommentCharts.tsx   # Data visualization charts
│       │   └── AnalyzedVideoList.tsx # Video history
│       ├── 🚦 routes/              # TanStack Router pages
│       ├── 🔗 services/            # API service layer
│       ├── 🎯 hooks/               # Custom React hooks
│       └── 📝 types/               # TypeScript definitions
├── ⚡ backend/                     # FastAPI Python Backend
│   ├── 🐳 Dockerfile               # Backend container config
│   ├── 📋 requirements.txt         # Python dependencies
│   ├── 📚 overview.md              # Detailed backend documentation
│   └── 📁 app/
│       ├── 🚀 main.py              # FastAPI application entry
│       ├── 🌐 api/
│       │   ├── routes/             # API endpoints
│       │   │   ├── videos.py       # Video analysis endpoints
│       │   │   ├── comments.py     # Comment retrieval & filtering
│       │   │   └── chart_data.py   # Analytics data endpoints
│       │   └── logic/              # Business logic layer
│       ├── ⚙️ core/
│       │   ├── config.py           # Application configuration
│       │   ├── sentiment/          # Sentiment analysis engine
│       │   └── integrations/       # Social media platform integrations
│       │       └── youtube/        # YouTube API integration
│       ├── 🗄️ db/
│       │   ├── session.py          # Database session management
│       │   └── init_db.py          # Database initialization
│       ├── 📊 models/              # SQLModel database models
│       ├── 📝 schemas/             # Pydantic API schemas
│       ├── 🔧 crud/                # Database operations
│       └── 🛠️ utils/               # Utility functions
└── 🗄️ PostgreSQL Database         # Persistent data storage
```

---

## 🚀 Tech Stack

### Backend

- **🐍 Python 3.11** with **FastAPI** - API routes and background tasks
- **🤖 Transformers & PyTorch** - Pretrained sentiment classifier
- **🗄️ PostgreSQL + SQLModel** - Database models and async sessions
- **📡 Google API Client** - YouTube Data API integration
- **⚡ Uvicorn** - ASGI server with auto-reload

### Frontend

- **⚛️ React 19** with **TypeScript** - Frontend components
- **🦄 Bun** - JavaScript runtime and package manager
- **🧭 TanStack Router** - Type-safe routing with devtools
- **🔄 TanStack Query** - API queries and polling
- **🎨 Tailwind CSS** - Utility-first styling framework
- **🧩 ShadCN/UI** - UI components
- **📊 Recharts** - Responsive data visualization
- **⚡ Vite** - Development server and build tool

### Infrastructure

- **🐳 Docker & Docker Compose** - Local service configuration
- **🔧 Environment Variables** - API key, database connection, and service URLs
- **🌐 CORS-enabled API** - Cross-origin resource sharing
- **📝 Auto-generated API Docs** - Interactive Swagger/OpenAPI

---

## 🚀 Quick Start

### Prerequisites

- 🐳 **Docker** and **Docker Compose**
- 🔑 **YouTube Data API v3 Key** ([Get one here](https://developers.google.com/youtube/v3/getting-started))
- Network access for dependencies, initial model downloads, and YouTube API requests; comment fetching uses your API quota.

### 1. Clone the Repository

```bash
git clone https://github.com/00200200/youtube-comment-sentiment-analyzer
cd youtube-comment-sentiment-analyzer
```

### 2. Environment Setup

```bash
# Copy environment template
cp .env.example .env

# Edit .env file with your configuration
nano .env  # or use your preferred editor
```

**Required environment variables:**

```env
# YouTube API Configuration
YOUTUBE_API_KEY=your_youtube_api_key_here

# Service Configuration
HOST=0.0.0.0
BACKEND_PORT=8000
FRONTEND_PORT=3000

# Database Configuration
POSTGRES_USER=emotube_user
POSTGRES_PASSWORD=secure_password_here
POSTGRES_DB=emotube_db
POSTGRES_HOST=db
POSTGRES_PORT=5432
DATABASE_URL=postgresql+asyncpg://${POSTGRES_USER}:${POSTGRES_PASSWORD}@${POSTGRES_HOST}:${POSTGRES_PORT}/${POSTGRES_DB}

# Frontend Configuration
VITE_BACKEND_URL=http://localhost:8000
```

### 3. Launch with Docker

```bash
# Start all services
docker-compose up -d

# View logs (optional)
docker-compose logs -f
```

### 4. Access the Application

- 🌐 **Frontend**: [http://localhost:3000](http://localhost:3000)
- ⚡ **Backend API**: [http://localhost:8000](http://localhost:8000)
- 📚 **API Docs**: [http://localhost:8000/docs](http://localhost:8000/docs)
- 🗄️ **Database**: `localhost:5432`

The supplied Compose setup uses Vite's development server, Uvicorn auto-reload, source mounts, and published database/API ports. The API has no authentication and allows all CORS origins. Treat this as a local development setup, not a production deployment template. Initial backend startup may take time to download and load the model.

---

## 🎯 Usage

### Analyzing YouTube Videos

1. **📱 Navigate** to the frontend application
2. **🔗 Enter** a YouTube video URL
3. **⚡ Watch** analysis status update through periodic polling
4. **📊 Explore** interactive charts and comment insights
5. **🔍 Filter** comments by sentiment, author, or keywords
6. **📈 View** sentiment counts over time and video engagement metrics

### API Endpoints

#### Videos

- `GET /videos` - List analyzed videos (paginated)
- `GET /videos?url={youtube_url}` - Analyze new video or get existing analysis

#### Comments

- `GET /comments?url={youtube_url}` - Get stored comments with filtering:
  - `sentiment` - Filter by sentiment (positive/negative/neutral/ambiguous)
  - `author` - Filter by author name
  - `min_likes` - Minimum like count
  - `phrase` - Text search within comments
  - `sort_by` - Sort field (for example, `published_at`, `like_count`, or `sentiment_label`)
  - `sort_order` - asc/desc

#### Analytics

- `GET /chart-data?url={youtube_url}` - Get visualization data

---

## 🌐 Platform Scope

The only integration is [`backend/app/core/integrations/youtube/`](backend/app/core/integrations/youtube/).
The routes, URL parsing, data models, and frontend are built around YouTube videos.
Supporting another platform would require implementation and testing across those parts of the application.

---

## 🛠️ Development

### Local Development Setup

This setup requires Python 3.11 and Bun. Configure the root `.env` first. For processes outside Docker, use
`localhost` in `DATABASE_URL` instead of the Compose hostname `db`. The example below
uses the credentials shown above; replace them with your configured values.

```bash
# Backend development, from the repository root
docker-compose up -d db
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
DATABASE_URL=postgresql+asyncpg://emotube_user:secure_password_here@localhost:5432/emotube_db \
  uvicorn app.main:app --reload --env-file ../.env

# Frontend development, in a separate terminal from the repository root
cd frontend
bun install
VITE_BACKEND_URL=http://localhost:8000 bun run start
```

### Docker Development

```bash
# Rebuild and restart services
docker-compose down
docker-compose up --build

# View service logs
docker-compose logs backend
docker-compose logs frontend
docker-compose logs db
```

### Database Management

```bash
# Access PostgreSQL
docker-compose exec db psql -U emotube_user -d emotube_db

# Backup database
docker-compose exec db pg_dump -U emotube_user emotube_db > backup.sql

# View database logs
docker-compose logs db
```

---

## 📊 Features Deep Dive

### Sentiment Analysis Engine

- **🤖 Model** - `cardiffnlp/twitter-xlm-roberta-base-sentiment`, configured in [`config.py`](backend/app/core/config.py)
- **🎯 Scores** - Stores the model's predicted label and score; scores below `0.6` are labeled `ambiguous`
- **🔄 Processing** - Fetches pages of top-level comments, then classifies and saves comments individually
- **📏 Input Limit** - Model inputs are truncated to 512 tokens

### Data Visualization

- **📊 Timeline** - Area charts of comment counts by sentiment and publication date
- **🔍 Comment View** - Filtered comments, model scores, and sentiment totals
- **📈 Video Details** - Counts and derived engagement metrics; no word clouds or dislike-correlation analysis are implemented

### Limitations

- Analysis is an on-demand background pass, not a stream of new YouTube comments. Polling refreshes stored results and status.
- Model scores are predictions, not verified measurements of a commenter's intent. The repository does not report a sentiment-accuracy evaluation on YouTube comments.
- API availability, quota, comment volume, and local inference speed affect completion time. This project does not provide a real-time latency guarantee.

---
