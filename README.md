# LogTo

Docker image of LogTo with Telegram connector

## Example

Docker Compose:

```yaml
services:
  logto:
    image: ghcr.io/b4ck5p4c3/logto:<version>
    entrypoint: ["sh", "-c", "npm run cli db seed -- --swe && npm start"]
    restart: unless-stopped
    ports:
      - 3001:3001
      - 3002:3002
    environment:
      - TRUST_PROXY_HEADER=1
      - DB_URL=postgres://username:password@hostname:port/database
      - ENDPOINT=https://sso.domain.tld
      - ADMIN_ENDPOINT=https://sso-admin.domain.tld
  postgres:
    image: postgres:14-alpine
    user: postgres
    environment:
      POSTGRES_USER: username
      POSTGRES_PASSWORD: password
    healthcheck:
      test: ["CMD-SHELL", "pg_isready"]
      interval: 10s
      timeout: 5s
      retries: 5
```