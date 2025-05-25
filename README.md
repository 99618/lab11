# Sprawozdanie z zadania laboratorium 11. 

## Pzzebieg zadania
1. Utworzenie sieci mostkowej lab11net:
```bash
  docker network create –driver bridge lab11net
  ```
![Screen](lab11_s1.PNG)

2. Utworzenie poszczególnych kontenerów web1, web2, web3 z podłączeniem do sieci lab11net,
zmapowaniem na różne porty dla hostów oraz podpięcie katalogów z logami i stroną html do nginx.

web1:
```bash
  docker run --rm -d --name web1 --network lab11net -p 8080:80 --mount type=bind,source="%USERPROFILE%\lab11\html\web1",target=/usr/share/nginx/html,readonly --mount type=bind,source="%USERPROFILE%\lab11\logs\web1",target=/var/log/nginx nginx:latest
  ```
web2:
```bash
  docker run --rm -d --name web2 --network lab11net -p 8081:80 --mount type=bind,source="%USERPROFILE%\lab11\html\web2",target=/usr/share/nginx/html,readonly --mount type=bind,source="%USERPROFILE%\lab11\logs\web2",target=/var/log/nginx nginx:latest
  ```
web3:
```bash
  docker run --rm -d --name web3 --network lab11net -p 8082:80 --mount type=bind,source="%USERPROFILE%\lab11\html\web3",target=/usr/share/nginx/html,readonly --mount type=bind,source="%USERPROFILE%\lab11\logs\web3",target=/var/log/nginx nginx:latest
  ```
Wykonanie poleceń w terminalu:
![Screen](lab11_s2.PNG)

## Potwiedzenie poprawności rozwiązania
1. Potwierdzenie działania kontenerów:
```bash
  docker ps --filter "name=web"
  ```
![Screen](lab11_s4.PNG)

2. Potwierdzenie działania stron za pomocą polecenia curl:
![Screen](lab11_s3.PNG)

3. Podejrzenie logów serwera na hoście za pomocą polecenia type, np.:
```bash
  type "%USERPROFILE%\lab11\logs\web1\access.log"
  ```
```bash
  "%USERPROFILE%\lab11\logs\web1\error.log"
  ```
Podfoldery i pliki logów:
![Screen](lab11_s5.PNG)

Porównanie plików access.log pomiędzy kontenerami:
![Screen](lab11_s6.PNG)

  
