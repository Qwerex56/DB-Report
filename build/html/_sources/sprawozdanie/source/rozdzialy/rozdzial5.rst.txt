
Szyfrowanie Danych
==================

Szyfrowanie danych w PostgreSQL może odbywać się zarówno na poziomie
transmisji danych, jak i na poziomie przechowywania danych.

Szyfrowanie w Transmisji
------------------------

Jak wspomniano wcześniej, SSL/TLS umożliwia szyfrowanie danych podczas
transmisji między klientem a serwerem, co zapobiega nieautoryzowanemu
dostępowi do danych w trakcie ich przesyłania.

Szyfrowanie na Poziomie Dysku
-----------------------------

PostgreSQL nie posiada natywnego wsparcia dla szyfrowania danych na
poziomie tabel lub baz danych, jednak możliwe jest wykorzystanie
zewnętrznych narzędzi i systemów plików szyfrujących. Przykładem może
być system plików z szyfrowaniem (np. LUKS w systemach Linux) lub
szyfrowanie oferowane przez rozwiązania chmurowe (np. Amazon RDS).

Przykładowa konfiguracja szyfrowania dysku na systemie Linux z użyciem
LUKS:

::

   sudo cryptsetup luksFormat /dev/sdX
   sudo cryptsetup luksOpen /dev/sdX encrypted_disk
   sudo mkfs.ext4 /dev/mapper/encrypted_disk
   sudo mount /dev/mapper/encrypted_disk /mnt/encrypted

Szyfrowanie na Poziomie Aplikacji
---------------------------------

Innym podejściem do szyfrowania danych jest szyfrowanie na poziomie
aplikacji, gdzie dane są szyfrowane przed zapisaniem do bazy danych i
odszyfrowywane po ich odczytaniu. Takie podejście zapewnia pełną
kontrolę nad procesem szyfrowania, jednak wymaga dodatkowej
implementacji w kodzie aplikacji.

Przykładowe biblioteki do szyfrowania danych na poziomie aplikacji:

-  **Python** - ``cryptography``, ``pycryptodome``.

-  **Java** - ``javax.crypto``, ``Bouncy Castle``.

-  **JavaScript** - ``crypto``, ``sjcl``.

Zarządzanie Kluczami Szyfrującymi
---------------------------------

Kluczowym elementem skutecznego szyfrowania danych jest zarządzanie
kluczami szyfrującymi. Klucze muszą być bezpiecznie przechowywane i
zarządzane, aby zapobiec ich utracie lub kradzieży. Przykładowe
narzędzia do zarządzania kluczami:

-  **HashiCorp Vault** - bezpieczne przechowywanie i zarządzanie
   tajemnicami oraz kluczami szyfrującymi.

-  **AWS Key Management Service (KMS)** - zarządzanie kluczami w
   środowisku chmurowym Amazon Web Services.

-  **GCP Cloud KMS** - zarządzanie kluczami w środowisku Google Cloud
   Platform.
