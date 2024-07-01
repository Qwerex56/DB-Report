https://github.com/Qwerex56/DB-Report - Link do projektu aplikacji laboratoryjnej

Kontrola i buforowanie połączeń
===============================

Kontrola i buforowanie połączeń z bazą danych to kluczowe aspekty zarządzania bazami danych, które mają na celu optymalizację wydajności i zapewnienie niezawodności.

Kontrola połączeń z bazą danych:
--------------------------------
- Zarządzanie pulą połączeń: Technika ta pozwala aplikacjom na utrzymanie puli aktywnych połączeń z bazą danych, które są wielokrotnie używane. Poprzez efektywne zarządzanie pulą połączeń, aplikacje mogą minimalizować koszty związane z nawiązywaniem nowych połączeń, co przyczynia się do zwiększenia wydajności i efektywności systemu.

- Monitorowanie wydajności połączenia: Proces ten obejmuje śledzenie metryk związanych z połączeniem z bazą danych, takich jak czas odpowiedzi, błędy połączenia, ilość przesyłanych danych itp. Regularne monitorowanie tych metryk umożliwia szybkie wykrywanie problemów, co pozwala na ich natychmiastowe rozwiązanie i poprawę ogólnej wydajności systemu.

- Zarządzanie transakcjami: Kontrola nad transakcjami obejmuje precyzyjne określenie, kiedy i w jaki sposób transakcje są przetwarzane w bazie danych. Poprzez skuteczne zarządzanie transakcjami, można zapewnić spójność danych oraz uniknąć konfliktów. Przykładowo, dbając o to, aby operacje w ramach jednej transakcji były wykonywane jako jedna, niepodzielna jednostka pracy, zapewniamy integralność danych.

Buforowanie połączeń z bazą danych: 
-----------------------------------
- Buforowanie zapytań: Technika ta polega na przechowywaniu wyników często używanych zapytań w pamięci podręcznej. Dzięki temu, gdy aplikacja ponownie potrzebuje wyników tego samego zapytania, może je szybko pobrać z pamięci podręcznej, co znacząco przyspiesza czas odpowiedzi i zmniejsza obciążenie bazy danych.

- Buforowanie wyników: Podobnie jak buforowanie zapytań, buforowanie wyników polega na przechowywaniu wyników kosztownych zapytań w pamięci podręcznej na przyszłe użycie. To pozwala uniknąć ponownego przetwarzania zapytań, które wymagają skomplikowanych obliczeń lub dostępu do wielu tabel, co przyczynia się do poprawy wydajności systemu.

- Inwalidacja bufora: Proces inwalidacji bufora polega na usuwaniu danych z pamięci podręcznej, gdy stają się przestarzałe lub nieaktualne. Jest to istotny aspekt zarządzania pamięcią podręczną, który zapewnia, że przechowywane dane są zawsze aktualne. Mechanizmy inwalidacji bufora mogą być zautomatyzowane (np. usuwanie danych po określonym czasie) lub sterowane manualnie przez aplikację
