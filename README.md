# FastAPI Calculator with Docker & PostgreSQL

A production-ready calculator API built with FastAPI, featuring Docker containerization, PostgreSQL database integration, and pgAdmin for database management.

## Features

- ✨ RESTful API endpoints for basic arithmetic operations
- 🐳 Docker containerization with Docker Compose
- 🗄️ PostgreSQL database integration
- 🎨 Web-based UI using Jinja2 templates
- 📊 pgAdmin for database administration
- ✅ Input validation using Pydantic
- 🔍 Comprehensive error handling and logging
- 🔄 Hot reload during development

## Tech Stack

- **FastAPI**: Modern, fast web framework for building APIs
- **PostgreSQL 18**: Relational database
- **Docker & Docker Compose**: Containerization
- **pgAdmin 4**: Database management interface
- **Pydantic**: Data validation
- **Uvicorn**: ASGI server



## Prerequisites

- Docker Desktop installed ([Download here](https://www.docker.com/products/docker-desktop))
- Docker Compose (included with Docker Desktop)
- Git (optional, for cloning)

## Quick Start

### 1. Clone or Download the Project

```bash
git clone https://github.com/techy-Nik/assignment-9.git
cd assigment-9
```

### 2. Build and Run with Docker Compose

```bash
docker-compose up --build
```

This command will:
- Build the FastAPI application container
- Start PostgreSQL database
- Start pgAdmin interface
- Set up networking between containers

### 3. Access the Services

- **FastAPI Application**: http://localhost:8000
- **API Documentation (Swagger)**: http://localhost:8000/docs
- **Alternative API Docs (ReDoc)**: http://localhost:8000/redoc
- **pgAdmin**: http://localhost:5050

## API Endpoints

### Base URL
```
http://localhost:8000
```

### Available Operations

#### 1. Addition
```http
POST /add
Content-Type: application/json

{
  "a": 10,
  "b": 5
}
```
**Response:**
```json
{
  "result": 15
}
```

#### 2. Subtraction
```http
POST /subtract
Content-Type: application/json

{
  "a": 10,
  "b": 5
}
```
**Response:**
```json
{
  "result": 5
}
```

#### 3. Multiplication
```http
POST /multiply
Content-Type: application/json

{
  "a": 10,
  "b": 5
}
```
**Response:**
```json
{
  "result": 50
}
```

#### 4. Division
```http
POST /divide
Content-Type: application/json

{
  "a": 10,
  "b": 5
}
```
**Response:**
```json
{
  "result": 2.0
}
```

### Error Handling

**Division by Zero:**
```json
{
  "error": "Cannot divide by zero!"
}
```

**Invalid Input:**
```json
{
  "error": "a: value is not a valid float"
}
```

## pgAdmin Configuration

### First Time Setup

1. Open http://localhost:5050
2. Login with credentials:
   - **Email**: `admin@example.com`
   - **Password**: `admin`

3. Add a new server:
   - Right-click "Servers" → "Register" → "Server"
   - **General Tab**:
     - Name: `FastAPI DB`
   - **Connection Tab**:
     - Host: `db` (container name)
     - Port: `5432`
     - Database: `fastapi_db`
     - Username: `postgres`
     - Password: `postgres`

## Development

### Running in Development Mode

The application runs with hot reload enabled by default. Any changes to the code will automatically restart the server.

### Viewing Logs

```bash
# All services
docker-compose logs -f

# Specific service
docker-compose logs -f web
docker-compose logs -f db
docker-compose logs -f pgadmin
```

### Stopping the Services

```bash
# Stop containers
docker-compose down

# Stop and remove volumes (⚠️ deletes database data)
docker-compose down -v
```

### Rebuilding After Changes

```bash
docker-compose up --build
```

## Environment Variables

### Web Service (FastAPI)
- `PYTHONDONTWRITEBYTECODE=1`: Prevents Python from writing .pyc files
- `PYTHONUNBUFFERED=1`: Forces stdout/stderr to be unbuffered
- `DATABASE_URL`: PostgreSQL connection string

### Database Service (PostgreSQL)
- `POSTGRES_USER`: Database username
- `POSTGRES_PASSWORD`: Database password
- `POSTGRES_DB`: Database name

### pgAdmin Service
- `PGADMIN_DEFAULT_EMAIL`: pgAdmin login email
- `PGADMIN_DEFAULT_PASSWORD`: pgAdmin login password

## Docker Volumes

The project uses persistent volumes to store data:

- `postgres_data`: PostgreSQL database files
- `pgadmin_data`: pgAdmin configuration and settings

## Network

All services communicate through a custom bridge network called `app-network`, allowing them to reference each other by service name.

## Testing the API

### Using curl

```bash
# Addition
curl -X POST "http://localhost:8000/add" \
  -H "Content-Type: application/json" \
  -d '{"a": 10, "b": 5}'

# Division
curl -X POST "http://localhost:8000/divide" \
  -H "Content-Type: application/json" \
  -d '{"a": 10, "b": 2}'
```

### Using Python

```python
import requests

response = requests.post(
    "http://localhost:8000/add",
    json={"a": 10, "b": 5}
)
print(response.json())  # {"result": 15}
```

## Troubleshooting

### Port Already in Use

If you get a port conflict error:

```bash
# Change the port mapping in docker-compose.yml
# For example, change "8000:8000" to "8001:8000"
```

### Database Connection Issues

```bash
# Check if database is healthy
docker-compose ps

# Restart the database service
docker-compose restart db
```

### Permission Errors

```bash
# On Linux/Mac, you may need to adjust permissions
sudo chown -R $USER:$USER .
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- FastAPI documentation: https://fastapi.tiangolo.com/
- Docker documentation: https://docs.docker.com/
- PostgreSQL documentation: https://www.postgresql.org/docs/

