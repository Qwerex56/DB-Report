Zabezpieczenie Połączenia przez SSL/TLS
=======================================

SSL (Secure Sockets Layer) oraz TLS (Transport Layer Security) są
standardowymi technologiami zabezpieczającymi połączenia sieciowe, w tym
również połączenia z bazą danych PostgreSQL.

Konfiguracja SSL/TLS
--------------------

Aby włączyć SSL/TLS w PostgreSQL, należy skonfigurować plik
``postgresql.conf`` oraz odpowiednio dostosować plik ``pg_hba.conf``.
Przykład konfiguracji:

::

   # postgresql.conf
   ssl = on
   ssl_cert_file = 'server.crt'
   ssl_key_file = 'server.key'

Dodatkowo, w pliku ``pg_hba.conf`` należy zdefiniować reguły
uwierzytelniania z użyciem certyfikatów SSL:

::

   # pg_hba.conf
   hostssl all all 0.0.0.0/0 cert

Tworzenie i Zarządzanie Certyfikatami
-------------------------------------

Do korzystania z SSL/TLS konieczne jest posiadanie certyfikatu serwera
oraz klucza prywatnego. Certyfikaty te mogą być wydawane przez zaufane
urzędy certyfikacji (CA) lub generowane samodzielnie (self-signed).
Przykładowe polecenia do generowania własnych certyfikatów:

::

   openssl genrsa -des3 -out server.key 2048
   openssl req -new -key server.key -out server.csr
   openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

Korzyści z SSL/TLS
------------------

SSL/TLS zapewnia szyfrowanie danych przesyłanych między klientem a
serwerem, co chroni przed podsłuchiwaniem oraz modyfikowaniem danych
podczas transmisji. Zapewnia również uwierzytelnienie serwera oraz,
opcjonalnie, klienta, co zwiększa bezpieczeństwo całego systemu.

Korzyści z używania SSL/TLS obejmują:

-  Ochronę danych wrażliwych podczas transmisji przez sieć.

-  Zapobieganie atakom typu man-in-the-middle, które polegają na
   przechwytywaniu i modyfikacji danych.

-  Uwierzytelnianie serwera, co pozwala klientom na weryfikację, że
   łączą się z właściwym serwerem.

Monitorowanie i Audyt Połączeń SSL/TLS
--------------------------------------

Ważnym aspektem korzystania z SSL/TLS jest monitorowanie i audyt
połączeń zabezpieczonych. PostgreSQL oferuje mechanizmy logowania, które
mogą rejestrować informacje o połączeniach SSL/TLS, co pozwala na:

-  Identyfikację prób nieautoryzowanego dostępu.

-  Analizę i diagnostykę problemów z połączeniami.

-  Zapewnienie zgodności z politykami bezpieczeństwa organizacji.
