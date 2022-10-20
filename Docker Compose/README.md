# Docker

### Linki warte uwagi 
* [Uproszczenie procesu uruchamiania kontenerów](https://www.youtube.com/watch?v=7tFQpv76FBE&t=0s)
* [Docker compose dla Linux](https://docs.docker.com/compose/install/)


#### docker-compose.yaml

Taki plik będziemy często przechowywać przy kodzie naszej aplikacji, tak aby każda osoba pracująca nad kodem uruchamiała kontener w tej samej konfiguracji.

Przeanalizujmy jak wyglądałby dla powyższego polecenia plik `docker-file.yaml`

```
version: "3.9"
services:
  java-app:
    image: registry.gitlab.com/devnotes.it/java/springbootshoopinglist-demo:v1
    ports:
      - "80:8080"
```
I uruchamiamy _(gdzie -d oznacza działanie w tle - tak jak przy docker run.)_
```
docker-compose up -d
```
Ważne
Jeżeli zmienicie coś w pliku Dockerfile to musicie przebudować obraz za pomocą polecenia:

docker-compose build