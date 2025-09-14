# homelab / platform

This is my playground for messing around with a "platform" stack.  
Think: reverse proxy, DBs, cache, admin tools, and a baby API.  

It’s not production-ready. It’s not meant to be pretty. It’s just me  
trying to glue stuff together with Docker and see what happens.  

---

## What's inside

- **Traefik**  
  Reverse proxy & entrypoint. Auto-discovers containers and routes them.  
  Comes with a dashboard at `:8080` (dev only, don’t expose this raw to the internet).

- **Whoami**  
  A dumb little container that just prints request info. Used to prove routing works.  

- **Postgres**  
  Main database. Data stored in a Docker volume (`pgdata/`).  

- **Redis**  
  Queue/cache. Persists with appendonly log. Volume: `redisdata/`.  

- **Adminer**  
  Super simple DB UI for Postgres, reachable at `/db`.  

- **RedisInsight**  
  GUI for poking at Redis, reachable at `/redis`.  

- **API (./api)**  
  My toy backend service (currently FastAPI + Alembic).  
  Handles DB migrations and serves stuff under `/api`.  

---

## File structure
```
platform/
├── api/ # the "app" container
│ ├── alembic.ini # Alembic config
│ ├── app.py # FastAPI toy app
│ ├── Dockerfile # builds the api service
│ └── migrations/ # Alembic migration folder
├── docker-compose.yml # main stack definition
├── requirements.txt # Python deps for the api
└── README.md # this file...
```


## Running it

1. Copy `.env.example` → `.env` and fill in secrets (DB user/pass, etc.).
2. maybe it works, give it a try:
   `docker compose up -d --build`





