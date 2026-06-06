# Sprawozdanie lab 13

# Michał Ziętek

### Budowanie i start kontenerów
```bash
docker compose up -d --build
```
Wynik:
```
[+] up 39/39
 ✔ Image nginx:1.25             Pulled                                 12.9s
 ✔ Image phpmyadmin:5.2         Pulled                                 19.7s
 ✔ Image lab13-php              Built                                  44.8s
 ✔ Network lab13_backend        Created                                0.1s
 ✔ Network lab13_frontend       Created                                0.1s
 ✔ Container lab13-mysql-1      Created                                0.3s
 ✔ Container lab13-phpmyadmin-1 Created                                0.3s
 ✔ Container lab13-php-1        Created                                0.2s
 ✔ Container lab13-nginx-1      Created                                0.1s
```

### Sprawdzenie statusu kontenerów
```bash
docker compose ps
```
Wynik:
```
NAME                 IMAGE            COMMAND                  SERVICE      CREATED          STATUS          PORTS
lab13-mysql-1        mysql:8.0        "docker-entrypoint.s…"   mysql        45 seconds ago   Up 44 seconds   3306/tcp, 33060/tcp
lab13-nginx-1        nginx:1.25       "/docker-entrypoint.…"   nginx        45 seconds ago   Up 43 seconds   0.0.0.0:4001->80/tcp, [::]:4001->80/tcp
lab13-php-1          lab13-php        "docker-php-entrypoi…"   php          45 seconds ago   Up 44 seconds   9000/tcp
lab13-phpmyadmin-1   phpmyadmin:5.2   "/docker-entrypoint.…"   phpmyadmin   45 seconds ago   Up 44 seconds   0.0.0.0:6001->80/tcp, [::]:6001->80/tcp
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

### Test strony PHP (LEMP)
```bash
http://localhost:4001
```

### Test phpMyAdmin + testowa baza
```bash
http://localhost:6001  
```
Dane logowania:  
Login: root  
Hasło: rootpassword
