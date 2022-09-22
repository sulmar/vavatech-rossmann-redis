
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

## Komendy

### Połączenie

| Komenda  | Opis   |
|---|---|
| **PING** [message] | Ping do serwera  |
| **ECHO** message | Wyświetlenie komunikatu |
| **AUTH** [username] password | Logowanie do serwera  |
| **SELECT** index | Wybór bazy danych |
| **SWAPDB** index index | Zamiana baz danych |
| **QUIT** | Zamknięcie połączenia |

### Diagnostyka
| Komenda  | Opis   |
|---|---|
| **INFO** [section] | Wyświetlenie informacji |
| **MONITOR** | Włączenie śledzenia |
| **OBJECT FREQ**  key | Pobranie częstotliwości dostępu do klucza |
| **MEMORY USAGE** key | Pobranie zajętości pamięci przez klucz |
 

### Konfiguracja
| Komenda  | Opis   |
|---|---|
| **CONFIG GET** parameter | Pobranie wartości parametru konfiguracji |
| **CONFIG SET** parameter value | Ustawienie wartości parametru konfiguracji |
| **CONFIG REWRITE** | Zapisanie konfiguracji w pamięci |


### Podstawowe

| Komenda  | Opis   |
|---|---|
| **RENAME** key newkey | Zmiana nazwy klucza |
| **MOVE** key db | Przesunięcie klucza do innej bazy danych |
| **EXISTS** key  | Sprawdzenie czy klucz istnieje |
| **DEL** key  | Usunięcie klucza  |
| **RANDOMKEY** | Pobranie losowego klucza |
| **DUMP** key  | Pobranie serializowanej wartości klucza  |
| **TYPE** key  | Pobranie typu klucza |
| **EXPIRE** key seconds  | Ustawienie czasu wygaśnięcia klucza |
| **EXPIREAT** key timestamp  | Ustawienie daty wygaśnięcia klucza |
| **TTL** key | Pobranie pozostałego czasu do wygaśnięcia klucza w sekundach |
| **PTTL** key | Pobranie pozostałego czasu do wygaśnięcia klucza w milisekundach 
| **PERSIST** key | Wyłączenie wygasania klucza |
| **KEYS** pattern | Pobranie wszystkich nazw kluczy według wzorca |
| **SCAN** cursor [MATCH pattern] [COUNT count] [TYPE type] | Pobranie określonej ilości nazw kluczy na podstawie wzorca lub typu |

### Strings

| Komenda  | Opis   |
|---|---|
| **SET** key value | Ustawienie wartości klucza  |
| **GET** key  | Pobranie wartości klucza |
| **MSET** key1 value1 [key2 value2] | Ustawienie wielu wartości kluczy  |
| **MGET** key1 [key2] | Pobranie wielu wartości kluczy  |
| **GETRANGE** key start end  | Pobranie fragmentu wartości klucza |
| **APPEND** key value | Dołączenie wartości do wartości klucza |
| **STRLEN** key | Pobranie długości wartości klucza  |
| **INCR** key | Zwiększenie wartości klucza o 1  |
| **INCRBY** key increment | Zwiększenie wartości klucza o podaną wartość |
| **INCRBYFLOAT** key increment | Zwiększenie wartości klucza o podaną wartość ułamkową |
| **DECR** key | Zmniejszenie wartości klucza o 1 |
| **DECRBY** key increment | Zmniejsze wartości klucza o podaną wartość |

### Hashes

| Komenda  | Opis   |
|---|---|
| **HSET** key field value | Ustawienie wartości pola danego klucza  |
| **HMSET** key field value | Ustawienie wielu wartości pola danego klucza  |
| **HGET** key field  | Pobranie wartości pola danego klucza |
| **HMGET** key field [field ...] | Pobranie wartości wybranych pól danego klucza |
| **HGETALL** key  | Pobranie wszystkich pól danego klucza |
| **HKEYS** key  | Pobranie kluczy danego klucza |
| **HVALS** key  | Pobranie wartości danego klucza |
| **HINCRBY** key field increment  | Inkrementacja wartości pola |
| **HEXISTS** key field | Sprawdzenie czy pole istnieje w danym kluczu |
| **HDEL** key field | Usunięcie pola danego klucza |
| **HSCAN** key cursor | Pobranie pól i wartości kluczy |
| **HSTRLEN** key field | Pobranie długości wartości pola |

