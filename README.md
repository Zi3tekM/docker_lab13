# Sprawozdanie lab 13

# Michał Ziętek

### Budowanie i start kontenerów
```bash
docker compose up -d --build
```

### Sprawdzenie statusu kontenerów
```bash
docker compose ps
```

### Sprawdzenie logów
```bash
docker compose logs
```

### Sprawdzenie sieci
```bash
docker network ls
```
Wynik:

```bash
315b6d070d11   lab13_backend             bridge    local
425fc88e8a37   lab13_frontend            bridge    local
```

### Sprawdzenie konkretnych sieci
```bash
docker network inspect lab13_backend
```
Wynik:
```json
[
    {
        "Name": "lab13_backend",
        "Driver": "bridge",
        "Containers": {
            "...": { "Name": "lab13-mysql-1",      "IPv4Address": "172.20.0.3/16" },
            "...": { "Name": "lab13-php-1",         "IPv4Address": "172.20.0.4/16" },
            "...": { "Name": "lab13-nginx-1",       "IPv4Address": "172.20.0.5/16" },
            "...": { "Name": "lab13-phpmyadmin-1",  "IPv4Address": "172.20.0.2/16" }
        }
    }
]
```

```bash
docker network inspect lab13_frontend
```
Wynik:
```json
[
    {
        "Name": "lab13_frontend",
        "Driver": "bridge",
        "Containers": {
            "...": { "Name": "lab13-nginx-1", "IPv4Address": "172.21.0.2/16" }
        }
    }
]
```
