Zarządzanie Użytkownikami a Dane Wprowadzone
============================================

Zarządzanie użytkownikami w PostgreSQL obejmuje tworzenie, modyfikowanie
i usuwanie użytkowników oraz ról. Ważnym aspektem jest zarządzanie
danymi wprowadzonymi przez użytkowników, szczególnie w kontekście
usuwania użytkowników.

Tworzenie i Modyfikowanie Użytkowników
--------------------------------------

Tworzenie nowych użytkowników w PostgreSQL odbywa się za pomocą
polecenia ``CREATE USER``. Przykład:

::

   CREATE USER username WITH PASSWORD 'password';

Modyfikowanie istniejących użytkowników można przeprowadzać za pomocą
polecenia ``ALTER USER``:

::

   ALTER USER username WITH PASSWORD 'new_password';

Usuwanie Użytkowników
---------------------

Usuwanie użytkowników w PostgreSQL odbywa się za pomocą polecenia
``DROP USER``. Przykład:

::

   DROP USER username;

Jednakże usunięcie użytkownika nie powoduje automatycznego usunięcia
danych, które zostały przez niego wprowadzone. Dane te pozostają w bazie
danych i mogą być dalej dostępne dla innych użytkowników z odpowiednimi
uprawnieniami.

Zachowanie Danych po Usunięciu Użytkownika
------------------------------------------

Dane wprowadzone przez usuniętego użytkownika pozostają w bazie danych,
co jest ważne dla zapewnienia integralności i ciągłości danych. W
praktyce oznacza to, że:

-  Rekordy w tabelach nadal istnieją i są dostępne dla innych
   użytkowników z odpowiednimi uprawnieniami.

-  Metadane, takie jak informacje o autorze danych, mogą być zachowane w
   celach audytowych.

Przykłady scenariuszy, w których zachowanie danych po usunięciu
użytkownika jest istotne:

-  **Zmiany kadrowe** - gdy pracownik odchodzi z firmy, jego dane
   powinny pozostać w systemie.

-  **Reorganizacja projektów** - dane wprowadzone przez użytkownika mogą
   być ważne dla trwających projektów.

-  **Naruszenia bezpieczeństwa** - w przypadku konieczności szybkiego
   usunięcia użytkownika, dane pozostają nienaruszone.

Polityki Retencji Danych
------------------------

Organizacje mogą wdrażać polityki retencji danych, które określają, jak
długo dane wprowadzone przez użytkowników są przechowywane oraz w jakich
warunkach mogą być usuwane. Polityki te mogą obejmować:

-  Automatyczne usuwanie danych po określonym czasie.

-  Przeglądy i audyty danych w celu określenia ich dalszej przydatności.

-  Mechanizmy archiwizacji danych w celu ich późniejszego odzyskania,
   jeśli zajdzie taka potrzeba.

