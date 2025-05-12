# Michał Grzona, grupa 3, 121356
## Nowoczesne technologie przetwarzania danych

# Laboratorium 3.

### Zawartość plików
- <i>model.pkl</i> - plik zawierający zapisany model.
- <i>model.py</i> - skrypt wczytujący model z pliku. W przypadku, gdy nie ma zapisanego modelu tworzy nowy model regresji logistycznej. Model został wytrenowany na datasecie <i>Iris</i> pochodzącym z biblioteki <i>sci-kit learn</i>
- <i>app.py</i> - główny skrtyp aplikacji, obsluga endpointów API.

### Endpointy API
- <i>/</i> - zwraca prostą wiadomość w formacie json (zadanie 1.)
![img.png](imgs/img.png)
- <i>/predict</i> - zwraca predykcję modelu regresji logistycznej (zdanie 2). W celu uzyskania odpowiedzi na żądanie należy przesłać odpiwdnie dane w formacie json. Model zwraca odpwiedź w formacie json. W odpowiedzi znajduje się predykcja modelu reprezentowana przez numer klasy. Przykład zapytania:
![img_1.png](imgs/img_1.png)
W przypadku błędnego zapytania (nieprawidłowy format) wyświetli się odpowiedni komunikat (zadanie 3.):
  - W przypadku przesłania danych w formacie innym niż json:
  ![img_3.png](imgs/img_3.png)
  - W przypadku braku odpowiednich kluczy:
  ![img_2.png](imgs/img_2.png)
- <i>/info</i> - zwraca informacje o modelu (zadanie 4.)
![img_4.png](imgs/img_4.png)
- <i>/health</i> - zwraca informacje dotyczące statusu serwera (zadanie 4.)
![img_5.png](imgs/img_5.png)

### Zdanie 5. Uruchomienie środowiska produkcyjnego
Ze względu, iż Gunicorn nie działa na systemie Windows wykorzystałem Waitress.
![img_6.png](imgs/img_6.png)
Aplikacja działa na porcie 8080.

# Laboratorium 4.

### Zadanie 1.
Utworzyłem plik <i>requirements.txt</i> zawierający moduły konieczne do instalacji do wirtualnego środowiska w celu poprawnego działania aplikacji. Wymagane biblioteki to:
- NumPy
- Flask
- scikit-learn

### Zadanie 2. Ze względu na wygodę korzystania z Dockera resztę ćwiczenia wykonałem na maszynie wirtualnej z systemem operacyjnym Ubuntu
Utworzyłem dockerfile o nazwie Dockerfile w drzewie projektu. Następnie na jego podstawie utworzyłem obraz dockerowy.
![img_7.png](imgs/img_7.png)

### Zadanie 3. 
Na podstawie wcześniej utworzonego obrazu utworzyłem kontener docker za pomocą komendy `docker run -d -p 5000:5000 ntpd-flask-app`.
![img_8.png](imgs/img_8.png)
Aplikacja po ruchumieniu w kontenerze działa poprawnie. Przykładowa predykcja:
![img_9.png](imgs/img_9.png)

### Zadanie 4.
Utworzyłem plik docker-compose.yaml i za jego pomocą uruchomiłem aplikację. Jako dodatkowy serwis wybrałem Redis. Dodałem prostą funkcjonalność która zlicza ilość zapytań pod endpoint <i>counter</i>.
![img_10.png](imgs/img_10.png)
![img_11.png](imgs/img_11.png)

### Zadanie 5. Sposób uruchaminia
Przed uruchomienime aplikacji należy pobrać cały kod z GitHub'a. Sposoby uruchamiania aplikacji:
- lokalnie - należy otworzyć projekt w wybranym IDE, skonfigurować interpreter python i zainstalować zależności podane w pliku requirements.txt. Jako zmienne środowiskowe można ustawić:
  - <i>FLASK_APP</i> - wskazanie na główny plik aplikacji. Domyślnie app.py
  - <i>FLASK_RUN_HOST</i> - wskazanie na jakim adresie ma działać aplikacji. Domyślnie localhost.
    - <i>FLASK_RUN_PORT</i> - wskazanie na jakim porcie ma działać aplikacja. Domyślnie 5000.
- za pomocą Dockera - na podstawie dostarczonego pliku Dockerfile należy zbudować obraz aplikacji. Dodatkowo należy pobrać obraz Redis, a następnie uruchomić 2 kontenery docker bazujące na wcześniej wspomnianych obrazach.
- za pomocą Docker Compose - należy wykorzystać plik `docker-compose.yaml` zawarty w projekcie. Po wejściu w katalog projektu w terminalu wpisac `docker-compose up -d`. UWAGA: przed wpisaniem komendy może być wymagane wpisanie sudo i podanie hasła administratora. `sudo docker-compose up -d`