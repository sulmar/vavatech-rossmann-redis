
# REDIS

## Instalacja

### Linux

- Instalacja serwera Redis
~~~ bash
sudo apt-get install redis-server
~~~

~~~ bash
- Sprawdzenie statusu 
sudo systemctl status redis
~~~

- Podłączenie
~~~ bash
sudo redis-cli
~~~

### Docker
- Pobranie obrazu
~~~
docker pull redis:latest
~~~

- Uruchomienie kontenera
~~~
docker run --name my-redis -d -p 6379:6379 redis
~~~

Uruchomienie trybu interaktywnego
~~~
docker exec -it my-redis redis-cli
~~~

- Uruchomienie kontenera
~~~
docker start my-redis 
~~~

- Zatrzymanie kontenera
~~~
docker stop my-redis
~~~

- Usunięcie kontenera
~~~
docker rm my-redis
~~~

### Docker Compose
1. Utwórz plik _docker-compose.yaml_
~~~ yaml
version: '3'
services:
  redis:
    image: redis:latest
    environment:
      - ALLOW_EMPTY_PASSWORD=yes
    restart: always
    ports:
      - '6379:6379'
    command: redis-server --loglevel warning
    volumes:
      - cache:/data
volumes:
  cache:
    driver: local
~~~

2. Uruchom
~~~ bash
docker-compose up -d
~~~

3. Podłącz
~~~ bash
docker exec -it redis-tutorial-redis-1 redis-cli
~~~

4. Zatrzymaj
~~~ bash
docker-compose down
~~~
