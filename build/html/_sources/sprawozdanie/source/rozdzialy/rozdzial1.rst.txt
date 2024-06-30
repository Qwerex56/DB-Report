pg_hba.conf - Sterowanie Dostępem
=================================

Plik ``pg_hba.conf`` (PostgreSQL Host-Based Authentication) jest
kluczowym elementem zarządzania bezpieczeństwem w PostgreSQL. Umożliwia
on kontrolę dostępu do serwera bazy danych na podstawie adresów IP,
typów połączeń oraz mechanizmów uwierzytelniania.

Struktura pliku pg_hba.conf
---------------------------

Plik ``pg_hba.conf`` składa się z linii, z których każda definiuje
regułę dostępu. Każda linia zawiera następujące pola:

-  **typ połączenia** - określa, czy połączenie jest lokalne
   (``local``), czy zdalne (``host``).

-  **baza danych** - nazwa bazy danych, do której dostęp jest
   kontrolowany.

-  **użytkownik** - nazwa użytkownika bazy danych.

-  **adres** - adres IP klienta (dla połączeń zdalnych).

-  **metoda uwierzytelniania** - określa mechanizm uwierzytelniania,
   który ma być używany.

Przykład reguły w pliku ``pg_hba.conf``:

::

   # Typ    Baza danych    Użytkownik    Adres              Metoda
   host     all            all           192.168.1.0/24     md5

Mechanizmy Dostępu
------------------

Plik ``pg_hba.conf`` definiuje kilka mechanizmów uwierzytelniania,
takich jak:

-  **trust** - pozwala na dostęp bez uwierzytelniania. Jest to opcja
   najmniej bezpieczna i powinna być używana tylko w wyjątkowych
   przypadkach.

-  **md5** - wykorzystuje hasła zaszyfrowane algorytmem MD5. Jest to
   standardowy mechanizm uwierzytelniania.

-  **password** - wymaga podania hasła w postaci nieszyfrowanej. Jest to
   mniej bezpieczne niż ``md5``.

-  **peer** - umożliwia uwierzytelnianie na podstawie identyfikatora
   systemowego użytkownika.

-  **cert** - wykorzystuje certyfikaty SSL do uwierzytelniania.

-  **scram-sha-256** - nowoczesny i bezpieczny mechanizm
   uwierzytelniania, który wykorzystuje algorytm SCRAM-SHA-256.

Konsekwencje Wyboru Mechanizmu Dostępu
--------------------------------------

Wybór odpowiedniego mechanizmu uwierzytelniania ma bezpośredni wpływ na
bezpieczeństwo systemu. Mechanizmy takie jak ``trust`` mogą znacznie
obniżyć poziom bezpieczeństwa, podczas gdy ``cert`` w połączeniu z SSL
zapewnia wysoki poziom ochrony danych. Warto dokładnie analizować
potrzeby i ryzyka związane z każdym mechanizmem uwierzytelniania.

Na przykład, stosowanie mechanizmu ``trust`` może być akceptowalne w
przypadku baz danych używanych wyłącznie w środowisku testowym, gdzie
bezpieczeństwo nie jest priorytetem. Natomiast w środowisku
produkcyjnym, gdzie przetwarzane są dane wrażliwe, konieczne jest użycie
bardziej zaawansowanych mechanizmów, takich jak ``md5``,
``scram-sha-256`` lub ``cert``.

Przykłady Konfiguracji
----------------------

Przykładowe konfiguracje pliku ``pg_hba.conf`` mogą obejmować różne
scenariusze dostępu:

::

   Pozwól na połączenie dowolnego użytkownika z hostem 192.168.12.10 do bazy danych "postgres", jeśli hasło 
   użytkownika jest poprawnie podane
   # Typ   Baza danych    Użytkownik    Adres              Metoda
   host    postgres       all           192.168.12.10/32   scram-sha-256

   Pozwól dowolnemu użytkownikowi na lokalnym systemie łączyć się z dowolną bazą danych
   używając dowolnej nazwy użytkownika bazy danych za pomocą gniazd Unix (domyślnie dla połączeń lokalnych)
   # Typ   Baza danych    Użytkownik    Adres              Metoda
   local   all            all                              trust

   Pozwól na połączenie używając wyrażenia regularnego dla DATABASE, które pozwala na połączenie z bazą danych db1, db2 
   oraz dowolnymi bazami danych o nazwie zaczynającej się od "db" i kończącej się liczbą składającą się z dwóch do 
   czterech cyfr (np. "db1234" lub "db12").
   # Typ   Baza danych                Użytkownik    Adres          Metoda
   local   db1,"/^db\d{2,4}$",db2     all           localhost      trust
