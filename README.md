# Tatakai API 🎌

> Unified Anime API combining HiAnime, regional scrapers, and utility APIs with modern caching, CORS, rate limiting, and logging.

## Social
> Discord : https://dsc.gg/tatakai

Disclaimer 
- No other Social Media Handle is availaible right now, If you see then please report us as we only have **discord server** .

## Features

- 🚀 **Modern Stack**: Built with [Hono](https://hono.dev/) - ultra-fast, lightweight web framework
- 💾 **Hybrid Caching**: Redis with LRU in-memory fallback
- 🔒 **Rate Limiting**: Configurable per-IP rate limiting
- 📝 **Structured Logging**: Pino logger with pretty dev output
- 🌐 **CORS Ready**: Configurable origin whitelisting
- 🐳 **Docker Ready**: Multi-stage Dockerfile included
- 📦 **TypeScript**: Full type safety
- 🧪 **Comprehensive Testing**: Built-in endpoint validation scripts

## API Endpoints

| Route | Description |
|-------|-------------|
| `/api/v1/hianime/*` | HiAnime scraper - search, info, episodes, sources |
| `/api/v1/animeya/*` | Animeya streaming platform |
| `/api/v1/anime/*` | External anime search providers (GogoAnime, Chia-Anime, etc.) |
| `/api/v1/anime-api/*` | Utility APIs (quotes, trace, images, facts, waifu) |
| `/api/v1/hindidubbed/*` | Hindi dubbed anime scraper |
| `/api/v1/animelok/*` | AnimeLok multi-language streaming |
| `/api/v1/watchaw/*` | WatchAnimeWorld multi-language streaming |
| `/api/v1/desidubanime/*` | DesiDubAnime - Hindi/regional dubbed anime |
| `/api/v1/aniworld/*` | AniWorld - German anime streaming (aniworld.to) |
| `/api/v1/toonstream/*` | ToonStream episodes and watch links |
| `/api/v1/hindiapi/*` | Hindi stream resolver + proxy |
| `/api/v1/anilisthindi/*` | AniList-Hindi episode resolver + proxy |
| `/api/v1/toonworld/*` | ToonWorld search and episode scraping |
| `/api/v1/webhooks/*` | Webhook endpoints (Discord) |
| `/health` | Health check |
| `/version` | API version info |
| `/api/v1/docs/llm` | Full LLM-friendly documentation |

## Route Details

For the complete v5 endpoint inventory (method + path for every mounted route), open:

- `/docs/endpoints`
- `/api/v1/docs/llm`

## Quick Start

### Prerequisites

- Node.js >= 18
- npm or yarn
- Redis (optional, for distributed caching)

### Installation

```bash
# Clone and install
cd TatakaiAPI
npm install

# Create .env file
cp .env.example .env

# Start development server
npm run dev
```

### Docker

```bash
# Build and run with Docker Compose
docker-compose up -d

# Or build image only
docker build -t tatakai-api .
docker run -p 4000:4000 tatakai-api
```

## Configuration

| Variable | Description | Default |
|----------|-------------|---------|
| `PORT` | Server port | `4000` |
| `NODE_ENV` | Environment | `development` |
| `REDIS_URL` | Redis connection URL | (empty = in-memory) |
| `CORS_ALLOWED_ORIGINS` | Allowed origins (comma-separated) | `*` |
| `RATE_LIMIT_WINDOW_MS` | Rate limit window | `60000` |
| `RATE_LIMIT_MAX_REQUESTS` | Max requests per window | `100` |
| `CACHE_TTL_SECONDS` | Default cache TTL | `300` |

## Testing

Run the comprehensive test suite to validate all API endpoints:

```bash
# Run basic validation
npm run test

# Run comprehensive endpoint tests
npm run test:comprehensive
```

The comprehensive test script checks all routes with sample parameters and reports success/failure status for each endpoint.

## Example Requests

```bash
# HiAnime home page
curl http://localhost:4000/api/v1/hianime/home

# Search anime on HiAnime
curl "http://localhost:4000/api/v1/hianime/search?q=naruto"

# External anime search (GogoAnime)
curl "http://localhost:4000/api/v1/anime/gogoanime/naruto"

# Anime quotes
curl "http://localhost:4000/api/v1/anime-api/quotes/random"

# Anime images
curl "http://localhost:4000/api/v1/anime-api/images/waifu"

# Hindi dubbed search
curl "http://localhost:4000/api/v1/hindidubbed/search?title=naruto"

# Animeya home
curl "http://localhost:4000/api/v1/animeya/home"
```

## Project Structure

```
TatakaiAPI/
├── src/
│   ├── config/       # Configuration (env, cache, cors, logger, etc.)
│   ├── docs/         # API documentation markdown files
│   ├── middleware/   # Hono middleware (logging, cache control)
│   ├── routes/       # API routes by provider
│   │   ├── hianime/          # HiAnime scraper
│   │   ├── anime/            # External search providers
│   │   ├── anime-api/        # Utility APIs
│   │   ├── animehindidubbed/ # Hindi dubbed scraper
│   │   ├── animelok/         # AnimeLok multi-language
│   │   ├── animeya/          # Animeya platform
│   │   ├── watchanimeworld/  # WatchAnimeWorld
│   │   ├── desidubanime/     # DesiDubAnime Hindi
│   │   └── aniworld/         # AniWorld German
│   ├── server.ts     # Main entry point
│   └── utils.ts      # Utility functions
├── scripts/          # Utility scripts
│   ├── comprehensive_test.ts  # Full API endpoint testing
│   └── validate_api.ts        # API validation script
├── public/           # Static files & docs UI
├── Dockerfile
└── docker-compose.yml
```

## License

MIT
