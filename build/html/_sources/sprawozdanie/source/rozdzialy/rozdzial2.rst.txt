Uprawnienia Użytkownika
=======================

Uprawnienia użytkownika w PostgreSQL są zarządzane na kilku poziomach:
systemu zarządzania bazą danych (DBMS), poszczególnych baz danych oraz
tabel.

Poziom DBMS
-----------

Na poziomie DBMS uprawnienia mogą obejmować możliwość tworzenia nowych
baz danych, zarządzanie użytkownikami oraz konfigurację systemu.
Przykładowe polecenia to:

::

   GRANT CREATE ON DATABASE dbname TO username;
   REVOKE CREATE ON DATABASE dbname FROM username;

Administratorzy bazy danych (DBA) mają pełne uprawnienia na poziomie
DBMS, co pozwala im na zarządzanie wszystkimi aspektami działania
systemu PostgreSQL. Uprawnienia te mogą obejmować:

-  Tworzenie i usuwanie baz danych.

-  Tworzenie i zarządzanie użytkownikami oraz rolami.

-  Konfigurację parametrów systemowych i optymalizację działania bazy
   danych.

Poziom Bazy Danych
------------------

Na poziomie bazy danych uprawnienia mogą obejmować dostęp do danych,
modyfikację struktur oraz wykonywanie operacji administracyjnych.
Polecenia zarządzające uprawnieniami to:

::

   GRANT ALL PRIVILEGES ON DATABASE dbname TO username;
   REVOKE CONNECT ON DATABASE dbname FROM username;

Uprawnienia na poziomie bazy danych mogą być szczegółowo dostosowane do
potrzeb poszczególnych użytkowników lub grup użytkowników (ról). Na
przykład, można przyznać uprawnienia do:

-  Łączenia się z bazą danych (``CONNECT``).

-  Tworzenia nowych schematów (``CREATE``).

-  Wykonywania zapytań (``SELECT``) i modyfikacji danych (``INSERT``,
   ``UPDATE``, ``DELETE``).

-  Zarządzania tabelami i innymi obiektami bazy danych (``ALTER``,
   ``DROP``).

Poziom Tabeli
-------------

Na poziomie tabeli uprawnienia mogą obejmować selekcję, wstawianie,
aktualizację oraz usuwanie danych. Przykładowe polecenia to:

::

   GRANT SELECT, INSERT ON TABLE tablename TO username;
   REVOKE UPDATE ON TABLE tablename FROM username;

Precyzyjne zarządzanie uprawnieniami na poziomie tabeli pozwala na
ochronę danych przed nieautoryzowanym dostępem oraz modyfikacją.
Przykłady uprawnień obejmują:

-  ``SELECT`` - możliwość odczytu danych z tabeli.

-  ``INSERT`` - możliwość dodawania nowych rekordów do tabeli.

-  ``UPDATE`` - możliwość modyfikowania istniejących rekordów.

-  ``DELETE`` - możliwość usuwania rekordów.

Role i Grupy Użytkowników
-------------------------

PostgreSQL umożliwia tworzenie ról i grup użytkowników, co upraszcza
zarządzanie uprawnieniami. Role mogą mieć przypisane uprawnienia, które
są dziedziczone przez użytkowników przypisanych do tych ról. Przykładowe
polecenia:

::

   CREATE ROLE read_only;
   GRANT SELECT ON ALL TABLES IN SCHEMA public TO read_only;
   GRANT read_only TO username;

Stosowanie ról i grup użytkowników pozwala na bardziej elastyczne i
skalowalne zarządzanie uprawnieniami. Na przykład, można stworzyć rolę
``read_only``, która ma tylko uprawnienia do odczytu danych, a następnie
przypisać tę rolę wielu użytkownikom, co znacznie upraszcza
administrację.
