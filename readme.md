# Michał Grzona, grupa 3, 121356
## Nowoczesne technologie przetwarzania danych

### Zawartość plików
- <i>model.pkl</i> - plik zawierający zapisany model.
- <i>model.py</i> - skrypt wczytujący model z pliku. W przypadku, gdy nie ma zapisanego modelu tworzy nowy model regresji logistycznej. Model został wytrenowany na datasecie <i>Iris</i> pochodzącym z biblioteki <i>sci-kit learn</i>
- <i>app.py</i> - główny skrtyp aplikacji, obsluga endpointów API.

### Endpointy API
- <i>/</i> - zwraca prostą wiadomość w formacie json (zadanie 1.)
![img.png](img.png)
- <i>/predict</i> - zwraca predykcję modelu regresji logistycznej (zdanie 2). W celu uzyskania odpowiedzi na żądanie należy przesłać odpiwdnie dane w formacie json. Model zwraca odpwiedź w formacie json. W odpowiedzi znajduje się predykcja modelu reprezentowana przez numer klasy. Przykład zapytania:
![img_1.png](img_1.png)
W przypadku błędnego zapytania (nieprawidłowy format) wyświetli się odpowiedni komunikat (zadanie 3.):
  - W przypadku przesłania danych w formacie innym niż json:
  ![img_3.png](img_3.png)
  - W przypadku braku odpowiednich kluczy:
  ![img_2.png](img_2.png)
- <i>/info</i> - zwraca informacje o modelu (zadanie 4.)
![img_4.png](img_4.png)
- <i>/health</i> - zwraca informacje dotyczące statusu serwera (zadanie 4.)
![img_5.png](img_5.png)

### Zdanie 5. Uruchomienie środowiska produkcyjnego
Ze względu, iż Gunicorn nie działa na systemie Windows wykorzystałem Waitress.
![img_6.png](img_6.png)
Aplikacja działa na porcie 8080.