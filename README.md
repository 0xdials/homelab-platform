# homelab / platform

a wretched little platform stack, might build something using it later.
basically: a reverse proxy, some dbs, a cache, random admin toys,
and a baby api duct-taped on top.

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
2. maybe it works maybe it doesnt i dont know im pretty tired, give it a try:
   `docker compose up -d --build`