### Sets

| Komenda  | Opis   |
|---|---|
| **SADD** key member [member] | Dodanie elementu do zbioru  |
| **SMEMBERS** key | Pobranie elementów ze zbioru |
| **SCARD** key | Pobranie ilości elementów w zbiorze |
| **SMOVE** source destination member | Przesunięcie elementu pomiędzy zbiorami |
| **SISMEMBER** key member | Sprawdzenie czy wartość jest elementem zbioru |
| **SREM** key member | Usunięcie elementu ze zbioru |
| **SPOP** key [count] | Usunięcie i pobranie pojedyńczego lub większej ilości losowych elementów ze zbioru |
| **SRANDMEMBER** key [count] | Pobranie pojedyńczego lub większej ilości losowych elementów ze zbioru |
| **SUNION** key [key] | Suma zbiorów |
| **SUNIONSTORE** destination key [key] | Suma zbiorów i zapisanie ich pod nowym kluczem |
| **SINTER** key [key] | Część wspólna zbiorów |
| **SINTERSTORE** desitination key [key] | Część wspólna zbiorów i zapisanie ich pod nowym kluczem |
| **SDIFF** key [key] | Różnica zbiorów |
| **SDIFFSTORE** desitination key [key] | Różnica zbiorów i zapisanie ich pod nowym kluczem |

### Sorted Sets

| Komenda  | Opis   |
|---|---|
| **ZADD** key score member | Dodanie elementu do zbioru  |
| **ZREM** key member | Usunięcie elementu ze zbioru  |
| **ZINCRBY** key increment member | Zwiększego wartości klucza w zbiorze  |
| **ZSCORE** key member | Pobranie wyniku elementu ze zbioru  |
| **ZSCAN** key cursor | Pobranie elementów ze zbioru |
| **ZCARD** key | Pobranie ilości elementów ze zbioru |
| **ZCOUNT** key min max | Pobranie ilości elementów ze zbioru, których wynik jest pomiędzy wartościami min i max |
| **ZRANK** key member | Pobranie rankingu na podstawie wyniku od najniższej wartości |
| **ZREVRANK** key member | Pobranie rankingu na podstawie wyniku od najwyższej wartości |
| **ZRANGEBYSCORE** key min max [withscores] | Pobranie elementów w zakresie rankingu |

### Lists

| Komenda  | Opis   |
|---|---|
| **LPUSH** key value [value] | Dodanie elementu do listy od lewej strony (początek) |
| **RPUSH** key value [value] | Dodanie elementu do listy od prawej strony (koniec) |
| **LSET** key index element | Ustawienie wartości elementu na liście na podstawieniu pozycji |
| **LINSERT** key BEFORE|AFTER pivot element | Wstawienie elementu do listy przed lub po wskazanym elementem na liście |
| **LRANGE** key start stop  | Pobranie fragmentu elementów listy |
| **LINDEX** key index | Pobranie elementu z listu na podstawie pozycji |
| **LREM** key count value  | Usunięcie określonej ilości elementów z listy począwszy od podanej wartości |
| **LPOP** key  | Pobranie i usunięcie elementu z listy od lewej strony (początek) |
| **RPOP** key  | Pobranie i usunięcie elementu z listy od prawej strony (koniec)|
| **RPOPLPUSH** key  | Przeniesienie elementu pomiędzy listami |
| **LMOVE** source destination LEFT|RIGHT LEFT|RIGHT | Przesunięcie elementu pomiędzy listami |
| **LLEN** key  | Pobranie ilości elementów listy |
| **LTRIM** key start stop | Wycina fragment listy |


### Geo

