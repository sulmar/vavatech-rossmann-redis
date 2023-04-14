
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
| **DBSIZE** | Pobranie ilości kluczy w aktualnej bazie danych |
| **CLIENT LIST** | Pobieranie listę wszystkich połączeń |
| **CLIENT KILL** | Zamyka wybrane połączenie na podst. IP, ID, lub nazwie użytkownika |
| **CLIENT SETNAME** connection-name | Ustawia nazwę połączenia |
| **CLIENT GETNAME** | Pobranie nazwy połączenia |
 
 

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


### Skrypty
| Komenda  | Opis   |
|---|---|
| **EVAL** script numkeys key [key ...] arg [arg ...] | Uruchomienie skryptu w języku Lua po stronie serwera |
| **EVALSHA** sha1 numkeys key [key ...] arg [arg ...] | Uruchomienie wskazanego skryptu w pamięci po stronie serwera |
| **SCRIPT LOAD** script | Załadowanie skryptu do pamięci |
| **SCRIPT EXISTS** sha1 | Sprawdzenie czy skrypt jest w pamięci |
| **SCRIPT KILL** | Zatrzymanie wykonywania aktualnie uruchomionego skryptu |
| **SCRIPT FLUSH** | Usunięcie wszystkich skryptów z pamięci |
| **SCRIPT DEBUG**  | Uruchomienie trybu śledzenia uruchamianych skryptów |


## Praca



### Podstawy
- Uruchomienie klienta
~~~
> redis-cli
~~~

- Sprawdzenie czy serwer działa
~~~
PING
~~~

- Wyświetlenie komunikatu
~~~ 
ECHO 'Hello World'
~~~

- Wyczyszczenie konsoli
~~~
CLEAR
~~~

- Wyjście z konsoli
~~~
QUIT
~~~

- Włączenie śledzenia
~~~
MONITOR
~~~

- Wyświetlenie informacji o serwerze
~~~
INFO Server
~~~

### Strings

#### Opis
Klucz może przechowywać tylko jedną wartość.

- do 2^32 bitów (512MB) na każdy klucz
- zastosowania
    - czysty tekst (np. przechowywanie strony www)
    - wartości numeryczne (np. ilość zgromadzonych punktów)    
    - surowe bity/flagi (dzienna aktywność użytkowników)
    - zawartość binarnych plików (PDF, obrazy)
    - obiekty json

#### Podstawowe operacje

- Ustawienie wartości klucza (tekst)
~~~
SET message "Hello World"
GET message
~~~

- Nadpisanie wartości klucza
~~~
SET message "Hello Redis"
GET message
~~~

- Ustawienie wartości klucza tylko jeśli wcześniej nie istniał
~~~
SETNX message "Hello Redis"
SETNX message "Hello World"
~~~

- Ustawienie wartości klucza tylko jeśli wcześniej nie istniał (za pomocą parametru)
~~~
SET message "Hello Redis" NX
~~~

- Ustawienie wartości istniejącego klucza. Nie tworzy nowego klucza.
~~~
SET greetings "Hello World" XX
~~~


- Sprawdzenie czy klucz istnieje
~~~
EXISTS message
~~~

- Usunięcie klucza
~~~
DEL message
~~~

- Usunięcie klucza bez blokowania
~~~
UNLINK message
~~~
Komenda odpina klucz z przestrzeni roboczej. Faktyczne usunięcie nastąpi później asynchronicznie (w osobnym wątku).

- Ustawienie wartości klucza (liczba całkowita)
~~~
SET points 100
GET points
~~~

- Inkrementacja wartości
~~~
INCR points
GET points
~~~

- Dekrementacja wartości
~~~
DECR points
GET points
~~~

- Inkrementacja wartości o podaną wartość
~~~
INCRBY points 10
GET points
~~~

- Dekrementacja wartości o podaną wartość
~~~
DECRBY points 10
GET points
~~~

- Ustawienie wartości klucza (liczba rzeczywista)
~~~
SET temp 21.45
GET temp
~~~

- Inkrementacja liczby rzeczywistej
~~~
SET temp 21.45
INCRBYFLOAT room1:temp 0.5
~~~

