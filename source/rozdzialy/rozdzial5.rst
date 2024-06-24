Replikacja
==========
Replikacja danych to metoda duplikowania informacji pomiędzy różnymi serwerami baz danych. 
Dzięki replikacji możemy:
- Zwiększyć skalowalność – obciążenie można rozdzielić między wiele serwerów. Operacje takie jak zapisywanie i aktualizowanie rekordów są wykonywane na jednym serwerze, podczas gdy pobieranie i przeszukiwanie danych są realizowane na innym.
- Poprawić bezpieczeństwo – poprzez replikację tworzymy kopię istniejącej bazy danych produkcyjnej. Choć nie zabezpieczy nas to przed operacjami typu DROP TABLE, może to być pomocne w przypadku awarii sprzętowej głównego serwera.
- Ułatwić analizę – złożone operacje analityczne, różne przeliczenia i analizy statystyczne mogą być przeprowadzane na dedykowanym serwerze, bez obciążania głównej bazy danych.
- Zapewnić separację – możemy udostępnić kopię bazy danych produkcyjnej dla programistów lub testerów, umożliwiając im pracę na kopii bazy.

Mechanizmy replikacji
---------------------
Replikacja w bazach danych odnosi się do procesu kopiowania i dystrybucji danych i obiektów z jednej bazy danych do innej, a następnie synchronizacji obu baz danych w celu utrzymania ich spójności.
Proces ten jest dość prosty. Główny serwer (master) prowadzi dziennik operacji, wykorzystując do tego pliki binarne zwane bin-logami, które zawierają instrukcje wykonane przez mastera. Te pliki są następnie odczytywane przez serwer zapasowy (slave), który wykonuje zapytania zawarte w bin-logach, co skutkuje dodawaniem nowych rekordów do bazy danych. W efekcie powstają dwie identyczne bazy danych. Po ustawieniu replikacji na serwerze master, uruchamiany jest dodatkowy wątek, który ma za zadanie wysyłać bin-logi do serwerów slave. Serwer zapasowy z kolei uruchamia dwa wątki: jeden do odczytu bin-logów i drugi do ich wykonania.
- Wątek I/O (Input/Output) - zajmuje się odbieraniem dziennika od serwera głównego i zapisywaniem go w plikach tymczasowych relay-log.
- Wątek SQL - parsuje te pliki i wykonuje zapytania do bazy danych.
W skrócie, mechanizm replikacji MySQL polega na tym, że serwer główny rejestruje swoje działania, a serwer zapasowy odtwarza te działania, tworząc kopię bazy danych.

Oprogramowanie i zaimplementowane mechanizmy replikacji
-------------------------------------------------------
- Replikacja oparta na zapisie (Write-Ahead Logging): Ten mechanizm jest powszechnie stosowany w systemach baz danych, takich jak PostgreSQL. Polega na rejestrowaniu transakcji w dzienniku zapisu przed ich zastosowaniem, a następnie replikacji dziennika na serwery repliki.
- Replikacja oparta na zrzutach (Snapshot-Based Replication): Systemy, takie jak Apache Cassandra, wykorzystują replikację opartą na zrzutach. Polega to na tworzeniu zrzutów stanu bazy danych w określonych odstępach czasu i replikacji ich na serwery repliki.
- Replikacja oparta na transakcjach (Transaction-Based Replication): W tym modelu każda transakcja jest replikowana na serwery repliki, co jest przydatne w systemach wymagających silnej spójności, np. Google Spanner.
- Replikacja asynchroniczna i synchroniczna: W replikacji asynchronicznej dane są najpierw zapisywane do głównej bazy danych, a następnie replikowane na serwery repliki. W replikacji synchronicznej dane są zapisywane jednocześnie do głównej bazy danych i serwerów repliki.
- Replikacja dwukierunkowa (Bi-Directional Replication): Pozwala na wprowadzanie zmian na dowolnym serwerze repliki, które są następnie replikowane na pozostałe serwery, co jest przydatne w przypadku wysokiej dostępności i tolerancji na awarie.

PostgreSQL oferuje różne typy replikacji, w tym replikację opartą na zapisie (Write-Ahead Logging), replikację asynchroniczną i synchroniczną oraz replikację logiczną. Replikacja oparta na zapisie (WAL) gwarantuje odporność na awarie poprzez zapisywanie zmian w bazie danych do dziennika zapisu przed ich zastosowaniem, który jest replikowany na serwery repliki. PostgreSQL obsługuje zarówno replikację asynchroniczną, gdzie dane są najpierw zapisywane do głównej bazy danych, a następnie replikowane, jak i replikację synchroniczną, gdzie dane są zapisywane jednocześnie do głównej bazy danych i serwerów repliki. Dodatkowo, replikacja logiczna pozwala na replikację wybranych tabel lub baz danych zamiast całego klastra, co jest przydatne zwłaszcza w przypadku dużych baz danych, gdzie replikacja całego klastra byłaby nieefektywna.

Plusy i minusy replikacji
-------------------------
Plusy:

- Poprawa wydajności i dostępności: Replikacja danych pozwala na dystrybucję obciążenia zapytań pomiędzy wiele serwerów, co zwiększa wydajność systemu. Użytkownicy mogą wysyłać zapytania do najbliższego serwera repliki, co skraca czas odpowiedzi. Ponadto, jeśli jeden serwer ulegnie awarii, inne serwery repliki mogą nadal obsługiwać zapytania, co zwiększa dostępność systemu.
- Bezpieczeństwo danych: Replikacja jest również kluczowym elementem strategii tworzenia kopii zapasowych i odzyskiwania danych. Jeśli główna baza danych ulegnie awarii, replika może zostać użyta do przywrócenia danych.
- Dystrybucja danych: Replikacja umożliwia dystrybucję danych do oddzielnych lokalizacji geograficznych. Na przykład, globalna firma może chcieć replikować dane między swoimi lokalizacjami w różnych krajach, aby lokalni użytkownicy mogli szybko i łatwo uzyskać dostęp do potrzebnych informacji.
- Analiza i raportowanie: Repliki danych mogą być używane do celów analitycznych i raportowych. Dzięki temu operacje te nie wpływają na wydajność głównej bazy danych obsługującej transakcje.

Minusy:

- Nie daje nam pewności, że po przeprowadzeniu operacji, dane z serwera głównego będą poprawnie przeniesione na serwer zapasowy
- Nie zapewnia ochrony przed operacjami niosącymi poważne konsekwencje - takimi jak DROP TABLE
