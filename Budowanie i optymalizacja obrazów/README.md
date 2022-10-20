# Docker

### Linki warte uwagi 
[Budowanie obrazów](https://www.youtube.com/watch?v=jcXfOjYeqEk)
### Budowanie obrazów

* Obrazy możemy w zasadzie tworzyć na dwa sposoby:
  * poprzez commit istniejącego kontenera
  * poprzez zbudowanie obrazu z wykorzystaniem pliku Dockerfile

1. Uruchamiamy kontener w oparciu o wybraną dystrybucję, z uruchomieniem bash-a, abyśmy mogli wejść później do kontenera i doinstalować wszystko co potrzebujemy.

```
docker run --name ubuntu -it -d ubuntu:20.04 bash
```

2. Wchodzimy do terminala kontenera i instalujemy
```
docker exec -it ubuntu bash
```
Instalujemy 
```
apt update
apt upgrade -y
apt install -y git openjdk-14-jdk maven
```

3. Klonujemy dane z repozytorium do konetenera
```
mkdir /code
cd /code
git clone https://gitlab.com/DevNotes.it/java/springbootshoopinglist-demo.git .
```
Budujemy aplikację (zgodnie z instrukcją z repozytorium)
```
mvn package
```
Przenosimy zbudowaną aplikację do docelowego katalogu
```
mkdir /opt/app
mv /code/target/DemoApp.jar /opt/app
```
Usuwamy wszystko co już nam nie będzie potrzebne, aby zmniejszyć rozmiar obrazu.
Usuwamy kod źródłowy naszej aplikacji
```
cd /
rm -r /code
```
Usuwamy zbędne aplikacje:
```
apt remove git maven
```
Czyścimy cache APT-a:
```
apt clean
apt autoremove --purge -y
rm -rf /var/lib/apt/lists
```
4. Commitujemy kontener
Wychodzimy z kontenera - `ctrl+d` - i commitujemy go.
```
docker commit ubuntu demo-app:v1
```
Właśnie utworzyliśmy nowy obraz o nazwie app. Dzięki tagom możemy tworzyć różne wersje obrazów.

Sprawdźmy czy obraz istnieje:
```
docker images
```
5. Sprawdzamy czy obraz będzie działać. Uruchamiamy kontener wraz z uruchomieniem naszej aplikacji.
```
docker run -it -d --name demo-app -p 80:8080 demo-app:v1 java -jar /opt/app/DemoApp.jar
```

#### Budujemy obraz w oparciu o plik Dockerfile

1. Utwórzmy plik Dockerfile
2. Budujemy obraz i nazywamy go java-app i ustawiamy tag v1:
```
docker build -t java-app:v .
```
3. Uruchamiamy kontener w oparciu o zbudowany obraz:
```
docker build -t java-app:v .
```

#### Przechowywanie obrazów
* DockerHub
* Github
* Gitlab

```
docker build -t <registry_url:version> .
```

```
docker push <registry_url>:<version>
```