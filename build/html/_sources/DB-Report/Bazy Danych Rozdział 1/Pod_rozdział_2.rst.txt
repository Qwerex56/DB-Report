SQLite
===============================

SQLite to lekki system zarządzania relacyjnymi bazami danych, który jest często używany w aplikacjach mobilnych i na komputerach stacjonarnych oraz jest szeroko stosowana w różnych aplikacjach, od urządzeń mobilnych po duże systemy. Ze względu na swoją prostotę i niewielkie wymagania sprzętowe, SQLite może działać na różnych platformach z minimalnymi wymaganiami sprzętowymi. SQLite jest znany z tego, że jest wyjątkowo lekki i może działać na szerokiej gamie sprzętu. Nie wymaga dedykowanego serwera ani skomplikowanej konfiguracji, co sprawia, że jest idealny dla aplikacji o ograniczonych zasobach sprzętowych. Poniżej przedstawiono podstawowe  informacje dotyczące SQLite:

- Biblioteka SQLite może być zmniejszona do rozmiaru poniżej 300KiB, co czyni ją wyjątkowo kompaktową w porównaniu do innych systemów baz danych.

- Ma minimalne Zapotrzebowanie na Pamięć: 
SQLite może działać przy bardzo małym zużyciu pamięci stosu (stack) - około 4KiB oraz niewielkim zużyciu pamięci sterty (heap) - około 100KiB.

- Może działać bez Serwera:
SQLite nie wymaga serwera do działania. Baza danych SQLite jest zintegrowana z aplikacją, która uzyskuje dostęp do bazy danych, a aplikacje wchodzą w interakcję bezpośrednio z plikami bazy danych przechowywanymi na dysku. SQLite jest zaprojektowany tak, aby być jak najbardziej kompatybilnym z innymi silnikami baz danych SQL. Dzięki temu, programiści doświadczeni w SQL powinni znaleźć się w  dialekcie  SQLite gdyż raczej będzie intuicyjny i naturalny. SQLite może pomijać niektóre mniej znane funkcje SQL, ale jego dialekt może zawierać pewne ulepszenia, których nie znajdziemy w niektórych dokumentach standardowych.

Wymagania sprzętowe dla SQLite są dość minimalne, oczywiście im lepszy sprzęt tym lepsze można osiągnąć wydajności bazy danych. 

Urządzenia mobilne i wbudowane
Dla aplikacji mobilnych i wbudowanych, gdzie zasoby są ograniczone, SQLite jest doskonałym wyborem. Może działać na:

- Smartfonach i tabletach z systemem Android lub iOS.

- Systemach wbudowanych i IoT, takich jak Raspberry Pi czy Arduino.

- Telewizorach Smart TV i systemach rozrywkowych w samochodach.

- Komputery osobiste i serwery

SQLite może być również używany na komputerach osobistych i serwerach, gdzie zasoby nie są tak ograniczone. Może działać na:

- Komputerach z systemem operacyjnym Windows, macOS lub Linux.
- Serwerach, które mogą obsługiwać większe obciążenia i przechowywać większe bazy danych.

Chociaż SQLite może działać na różnorodnym sprzęcie, istnieją pewne optymalizacje, które można przeprowadzić, aby poprawić wydajność bazy danych. Warto jednak pomyśleć o doborze odpowiedniego sprzętu w zależności jak dużą bazę danych SQLite chce się stworzyć, warto pomyśleć o tym aby sprzęt miał odpowiednią ilość pamięci zarówno RAM jak i  przestrzeni dyskowej. Przy doborze sprzętu do tej bazy danych warto wziąć pod uwagę : 

- Pamięć RAM:
Im więcej pamięci RAM, tym lepiej, może to pomóc w przyspieszeniu operacji na bazie danych, ponieważ SQLite korzysta z pamięci do przechowywania tymczasowych tabel i buforowania danych.

- Przestrzeń dyskowa:
SQLite przechowuje całą bazę danych w jednym pliku, więc ważne jest, aby mieć wystarczającą ilość przestrzeni dyskowej, szczególnie jeśli spodziewamy się wzrostu danych. Warto zwrócić uwagę też na rodzaj dysku, dysk SSD będzie lepiej się sprawował, dzięki temu, że osiąga szybsze wyniki odczytu i zapisu. 

- Procesor:
Szybszy procesor może poprawić czas odpowiedzi bazy danych, szczególnie przy skomplikowanych zapytaniach i dużych zbiorach danych.

Przykładowe konfiguracje sprzętowe dla aplikacji mobilnych:
--------------------------------
Procesor: 4-rdzeniowy
RAM: 2 GB
Przestrzeń dyskowa: 32 GB
Dla aplikacji desktopowych:
Procesor: Intel Core i5 lub lepszy
RAM: 8 GB
Przestrzeń dyskowa: 256 GB SSD
Dla serwerów:
Procesor: Intel Xeon lub lepszy
RAM: 16 GB lub więcej
Przestrzeń dyskowa: 1 TB SSD lub więcej

SQLite jest niezwykle elastyczną bazą danych, która może działać na różnorodnym sprzęcie. Wybór odpowiedniego sprzętu zależy od wymagań aplikacji i oczekiwanej skali danych, ale zawsze warto zainwestować w lepszy sprzęt, aby zapewnić płynną pracę i szybką odpowiedź bazy danych.