| Komenda  | Opis   |
|---|---|
| **GEOADD** key longitude latitude member | Dodanie elementu o podanej pozycji do zbioru |
| **GEOPOS** key member  | Pobranie pozycji elementu |
| **GEOHASH** key member  | Pobranie pozycji elementu w formacie GeoHash |
| **GEODIST** key member1 member2 [unit] ]| Obliczenie odległości pomiędzy elementami |
| **GEOSEARCH** key ...   | Wyszukiwanie elementów w określonym obszarze |
| **GEOSEARCHSTORE** key ...   | Wyszukiwanie elementów w określonym obszarze i zapisanie wyników do osobnego zbioru |
| **GEORADIUS** key longitude latitude radius   | Wyszukiwanie elementów w określonym promieniu |
| **GEORADIUSBYMEMBER** key member radius   | Wyszukiwanie elementów w określonym promieniu od podanego elementu |


### Bitmaps

| Komenda  | Opis   |
|---|---|
| **SETBIT** key offset value | Ustawienie bitu |
| **GETBIT** key offset | Pobranie bitu |
| **BITOP** operation destkey key | Wykonanie operacji bitowej na kluczach |
| **BITCOUNT** key [start end] | Obliczenie ilości ustawionych bitów na 1 |
| **BITPOS** key [start] [end] | Pobranie pozycji bitu ustawionego na 1 |


### Transakcje

| Komenda  | Opis   |
|---|---|
| **MULTI**  | Rozpoczęcie bloku transakcji |
| **EXEC** | Wykonanie wszystkich komend |
| **DISCARD** | Porzucenie wszystkich komend |
| **WATCH** key [key] | Śledzenie zmian klucza |
| **UNWATCH** | Zwolnienie śledzenie zmian klucza |


### Pub/Sub

| Komenda  | Opis   |
|---|---|
| **SUBSCRIBE** channel [channel ...] | Nasłuchiwanie komunikatów publikowanych do podanego kanału |
| **PSUBSCRIBE** pattern [pattern] | Nasłuchiwanie komunikatów według wzorca |
| **PUBLISH** channel message | Wysłanie komunikatu na kanał |
| **UNSUBSCRIBE** [channel] | Zatrzymanie nasłuchiwania komunikatów |

### Stream

| Komenda  | Opis   |
|---|---|
| **XADD** key ID field string [field string...] | Pisanie do strumienia |
| **XREAD** [count] STREAMS key ID | Czytanie ze strumienia |
| **XLEN** key | Pobranie długości strumienia |

### Cluster
| Komenda  | Opis   |
|---|---|
| **CLUSTER SLOTS** | Wyświetlenie informacji o slotach  (przestarzałe)|
| **CLUSTER SHARDS** | Wyświetlenie informacji o slotach |
| **CLUSTER INFO** | Wyświetlenie informacji o działaniu klastra |
| **CLUSTER KEYSLOT** key | Obliczenie funkcji hash dla klucza |


## Transakcje

### Zatwierdzenie transakcji

Scenariusz: _John wykonuje przelew dla Jeny_

~~~
MSET john:debet 100 jeny:debet 100
MULTI
DECRBY john:debet 40
INCRBY jeny:debet 40
EXEC 
~~~

Polecenie **MULTI** powoduje, że wszystkie operacje od tego momentu są kolejkowane. Dopiero operacja **EXEC** je faktycznie wykonuje.

### Wycofanie transakcji

Scenariusz: _Jeny zwraca pieniądze Johnemu, ale rozmyśla się._

~~~
MSET jeny:debet 100 john:debet 100 
MULTI
DECRBY john:debet 40
INCRBY jeny:debet 40
DISCARD 
~~~

Polecenie **MULTI** powoduje, że wszystkie operacje od tego momentu są kolejkowane. Dopiero operacja **DISCARD** czyści kolejkę operacji.

### Śledzenie zmian klucza

Scenariusz: _John wykonuje przelew dla Jeny_ ale w międzyczasie inny użytkownik modyfikuje stan konta Johna