- Dekrementacja liczby rzeczywistej
~~~
INCRBYFLOAT room1:temp -0.25
~~~

- Konwencja nazewnictwa kluczy (przestrzeń nazw)
~~~
SET server:name server1
GET server:name
SET server:port 5000
GET server:port
~~~

- Ustawienie wartości wielu kluczom
~~~ 
MSET key1 "Hello" key2 "World"
~~~

- Pobranie wartości wielu kluczy
~~~
MGET key1 key2
~~~

- Dodanie wartości do klucza
~~~
SET message "Hello, "
APPEND message " World!"
~~~

- Pobranie zakresu wartości
~~~
GETRANGE message 0 4
GETRANGE message 6 10
~~~

- Zmiana nazwy klucza
~~~
RENAME message greeting
~~~

#### Klucze tymczasowe

- Ustawienie wartości klucza tymczasowego
~~~
SET token "ABC123" EX 60
TTL token
~~~

- Ustawienie wartości klucza tymczasowego (składnia skrócona)
~~~
SETEX token 60 "ABC123"
TTL token
~~~

- Nadpisanie wartości klucza tymczasowego z zachowaniem czasu
~~~
SET token "XYZ321" KEEPTTL
~~~

Bez parametru _KEEPTTL_ klucz zostałby nadpisany i ustawiony czas odliczałbym od początku.


- Ustawienie klucza tymczasowego, który wygaśnie o dokładnie podanej dacie i godzinie.
~~~
SET ticket "redis"
EXPIREAT ticket 1573041600
TTL ticket
~~~
Czas podawany jest w formacie Unix timestamp (ilość sekund od 1970-01-01)
Wskazówka: skorzystaj z konwertera https://www.epochconverter.com/


- Ustawienie wygaśnięcia klucza
~~~
SET greeting "Hello World"
EXPIRE greeting 60
TTL greeting
~~~

- Utrwalenie tymczasowego klucza
~~~
PERSIST greeting
TTL greeting
~~~

### Hash

#### Opis
Tablice asocjacyjne. Klucz może przechowywać wiele wartości w poszczególnych polach.

#### Podstawowe operacje

Jeśli chcesz zmodyfikować cały obiekt zwykły string wystarczy:
~~~
SET user:marcin { 'name':'Marcin Sulecki', 'email': 'marcin.sulecki@gmail.com'}
~~~

Natomiast w przypadku, gdy chcesz mieć dostęp do pojedynczych pól lepszym rozwiązaniem będą tablice asosjacyjne

- Dodanie wartości
~~~
HSET user1 firstname John
HSET user1 lastname Smith
HSET user1 email john.smith@domain.com
HSET user1 points 10
~~~

- Dodanie wielu wartości
~~~
HMSET user2 firstname "Bob" lastname "Smith" email bob@domain.com phone 555-123-123
~~~

- Pobranie wybranego pola
~~~
HGET user1 firstname
HGET user1 lastname
~~~

- Pobranie wartości wielu pól
~~~
HMGET user1 firstname lastname
~~~

- Pobranie wszystkich pól
~~~
HKEYS user1
~~~

- Pobranie wszystkich wartości
~~~
HVALS user1
~~~

- Pobranie wszystkich pól i wartości
~~~
HGETALL user1
~~~

- Inkrementacja wybranego pola
~~~
HINCRBY user1 points 5
~~~

- Usunięcie wybranego pola
~~~
HDEL user1 phone
~~~


### Lists

#### Opis
- Do 2^32 elementów w każdym kluczu
- zastosowania
    - kolejka
    - stos    
    - ostatnie wiadomości

#### Podstawowe operacje
- Wstawienie elementów na początek listy
~~~
LPUSH people "John"
LPUSH people "Tom"
LPUSH people "Jenny"
~~~

- Pobranie wszystkich elementów
~~~
 LRANGE people 0 -1
~~~


- Pobranie zakresu elementów
~~~
 LRANGE people 1 2
~~~

- Pobranie elementu z listy o podanym indeksie
~~~
LINDEX people 2
~~~

- Ustawienie wartości pod podanym indeksem
~~~
LSET people 1 Jerry
~~~

