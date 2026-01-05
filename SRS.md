# 5. Atrybuty Jakościowe

Poniżej zdefioniowano atrybuty jakościowe, które opisują, w jaki sposób system ma docelowo działać. Poniższe cele są mierzalne, co ułatwia dalsze tworzenie aplikacji i umożliwi w przyszłości określenie postępów w tworzeniu i rozwoju aplikacji.

* **Wydajność (Performance):**
    * **WNF-WYD-01:** Aplikacja musi stać się w pełni interaktywna (użytkownik może kliknąć i przewijać) w czasie poniżej 5 sekund od rozpoczęcia ładowania, nawet przy złożonych (np. tygodniowych) planach.
* **Dostępność (Availability):**
    * **WNF-NIEZ-01:** System musi posiadać mechanizm pobierania danych z pamięci podręcznej (cache), umożliwiający wyświetlenie wcześniej wygenerowanych planów, nawet gdy zewnętrzne API (np. OpenTripMap) jest nieosiągalne.
* **Bezpieczeństwo (Security):**
    * **WNF-BEZ-01:** Połączenie między przeglądarką użytkownika a serwerem musi być wymuszone przez protokół HTTPS z certyfikatem TLS 1.3.
    * **WNF-BEZ-02:** Wszystkie dane wrażliwe użytkowników, takie jak tokeny sesyjne, adresy e-mail, czy hasła przesyłane między frontendem a backendem muszą być chronione przez politykę Content Security Policy (CSP), która uniemożliwia wykonywanie nieautoryzowanych skryptów (ataki XSS).
* **Skalowalność (Scalability):**
    * **WNF-SKAL-01:** System musi być w stanie automatycznie uruchomić dodatkowe instancje kontenerów w czasie poniżej 30 sekund w odpowiedzi na gwałtowny wzrost liczby użytkowników obecnie korzystających z aplikacji.

### Jakość projektu

* **Modyfikowalność (Modifiability):**
    * **WNF-MOD-01:** System musi umożliwiać dodanie nowej wersji językowej interfejsu bez ingerencji w kod źródłowy, jedynie poprzez dołączenie nowego pliku z tłumaczeniami w formacie JSON lub YAML.
* **Przenośność (Portability):**
    * **WNF-PRZEN-01:** Całość infrastruktury aplikacji (backend, frontend, baza danych, cache) musi być zdefiniowana jako kod (Infrastructure as Code) w pliku `docker-compose.yml`, umożliwiając uruchomienie identycznego środowiska na systemach Windows, macOS oraz Linux.


## Kluczowe atrybuty niefunkcjonalne

Poniżej wyróżniono trzy najważniejsze atrybuty jakościowe dla naszego projektu:

### 1. Modyfikowalność
System polega na zewnętrznych źródłach danych, więc ich struktura może często ulegać zmianie. Wysoka modyfikowalność pozwala na błyskawiczną adaptację do nowych wersji API lub łatwe podpięcie nowych partnerów afiliacyjnych bez odczuwalnych przerw w działaniu aplikacji.

### 2. Wydajność
Użytkownik korzystający z aplikacji oczekuje responsywnej aplikacji, która będzie realizować polecenia użytkownika tuż po zleceniu działania. Optymalizacja szybkości generowania tras i responsywności całej aplikacji bezpośrednio wpływa na ilość wykorzystanych linków afiliacyjnych. Im szybciej działa aplikacja, tym mniejsza szansa na rezygnację użytkownika z korzystania z generowanego planu.

### 3. Dostępność
Podróżujący często sprawdzają plany w miejscach z ograniczonym zasięgiem. Stabilność systemu i mechanizmy cache gwarantują, że użytkownik zawsze ma dostęp do swojego planu, co daje przewagę nad innymi rozwiązaniami oraz umożliwia częste korzystanie z aplikacji.

# 6. Analiza Porównawcza

W ramach analizy porównawczej zestawiono nasza aplikację razem z bezpośrednią konkurencją, czyli popularną aplikacją do planowania podróży Wanderlog oraz z konkurencją pośrednią, czyli Google Maps. Poniżej pokakano tabelę, w której porównano Funkcjonalność, UX, model biznesowy oraz wspracie zewnętrznych rozwiązań w wymienionych aplikacjach.

| **Kryterium Oceny** | **Nasza aplikacja** | **Wanderlog** | **Google Maps** |
| :--- | :--- | :--- | :--- |
| **Funkcjonalność** | System sam układa plan dnia i trasę na bazie preferencji i budżetu. | Aplikacja pozwala na zapisywanie rezerwacji, notatek i ręczne tworzenie listy miejsc do odwiedzenia. | Aplikacja pozwala na lokalizację miejsc i szukaniu drogi pomiędzy poszczególnymi obiektami |
| **User Experience** | Minimalistyczny interfejs, natychmiastowy wynik bez nadmiarowej konfiguracji. | Rozbudowany interfejs z wieloma panelami, wymagający czasu na opanowanie. | Wygodna do nawigacji, ale nie najlepsza przy tworzeniu szczegółowego planu podróży. |
| **Model Biznesowy** | Darmowy dostęp do planera, prowizje od rezerwacji oraz płatne warianty tras (VIP). |  Wiele funkcji, np. plan podróży offline, czy śledzenie bieżącej trasy lotu wybranego samolotu ukrytych za płatnym abonamentem. | Zarabianie na widoczności lokalnych firm i danych użytkowników. |
| **Wsparcie i wykorzystanie zewnętrznych rozwiązań** |  Oparcie na OpenStreetMap i OpenTripMap, odsyłanie do zewnętrznych portali rezerwacyjnych dzieki linkom afiliacyjnym. | Integracja z Gmail i komercyjnymi API dostawców map. | Pełna integracja z usługami Google, ogromna baza danych gromadzonych przez Google. |


**1. Co konkurencja robi dobrze?**
* Google Maps oferuje czytelny widok punktów na mapie oraz wyczerpującą ilość danych o miejscach. Nasz system powinien dążyć do podobnej płynności działania mapy i wygody z korzystania z map.
* Wanderlog w wygodny sposób pozwala znaleźć noclegi w zależności od tego, gdzie użytkownik będzie przebywał danego dnia. Nasza aplikacja również powinna dopasowywać noclegi do miejsca, w którym uzytkownik będzie sie znajdował.

**2. Jakie są słabe punkty konkurencji?**
* Google Maps daje narzędzia, ale nie zwraca gotowego planu podróży. Nasza aplikacja automatyzuje tworzenie planów, co może zachęcić użytkowników do korzystania z naszej aplikacji.
* Wanderlog jest zbyt rozbudowany do krótkich wyjazdów, dodatkowo blokuje funkcje offline za subskrypcją. Nasz projekt stawia na darmowy dostęp offline, co może przyciągnąć użytkowników, którzy będą podróżować po miejscach z ograniczonym zasięgiem i dostępem do internetu.