1. Użytkownik nr 1 zaczyna wprowadzać zmiany:
~~~
MULTI
WATCH john:debet
DECRBY john:debet 40
INCRBY jeny:debet 40
~~~

2. Użytkownik nr 2 modyfikuje w międzyczasie wartość klucza:
~~~
INCRBY john:debet 50
~~~

3. Użytkownik nr 1 zatwierdza transakcję
~~~
EXEC 
~~~

W przypadku gdy w ktoś w międzyczasie zmienił zawartość obserwowanego klucza, transakcja zostaje wycofana.



## Cluster

### Linux


1. Utwórz plik konfiguracyjny
~~~ bash
vim redis.conf        
~~~

_redis.conf_
~~~ 
port 7000
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
appendonly yes
~~~


2. Utwórz podkatalogi
~~~ bash
mkdir 7000 7001 7002 7003 7004 7005 7006 7007
~~~

3. Skopiuj pliki konfiguracyjny do poszczególnych katalogów
~~~ bash
cp redis.conf 7000/redis.conf                                   
...
cp redis.conf 7007/redis.conf                                   
~~~
                         
3. Zmień porty w poszczególnych plikach redis.conf
~~~ bash
vim 7000/redis.conf
...
vim 7007/redis.conf
~~~

4. Uruchom serwery
~~~ bash
cd 7000
redis-server ./redis.conf  
...
cd 7007
redis-server ./redis.conf  
~~~

5. Utwórz klaster
~~~ bash
redis-cli --cluster create 127.0.0.1:7000 127.0.0.1:7001 \
127.0.0.1:7002 127.0.0.1:7003 127.0.0.1:7004 127.0.0.1:7005 127.0.0.1:7006 127.0.0.1:7007 --cluster-replicas 1
~~~

6. Połącz się do jednego z wezłów master
~~~ bash
redis-cli -p 7000 -c   
~~~

7. Dodaj klucze
~~~ 
SET foo Hello
SET boo World
~~~

Możesz zauważyć, że klucze zapisywane są w różnych slotach.

- informacje o slotach (przestarzałe): 
~~~
CLUSTER SLOTS 
~~~

- informacje o slotach (od wersji 7.0)
~~~
CLUSTER SHARDS 
~~~

- informacje o działaniu klastra
~~~
CLUSTER INFO
~~~

- Obliczenie funkcji hash dla klucza o podanej nazwie
~~~
CLUSTER KEYSLOT foo
~~~

(klucz nie musi istnieć)

### Problemy (błąd CROSSSLOT)



#### Scenariusz 1

- Przykład
~~~
SADD user:512:following user:123 user:321 user:132
CLUSTER KEYSLOT user:512:following 
SADD user:512:followed_by user:123 user:132 
CLUSTER KEYSLOT user:512:followed_by
~~~

- Problem
~~~
SINTER user:512:following user:512:followed_by
~~~
_(error) CROSSSLOT Keys in request don't hash to the same slot_

- Przyczyna
Klucze znajdują się w innych slotach.

- Rozwiązanie
~~~
SADD user:{512}:following user:123 user:321 user:132
CLUSTER KEYSLOT user:{512}:following 
~~~

{...} - oznacza, że tylko dla tej części klucza ma być obliczony hash, dzięki temu pozostała część nazwy klucza nie ma znaczenia

~~~
SADD user:{512}:followed_by user:123 user:132
CLUSTER KEYSLOT user:{512}:followed_by
~~~

- Sprawdzenie
~~~
SINTER user:{512}:following user:{512}:followed_by
~~~ 

#### Scenariusz 2

- Przykład
~~~ 
SET foo Hello
SET boo World
~~~ 

- Problem
~~~
MGET foo boo
~~~

_(error) CROSSSLOT Keys in request don't hash to the same slot_

- Rozwiązanie
~~~
CLUSTER KEYSLOT foo
CLUSTER KEYSLOT boo
CLUSTER KEYSLOT f{oo}
CLUSTER KEYSLOT b{oo}
SET f{oo} Hello
SET b{oo} World
MGET f{oo} b{oo}
~~~
