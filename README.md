# Sprawozdanie lab 13

# Michał Ziętek

### Budowanie i start kontenerów
```bash
docker compose up -d --build
```
Wynik:
```
[+] Building 12.3s (7/7) FINISHED
 => [php internal] load build definition from Dockerfile
 => [php] FROM docker.io/library/php:8.2-fpm
 => [php] RUN docker-php-ext-install mysqli pdo pdo_mysql
[+] Running 5/5
 ✔ Network lab13_frontend        Created
 ✔ Network lab13_backend         Created
 ✔ Container lab13-mysql-1       Started
 ✔ Container lab13-php-1         Started
 ✔ Container lab13-nginx-1       Started
 ✔ Container lab13-phpmyadmin-1  Started
```

### Sprawdzenie statusu kontenerów
```bash
docker compose ps
```
Wynik:
```
NAME                    IMAGE          STATUS          PORTS
lab13-mysql-1           mysql:8.0      Up              3306/tcp
lab13-nginx-1           nginx:1.25     Up              0.0.0.0:4001->80/tcp
lab13-php-1             lab13-php      Up              9000/tcp
lab13-phpmyadmin-1      phpmyadmin:5.2 Up              0.0.0.0:6001->80/tcp
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
