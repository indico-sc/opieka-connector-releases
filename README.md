# Konektory Opieka techniczna

## Wydanie 2026-09-05

- [Joomla 0.1.18 — Joomla 3, 4, 5, 6](joomla/0.1.18/pkg_opiekaconnector-joomla.zip)
- [WordPress 0.1.4 — WordPress 6, 7](wordpress/0.1.4/opieka-connector-wordpress.zip)

Konektory wymagają PHP co najmniej 7.4; wymagania samego CMS mogą być wyższe. Obsługa starszego CMS nie zastępuje jego aktualizacji bezpieczeństwa.

Przetestowane środowiska: Joomla 3.10.11/PHP 7.4, Joomla 4.4.14/PHP 8.1, Joomla 5.4.8/PHP 8.3, Joomla 6.1.3/PHP 8.4, WordPress 6.0.3/PHP 7.4 i WordPress 7.1/PHP 8.3. Nie jest to deklaracja przetestowania każdej historycznej wersji punktowej ani obsługi PHP starszego niż 7.4.

Joomla 3 używa `https://domena/index.php/v1/opieka/`. Joomla 4–6 używa `https://domena/api/index.php/v1/opieka/`. W instalacji w podkatalogu należy zachować jego prefiks. Dokładny endpoint znajduje się w ustawieniach pluginu systemowego. WordPress zachowuje `/wp-json/opieka/v1/`.

## Strumień aktualizacji

- [Podpisany manifest](manifest.json): Ed25519, SHA-256 i rozmiar paczek, ograniczony czas ważności.
- [Natywny strumień Joomla](joomla-stable.xml): rekordy dla linii 3–6, jawne `client=0`, wymagania PHP i SHA-256.
- WordPress weryfikuje podpis manifestu i pobraną paczkę; nie włącza samoczynnych aktualizacji konektora.
- Manifest należy odnowić przed datą `expiresAt`; wygasły manifest nie jest akceptowany przez weryfikatory podpisu.

Adresy zawierające wersję są niezmienne. Starsze pliki ZIP w katalogu głównym pozostawiono dla wcześniej zapisanych, wstrzymanych przebiegów; do nowych instalacji używaj linków powyżej lub podpisanego manifestu.

## Najważniejsze poprawki

- Zgodny instalator i podpisane API dla Joomla 3; wspólny kod obsługi API z Joomla 4–6.
- Obsługa różnic zdarzeń Joomla 4 i Joomla 5/6.
- Kontrolki konfiguracji i poprawny endpoint dla każdej linii Joomla.
- Zachowanie danych dostępowych przy ponownej instalacji.
- WordPress: obsługa PHP 7.4, zachowanie historii przy reaktywacji, komplet zależności REST i zachowanie aktywacji po aktualizacji pojedynczej wtyczki.
- Naprawiona identyfikacja pakietu w natywnym strumieniu Joomla.

Testy objęły instalację, ponowną instalację, podpisane health/inventory/events, odrzucanie błędnego podpisu i powtórzonego nonce oraz wymóg HTTPS. Strumień Joomla przeszedł natywne wykrywanie, pobieranie i instalację aktualizacji w czterech liniach. WordPress przeszedł odrzucanie zmienionego manifestu i paczki, aktualizację konektora 0.1.3 → 0.1.4 w testowej instancji 7.1 oraz podpisaną aktualizację testowej wtyczki w 6.0.3 i 7.1. Testy aktualizacji używały izolowanych transportów testowych, a nie stron klientów.
