# 🐊 Gator - RSS Feed Aggregator

A modern, high-performance RSS feed aggregator built with Go that allows users to follow multiple RSS feeds and retrieve posts efficiently.

## ✨ Features

- **🚀 High Performance**: Built with Go and Chi router for blazing-fast performance
- **📡 RSS Feed Scraping**: Automatically fetches and parses RSS feeds at configurable intervals
- **👥 User Management**: Secure user authentication with API keys
- **📰 Feed Management**: Create, follow, and manage multiple RSS feeds
- **🔄 Concurrent Processing**: Goroutine-based concurrent feed scraping
- **🛡️ CORS Support**: Cross-origin resource sharing configured for web applications
- **🗄️ PostgreSQL Database**: Robust data persistence with SQLC for type-safe queries
- **📡 RESTful API**: Clean REST API endpoints for all operations

## 🏗️ Architecture

- **Go 1.25.6** - Modern Go with latest features
- **Chi Router** - Lightweight, fast HTTP router
- **PostgreSQL** - Reliable database with SQLC for type-safe database operations
- **Concurrent Scraping** - Multiple goroutines for efficient feed processing
- **Environment Configuration** - Secure configuration with .env files

## 🚀 Quick Start

### Prerequisites

- Go 1.25.6 or higher
- PostgreSQL database
- Git

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/nayemmmmmmmmmm/gator.git
   cd gator
   ```

2. **Install dependencies**
   ```bash
   go mod download
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env
   ```
   
   Edit `.env` with your configuration:
   ```env
   PORT=8080
   DB_URL=postgres://username:password@localhost:5432/gator_db?sslmode=disable
   ```

4. **Set up the database**
   ```bash
   # Create database
   createdb gator_db
   
   # Run migrations (if using goose)
   goose up
   ```

5. **Run the application**
   ```bash
   go run main.go
   ```

The server will start on `http://localhost:8080`

## 📡 API Endpoints

### Health Check
- `GET /v1/healthz` - Health check endpoint
- `GET /v1/err` - Error testing endpoint

### User Management
- `POST /v1/users` - Create a new user
- `GET /v1/users` - Get current user (requires authentication)

### Feed Management
- `POST /v1/feeds` - Create a new feed (requires authentication)
- `GET /v1/feeds` - Get all feeds
- `GET /v1/posts` - Get posts for followed feeds (requires authentication)

### Feed Following
- `POST /v1/feed_follows` - Follow a feed (requires authentication)
- `GET /v1/feed_follows` - Get followed feeds (requires authentication)
- `DELETE /v1/feed_follows/{feedFollowID}` - Unfollow a feed (requires authentication)

## 🔐 Authentication

The API uses API key-based authentication. Include your API key in the `Authorization` header:

```
Authorization: ApiKey <your-api-key>
```

## 🗄️ Database Schema

The application uses the following main tables:

- **users** - User information and API keys
- **feeds** - RSS feed information
- **feed_follows** - User-feed relationships
- **posts** - Scraped posts from feeds

## ⚙️ Configuration

The scraper runs concurrently with configurable parameters:
- **Concurrency**: Number of goroutines (default: 10)
- **Interval**: Time between scraping cycles (default: 1 minute)

## 🛠️ Development

### Project Structure

```
gator/
├── main.go                 # Application entry point
├── handler_*.go           # HTTP handlers
├── middleware_auth.go     # Authentication middleware
├── models.go              # Data models and converters
├── scraper.go             # RSS feed scraping logic
├── rss.go                 # RSS parsing utilities
├── internal/              # Internal packages
│   └── database/          # Database queries (SQLC generated)
├── sql/                   # Database schema and migrations
│   ├── schema/           # SQL schema files
│   └── queries/          # SQL query files
└── vendor/                # Go dependencies
```

### Key Technologies

- **[Chi](https://github.com/go-chi/chi)** - HTTP router
- **[SQLC](https://sqlc.dev/)** - Type-safe SQL code generation
- **[lib/pq](https://github.com/lib/pq)** - PostgreSQL driver
- **[godotenv](https://github.com/joho/godotenv)** - Environment variable management

### Running Tests

```bash
go test ./...
```

### Building

```bash
# Build for current platform
go build -o gator

# Build for multiple platforms
GOOS=linux GOARCH=amd64 go build -o gator-linux
GOOS=windows GOARCH=amd64 go build -o gator-windows.exe
GOOS=darwin GOARCH=amd64 go build -o gator-macos
```

## 📈 Performance Features

- **Concurrent Scraping**: Multiple feeds processed simultaneously
- **Database Optimization**: Efficient queries with proper indexing
- **Memory Management**: Optimized for high-throughput scenarios
- **Error Handling**: Robust error recovery and logging

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with [Go](https://golang.org/)
- Database operations powered by [SQLC](https://sqlc.dev/)
- Routing handled by [Chi](https://github.com/go-chi/chi)

## 📞 Support

If you have any questions or issues, please open an issue on the GitHub repository.
