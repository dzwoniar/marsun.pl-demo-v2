# Marsun — landing B2B z kalkulatorem kosztu awarii

Drugi wariant statycznego prototypu strony dla dystrybutora sprzętu OZE. Łączy prezentację oferty dla instalatorów z interaktywną ilustracją kosztu awarii i potencjalnej oszczędności wynikającej ze wsparcia serwisowego.

To demonstracja interfejsu i komunikacji oferty. Obsługa klientów B2B, zamówień i szkoleń nie jest częścią kodu.

## Funkcje

- Responsywne sekcje problemu, oferty, porównania, procesu współpracy, opinii i FAQ.
- Kalkulator aktualizowany suwakiem od 1 do 10 awarii.
- Rozwijane FAQ oraz nawigacja między sekcjami strony.
- Animacje wejścia sekcji przez `IntersectionObserver`.

## Uruchomienie lokalne

Wymagania: współczesna przeglądarka i Python 3 do prostego serwera plików.

```bash
git clone https://github.com/dzwoniar/marsun.pl-demo-v2.git
cd marsun.pl-demo-v2
python -m http.server 8000 --bind 127.0.0.1
```

Otwórz [http://localhost:8000](http://localhost:8000). Na Windows alternatywą jest `py -m http.server 8000 --bind 127.0.0.1`. Zatrzymaj serwer przez `Ctrl+C`. Nie ma paczek do instalacji ani kroku budowania.

## Architektura

```text
.
├── index.html   # wszystkie sekcje, CSS i JavaScript
└── README.md
```

[index.html](index.html) zawiera całą implementację: statyczne dane oferty w HTML, osadzony CSS oraz skrypt animacji i kalkulatora. Stos to HTML5, CSS i JavaScript bez frameworka. Google Fonts dostarcza DM Sans i Playfair Display; fonty wymagają połączenia z zewnętrzną usługą.

Funkcja `updateCalc(v)` wykonuje obliczenia wyłącznie w przeglądarce:

```text
koszt = zaokrąglenie(liczba_awarii × 15 000 zł)
oszczędność = zaokrąglenie(koszt × 0,85)
```

Wyniki trafiają do elementów `calc-loss` i `calc-save`, z formatowaniem `pl-PL`. Stała kwota i współczynnik są założeniami demonstracji, a nie danymi pobieranymi z systemu serwisowego.

## Ograniczenia prototypu

- Kalkulator nie wykonuje wyceny ani analizy rzeczywistych awarii; nie zapisuje wyników i nie korzysta z API.
- Końcowe CTA do szkolenia i PDF mają `href="#"`. W repozytorium nie ma pliku PDF, rejestracji ani płatności.
- Opisywana w treści rejestracja B2B i weryfikacja NIP przez API GUS nie są zaimplementowane.
- Deklaracje handlowe, opinie i liczby na stronie są treścią prototypu; dokumentacja nie potwierdza ich aktualności.
- Nie ma backendu, bazy danych, zmiennych środowiskowych ani skonfigurowanych testów automatycznych.

## Powiązane projekty

[Pierwszy wariant strony](https://github.com/dzwoniar/marsun.pl-demo) nie zawiera kalkulatora. [Landing lead magnetu v2](https://github.com/dzwoniar/marsun.pl-demo-lead-v2) pokazuje osobną ścieżkę formularza kontaktowego.
