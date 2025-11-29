# Backend Environment Variables Setup

This backend uses environment variables for configuration. Follow these steps to set up your environment:

## Setup Instructions

1. **Create a `.env` file in the `backend` directory:**
   ```bash
   cp .env.example .env
   ```

2. **Edit `.env` file with your configuration:**
   ```env
   # Database Configuration
   DATABASE_URL=postgresql://user:password@localhost:5432/pair_programming
   
   # Server Configuration
   HOST=0.0.0.0
   PORT=8000
   RELOAD=true
   
   # CORS Configuration
   CORS_ORIGINS=http://localhost:3000,http://localhost:3001,http://127.0.0.1:3000,http://127.0.0.1:3001
   ```

## Environment Variables

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `DATABASE_URL` | PostgreSQL connection string | None | ✅ Yes |
| `HOST` | Server host address | `0.0.0.0` | No |
| `PORT` | Server port | `8000` | No |
| `RELOAD` | Enable auto-reload on code changes | `true` | No |
| `CORS_ORIGINS` | Comma-separated list of allowed CORS origins | `http://localhost:3000,http://localhost:3001,http://127.0.0.1:3000,http://127.0.0.1:3001` | No |

## Database URL Format

The `DATABASE_URL` should follow this format:
```
postgresql://username:password@host:port/database
```

### Examples:

**Local PostgreSQL:**
```env
DATABASE_URL=postgresql://postgres:password@localhost:5432/pair_programming
```

**Remote PostgreSQL (e.g., AWS RDS, Heroku):**
```env
DATABASE_URL=postgresql://user:password@your-db-host.com:5432/your_database
```

**With SSL:**
```env
DATABASE_URL=postgresql://user:password@host:5432/db?sslmode=require
```

## For Production

When deploying to production, update your `.env` file:

```env
# Production example
DATABASE_URL=postgresql://prod_user:secure_password@prod-db-host:5432/prod_database
HOST=0.0.0.0
PORT=8000
RELOAD=false
CORS_ORIGINS=https://yourdomain.com,https://www.yourdomain.com
```

## Important Notes

- **Never commit `.env` file**: It's already in `.gitignore` to prevent committing sensitive data
- **Restart required**: After changing `.env` file, restart the server
- **Database URL is required**: The application will fail to start if `DATABASE_URL` is not set
- **CORS Origins**: For production, only include your actual frontend domain(s)

## Troubleshooting

### Database Connection Error
- Verify your `DATABASE_URL` is correct
- Ensure PostgreSQL is running
- Check database credentials
- Verify network connectivity to database host

### CORS Errors
- Add your frontend URL to `CORS_ORIGINS`
- Ensure URLs are comma-separated without spaces (or with spaces that will be trimmed)
- For production, use `https://` URLs

### Port Already in Use
- Change `PORT` in `.env` to a different port
- Or stop the process using port 8000