- Wstawienie elementów na koniec listy
~~~
RPUSH people Harry
~~~

- Pobranie ilości elementów listy
~~~
LLEN people
~~~

- Pobranie i usunięcie elementu z góry
~~~
LPOP people
~~~

- Pobranie i usunięcie elementu z dołu
~~~
RPOP people 
~~~

- Wstawienie elementu do listy
~~~
LINSERT people BEFORE "John" "Kate"
~~~

Usunięcie określonej ilości elementów z listy począwszy od podanej wartości
~~~
LREM people 2 John 
~~~

- Przesunięcie elementu pomiędzy listami
~~~
LPUSH sent "order-1"
LPUSH sent "order-2"
LPUSH sent "order-3"
RPOPLPUSH ordered delivered
~~~

### Sets

#### Opis
Nieuporządkowany zbiór **unikalnych** elementów.

- Do 2^32 elementów w każdym kluczu
- zastosowania
    - przechowywanie relacji (znajomi, followers)
    - unikalni odwiedzający stronę www    

#### Podstawowe operacje

- Dodanie elementów do zbioru
~~~ 
SADD members John
SADD members Bob
SADD members Ann
~~~

- Pobranie elementów ze zbioru
~~~
SMEMBERS members
~~~

- Pobranie ilości elementów
~~~
SCARD members
~~~

- Przesunięcie elementu pomiędzy zbiorami
~~~
SADD online user1 user2 user3
SADD offline user4 user5
SMOVE online offline user1
~~~

- Sprawdzenie czy wartość jest elementem zbioru
~~~
SISMEMBER online user2
~~~

- Usunięcie elementu ze zbioru
~~~
SREM online user1
~~~

- Pobranie losowego elementu ze zbioru 
~~~
SADD users user1 user2 user3 user4 user5 
SRANDMEMBER users
~~~

- Pobranie i usunięcie losowego elementu ze zbioru 
~~~
SPOP users
~~~

#### Operacje na zbiorach

- Suma zbiorów
~~~
SUNION online offline
~~~

- Suma zbiorów i zapisanie ich pod nowym kluczem
~~~
SUNIONSTORE all online offline
~~~

- Część wspólna zbiorów
~~~
SADD warszawa company1 company2 company3 company4
SADD bydgoszcz company2 company3 company5 
SINTER warszawa bydgoszcz
~~~

- Część wspólna zbiorów i zapisanie ich pod nowym kluczem
~~~
SINTERSTORE common online offline
~~~

-- Różnica zbiorów
~~~
SDIFF warszawa bydgoszcz
~~~

-- Różnica zbiorów i zapisanie ich pod nowym kluczem
~~~
SDIFFSTORE diff online offline
~~~


### Sorted Sets

#### Opis
- Uporządkowane zbiory elementów. Każdemu elementowi można przypisać wagę (score).

- Do 2^32 elementów w każdym kluczu
- zastosowania
    - listy rankingowe
    - wyszukiwarki

#### Podstawowe operacje

Dodanie elementów
~~~
ZADD skills:john 100 redis
ZADD skills:john 99 sql
ZADD skills:john 94 nosql
ZADD skills:john 70 csharp
ZADD skills:john 30 javascript
ZADD skills:john 1 python
ZADD skills:john -10 basic
~~~

- Pobranie ilości elementów
~~~
ZCARD skills:john 
~~~

- Pobranie rankingu podanego klucza 
~~~
ZSCORE skills:john redis
~~~

- Pobranie elementów wg rankingu
~~~
ZRANGEBYSCORE skills:john 50 100
~~~

