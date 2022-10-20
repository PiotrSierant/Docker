# Docker

### Linki warte uwagi 

* [Co to jest Docker i dlaczego warto go znać](https://www.youtube.com/watch?v=VDZAzjqL4BQ&list=PL2zsrr3O56srCDp5UjAKkvaQYI0Kacxqo&index=1)
* [Pobierz Docker](https://docs.docker.com/get-docker/)
* [Instalacja Docker'a](https://www.youtube.com/watch?v=ssTS6q_6eSg)
* [Linux w Windowsie? - Instalacja Linuksa z wykorzystaniem WSL-a](https://www.youtube.com/watch?v=fyn3Whhlt08)

### Instalacja
* [Instalacja Windows](https://docs.docker.com/desktop/install/windows-install/)
* [Instalacja Linux](https://docs.docker.com/engine/install/)
* [Instalacja Mac](https://docs.docker.com/desktop/install/mac-install/)
* [Zainstaluj Linuksa w systemie Windows z WSL](https://learn.microsoft.com/pl-pl/windows/wsl/install)
  * [Kroki ręcznej instalacji dla starszych wersji WSL](https://learn.microsoft.com/pl-pl/windows/wsl/install-manual)

#### Moja historia instalacji, krok po kroku
Otwarcie power shella: 
* Step 1 - Enable the Windows Subsystem for Linux
  ```
  dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
  ```
  
* Step 2 - Enable Virtual Machine feature
  ```
  dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
  ```
  
* Step 3 - Download the Linux kernel update package
  [Pobranie i instalacja pliku](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

* Step 4 - Set WSL 2 as your default version
  ```
  wsl --set-default-version 2
  ```
* Step 5 - Install your Linux distribution of choice
  * Instalacja wybranej dystrybucji Linux`a. [(Mój wybór)](https://www.microsoft.com/store/apps/9N9TNGVNDL3Q)
### Komendy
#### Uruchomienie
```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```
```
docker run [docker_image]
```
Przykład: 
```
docker run hello-world
```
#### Wyświetlanie listy kontenerów
```
docker ps -a
```
#### Usuwanie wybranego obrazu
```
docker rmi [ID/Name]
```
#### Usuwanie wszystkich nieużywanych obrazów
```
docker rmi $(docker images -q)
```
#### Upublicznianie portów
```
-p [host_ip]:[host_port]:[container_port]
```
Przykład:
```
docker run -p 8080:80 nginx
```
#### Nadawanie nazw kontenerom
```
docker run --name [container_name] [docker_image]
```
Przykład:
```
docker run --name my-nginx -p 8080:80 nginx
docker run --name my-db -e MYSQL_ROOT_PASSWORD=password -p 3306:3306 mysql:8
```