- Przedział lewostronnie otwarty (wartości > 1 i <=100)
~~~
ZRANGEBYSCORE skills:john (1 100
~~~

- Przedział prawostronnie otwarty (wartości >= 1 i <100)
~~~
ZRANGEBYSCORE skills:john 1 (100
~~~

- Przedział lewostronnie i prawostronnie otwarty (wartości > 1 i <100)
~~~
ZRANGEBYSCORE skills:john (1 (100
~~~

- Przedział od minus nieskończoności do 100
~~~
ZRANGEBYSCORE skills:john -inf 100
~~~

- Dodawanie wartości nieskończonych
~~~
ZADD skills:john -inf birds
ZADD skills:john +inf football
ZRANGEBYSCORE skills:john -inf +inf
ZRANGEBYSCORE skills:john (-inf (+inf
~~~

- Przedział od minus nieskończoności do plus nieskończoności
~~~
ZRANGEBYSCORE skills:john -inf +inf
~~~

- Zwiększenie rankingu 
~~~ 
ZINCRBY skills:john 1 nosql  
~~~

- Usunięcie elementu ze zbioru
~~~
ZREM skills:john javascript
~~~

- Agregacja zbiorów
~~~
ZADD rezults:mens:100m:round:1 9.99 Runner1 10.00 Runner2 10.03 Runner3
ZADD rezults:mens:100m:round:2 10.99 Runner1 9.99 Runner2 10.03 Runner3
ZUNION 2 rezults:mens:100m:round:1 rezults:mens:100m:round:2 AGGREGATE MIN WITHSCORES 
~~~


- Przykład
Bieg mężczyzn na 100m.
Zawodnik Runner3 został zdyskwalifikowany zatem przyjmujemy +inf
~~~
ZADD rezults:mens:100m:final 9.99 Runner1 10.00 Runner2 +inf Runner3
~~~

- Wyświetlenie wyników wszystkich biegaczy
~~~
ZRANGEBYSCORE rezults:men100m:final -inf +inf WITHSCORES
~~~

- Wyświetlenie wyników, którzy ukończyli bieg
~~~
ZRANGEBYSCORE rezults:men100m:final -inf (+inf WITHSCORES
~~~



### Bitmaps

#### Opis 
String, który może być przetwarzany za pomocą operacji bitowych.


#### Podstawowe operacje

- Ustawienie wartość bitu na określonej pozycji
~~~
SETBIT article1:today 5 1
SETBIT article2:today 5 1
SETBIT article2:today 3 1
SETBIT article2:today 2 1
SETBIT article1:today 2 1
~~~

Pobranie bitu
~~~
GETBIT article1:today 5
~~~

Operacja AND
~~~
BITOP AND readbotharticles article1:today article2:today
GETBIT readbotharticles 2
GETBIT readbotharticles 3
GETBIT readbotharticles 5
~~~

Operacja OR
~~~
BITOP OR readanyarticle article1:today article2:today
GETBIT readanyarticle 2
GETBIT readanyarticle 3
GETBIT readanyarticle 5
~~~

Obliczenie ilości ustawionych bitów na 1
~~~
BITCOUNT readbotharticles
~~~


### Geo

#### Opis 
- Uporządkowane zbiory elementów. Każdemu elementowi można przypisać pozycję (długość i szerokość geograficzną). Geo oparty jest o _Sorted List_.


#### Podstawowe operacje
- Dodanie pozycji
~~~
GEOADD vehicles 52.361389 19.115556 Vehicle1
GEOADD vehicles 52.361389 19.115556 Vehicle2
GEOADD vehicles 52.361389 19.115556 Vehicle3
GEOADD vehicles 52.361389 19.115556 Vehicle4
~~~

- Pobranie pozycji określonego klucza
~~~
GEOPOS vehicles Vehicle2
~~~

- Obliczenie dystansu pomiędzy dwoma pozycjami
~~~ 
GEODIST vehicles Vehicle1 Vehicle4 km
~~~

- Wyszukanie pozycji w określonym promieniu
~~~
GEORADIUS vehicles 0 0 200 km
~~~

- Usunięcie elementu ze zbioru
~~~
ZREM vehicles Vehicle2
~~~

### Pub/Sub

#### Opis
Mechanizm umożliwiający realizację wzorca publish-consument. Zamiast klucza jest kanał (channel). 
Klienci wysyłają wiadomości na określony kanał a odbiorcy otrzymują te wiadomości.

- Utworzenie subskrypcji
~~~
SUBSCRIBE sensors:kitchen:temp
~~~

- Wysłanie wiadomości
~~~
PUBLISH sensors:kitchen:temp 21.01
PUBLISH sensors:bathroom:temp 22.50
PUBLISH sensors:kitchen:temp 20.01
PUBLISH sensors:bathroom:humadity 99
~~~

Odbiorca będzie otrzymywać tylko wiadomości o temperaturze w kuchni zgodnie z szablonem _sensors:kitchen:temp_

Utworzenie subskrypcji z użyciem wzorca
~~~
PSUBSCRIBE sensors:*:temp
~~~

Odbiorca będzie otrzymywać wiadomości o temperaturze ze wszystkich pomieszczeń, zgodnie z szablonem _sensors:*:temp_.

~~~
? - pojedynczy znak
* - dowolny ilość znaków
[ae] - zbiór znaków
~~~

Utworzenie subskrypcji z użyciem wzorca
~~~
PSUBSCRIBE sensors:room?:temp
~~~

- Wysłanie wiadomości
~~~
PUBLISH sensors:kitchen:temp 21.01
PUBLISH sensors:room1:temp 22.50
PUBLISH sensors:room2:temp 20.01
PUBLISH sensors:bathroom:humadity 99
~~~

Odbiorca będzie otrzymywać wiadomości o temperaturze ze wszystkich pokoi, zgodnie z szablonem _sensors:room?:temp_.


- Usunięcie subskrypcji
~~~
UNSUBSCRIBE
~~~

### Streams

#### Opis
Strumienie umożliwiają zapisywanie do zbioru informacji i równoczesne odczytywanie tych informacji.

#### Podstawowe operacje

- Pisanie do strumienia
~~~
XADD events * user john action login
XADD events * user john action visit page index.htm
XADD events * user john action purchase item computer
XADD events * user john action purchase item monitor
XADD events * user john action paid amount 1000
~~~

- Czytanie ze strumienia 
~~~
XREAD count 2 streams events 0
XREAD count 2 streams events 1572983745546-0
~~~


## Backup

### Rodzaje kopii

#### Migawka (snapshot)
- zapis stanu bazy na dysku w pliku *.rdb w formacie _RDB Dumb Format_ 
- zawiera binarną reprezentację zawartości pamięci bazy na dysku

#### AOF (Append-only)
- dziennik (_journal_), który zapisuje wszystkie zmiany w bazie
- umożliwia powrót do wcześniejszego stanu

Należy włączyć w pliku konfiguracyjnym:
'appendonly yes'


### Operacje 

- Backup wybranej bazy danych na dysku
~~~
SAVE
~~~
Powstanie plik _var/libs/redis/dump.rdb_
SAVE uruchamiany jest synchronicznie i blokuje połączenia klientów. Niezalecany na środowisku produkcyjnym. Zamiast tego użyj polecenia _BGSAVE_

- Backup asynchroniczny
~~~
BGSAVE
~~~
Umożliwia dodawanie i modyfikacje danych podczas tej operacji, ale ich zmiany nie będą zapisane w tej migawce.

- Konfiguracja backupu
~~~
CONFIG SET SAVE 60 1
~~~

Oznacza, że backup będzie tworzony co 60 sekund jeśli przynajmniej jeden klucz został zmieniony.

- Pobranie katalogu w którym znajduje się backup
~~~
CONFIG GET dir
~~~

- Pobranie czasu ostatniego backupu w formacie unix
~~~
LASTSAVE
~~~

- Wyłączenie backupu
~~~
CONFIG SET SAVE ""
~~~


- blokuje wszystkie połączenia, zapisuje dane (SAVE) i wyłącza serwer
~~~
SHUTDOWN
~~~

- Pobranie czasu serwera w formie listy dwuelementowej (czas unix i liczbę mikrosekund)
~~~
TIME
~~~



## Autoryzacja

- Ustawienie hasła dla użytkownika domyślnego (default)
~~~
CONFIG SET requirepass P@ssw0rd
~~~

- Autoryzacja
~~~
AUTH P@ssw0rd
~~~

- Usunięcie hasła
~~~
CONFIG SET requirepass ""
~~~

- Sprawdzenie kim jestem
~~~
ACL WHOAMI
~~~

 Utworzenie nowego użytkownika
~~~
ACL SETUSER alice
~~~

- Dodanie hasła do użytkownika
~~~
ACL SETUSER alice on >P@ssw0rd
~~~

- Dodanie uprawnień do użytkownika
~~~
ACL SETUSER alice +get +set
~~~

## Masowe wstawianie danych

- Pobranie danych
~~~ bash
curl http://antirez.com/misc/female-names.txt --output female-names.txt
~~~

- Dostosowanie pliku
~~~ bash
sed 's/^/SADD members /' female-names.txt  > names.txt
~~~


- Skopiowanie pliku do obrazu Dockera
~~~ bash
docker cp names.txt my-redis:/data/names.txt
~~~

- Import danych z pliku do Redisa
~~~ bash
cat names.txt | redis-cli --pipe
~~~

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


## Skrypty

- Wykonane wyrażenia

~~~ lua
EVAL "return 'Hello World'" 0
~~~ 

- Przekazywanie parametru
~~~ lua
EVAL "return 'Hello ' .. ARGV[1]" 0 John
~~~ 

- Wykonane polecenia Redis
~~~ lua
EVAL "return redis.call('SET','foo', 'Hello')" 0
EVAL "return redis.call('GET','foo')" 0 
~~~

- Przekazanie kluczy i wartości parametrów do polecenia Redis
~~~ lua
EVAL "return redis.call('SET',KEYS[1], ARGV[1])" 1 message Hello
EVAL "return redis.call('GET',KEYS[1])" 1 message 
~~~

Parametry skryptu podzielone są na 2 grupy: **KEYS** klucze i **ARGV** argumenty. Przed nimi należy podać ilość parametrów.
Parametry indeksowane są od 1.

- Załadowanie skryptu
~~~ 
SCRIPT LOAD "return redis.call('SET',KEYS[1], ARGV[1])"
~~~

Operacja zwróci SHA.

- Wykonanie skryptu
~~~
EVALSHA {sha} 1 message "Hello World"
~~~

**Uwaga** Tablice w języku LUA rozpoczynają się od 1.

- Wykonanie skryptu z pliku 

_hello.lua_

~~~ lua
local msg = "Hello, world!"
return msg
~~~

~~~ bash
redis-cli --EVAL hello.lua
~~~



- Załadowanie skryptu z pliku
~~~ bash
redis-cli -x SCRIPT LOAD < hello.lua
~~~

- Przerywanie skryptu
~~~ lua
while(true)
do
end
return 0
~~~

~~~ bash
SCRIPT KILL
~~~

- Wstawianie danych
_create-users.lua_
~~~ lua
for i=1,10000 do redis.call('SADD', 'users', "user:"..i) end
return 0
~~~

- Wykonanie skryptu
~~~
EVALSHA {sha} 1 count 1000
~~~



## Cluster

### Tworzenie klastra w systemie Linux


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

### Praca z klastrem

1. Połącz się do jednego z wezłów master
~~~ bash
redis-cli -p 7000 -c   
~~~

uwaga: pamiętaj o parametrze -c



- informacje o działaniu klastra
~~~
CLUSTER INFO
~~~

wskazówka: upewnij się, że `cluster_state:ok`

- Dodaj klucze
~~~ 
SET foo Hello
SET boo World
~~~

Klucze zapisywane są w różnych slotach.

- Rozważmy przykład:
~~~ 
SET user:1 a
SET user:2 b
SET user:3 b
SET user:4 b
SET user:5 b
~~~

Można zauważyć, że przy niektórych kluczah następuje przełączanie pomiędzy wezłami (Node).


Klaster podzielony jest na 16384 slotów.

Każdy węzeł (node) jest odpowiedzialny za podzbiór skrótów (hash slot).

Na przykład kluster z 3 węzłami:

- Node A zawiera hash slots od 10923 do 16384. 
- Node B zawiera hash slots od 5461 do 10922. 
- Node C zawiera hash slots od 11001 do 16383.

https://redis.io/docs/management/scaling/

Wyświetlenie informacji o węzłach wraz przedziałami:
~~~
CLUSTER NODES
~~~

- gdy odwołujemy się do klucza obliczania jest funkcja:
~~~
HASH_SLOT = CRC16(key) mod 16384
~~~

1. oblicza skrót klucza za pomocą funkcji hash CRC16(key)
2. oblicza resztę z dzielenia skrótu przez ilość wszystkich slotów (16384) i otrzymuje slot
3. slot mapowany jest na fizyczną instancję

- Obliczenie funkcji hash dla klucza o podanej nazwie
~~~
CLUSTER KEYSLOT foo
~~~

(klucz nie musi istnieć)

- informacje o slotach (przestarzałe): 
~~~
CLUSTER SLOTS 
~~~

- informacje o slotach (od wersji 7.0)
~~~
CLUSTER SHARDS 
~~~

![Cluster Redis](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*YmO4drOx8janLaKRoc1DTw.png)


### Problemy (błąd CROSSSLOT)

#### Scenariusz 1

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


- Przyczyna
Klucze znajdują się w innych slotach.

Sprawdzmy to:
~~~
CLUSTER KEYSLOT foo
CLUSTER KEYSLOT boo
~~~

- Rozwiązanie
~~~
SET f{oo} Hello
SET b{oo} World
MGET f{oo} b{oo}
~~~


Sprawdzmy to:
~~~
CLUSTER KEYSLOT f{oo}
CLUSTER KEYSLOT b{oo}
~~~
w tym przypadku obydwa klucze mają ten sam slot (obliczony dla {oo}).




#### Scenariusz 1

- Przykład
~~~
SADD user:online user:1 user:2 user:3
SADD user:offline user:4 user:5
~~~

- Problem
~~~
SUNION user:online user:offline
~~~
_(error) CROSSSLOT Keys in request don't hash to the same slot_

- Przyczyna
Klucze znajdują się w innych slotach.

Sprawdzmy to:
~~~
CLUSTER KEYSLOT user:online
CLUSTER KEYSLOT user:offline
~~~



- Rozwiązanie
~~~
SADD {user}:online user:1 user:2 user:3
SADD {user}:offline user:4 user:5
~~~

{...} - oznacza, że tylko dla tej części klucza ma być obliczony hash. Pozostała część nazwy klucza nie ma znaczenia.


#### Scenariusz 2

- Przykład
~~~
SADD user:512:following user:123 user:321 user:132
SADD user:512:followed_by user:123 user:132 
~~~
_(error) CROSSSLOT Keys in request don't hash to the same slot_

- Problem
~~~
SINTER user:512:following user:512:followed_by
~~~
_(error) CROSSSLOT Keys in request don't hash to the same slot_

- Przyczyna
Klucze znajdują się w innych slotach.
Sprawdzmy to:
~~~
CLUSTER KEYSLOT user:512:following 
CLUSTER KEYSLOT user:512:followed_by
~~~


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



## Integracja

### Node.js


1. Zainstaluj pakiet
~~~ bash
npm install redis
~~~

2. Utwórz _app.js_
~~~ js
const redis = require('redis')
const client = redis.createClient();

client
    .on('ready', () => console.log('Connected to Redis.'))
    .on('error', err => console.error('Redis error', err));

client.connect().then(() => {

    client.ping().then(response => console.log(response));

    client.set('foo', 'boo').then(response => console.log(response));
    client.get('foo').then(value => console.log(`Value retrieved from Redis: ${value}`));    

    client.set('score', 0).then(response => console.log(response));
    client.incr('score').then(response => console.log(response));
    client.incrBy('score', 10).then(response => console.log(response));
    client.get('score').then(value => console.log(`Score retrieved from Redis: ${value}`));    

});  
~~~

#### Wersja async-await
~~~ js
const redis = require('redis')
const client = redis.createClient();

(async () => {
    await client.connect();

    const pingCommandResult = await client.ping();
    console.log(pingCommandResult);

    const setCommandResult = await client.set('foo', 'boo');
    console.log(setCommandResult);
    
    const getCommandResult = await client.get('foo');
    console.log(`Value retrieved from Redis: ${getCommandResult}`)
    
    const setScoreCommandResult = await client.set('score', 0);
    console.log(setScoreCommandResult);

    const incrCommandResult = await client.incr('score');
    console.log(incrCommandResult);

    const incrByCommandResult = await client.incrBy('score', 10);
    console.log(`Score retrieved from Redis: ${incrByCommandResult}`);

})();
~~~
