# Warsztat 4: Dashboard — centrum dowodzenia agenta

> 📋 **Skopiuj i wklej do AI assistanta:**
> *"Przeczytaj plik W4_DASHBOARD.md i zbuduj profesjonalny dashboard jako stronę startową agenta"*

## Cel
Zbuduj "centrum dowodzenia" — stronę startową która automatycznie ładuje prawdziwe dane: pogodę, kursy walut, nadchodzące święta. Profesjonalny produkt, nie prototyp.

## Kontekst
Po Warsztatach 1-3 masz agenta z 10 narzędziami, stroną ReAct (/react), asystentem podróży (/travel) i error handling. Teraz zamykamy to wszystko w profesjonalnym dashboardzie.

## Co budujemy

### 1. Strona: `app/dashboard/page.tsx`

```
Dashboard to NIE czat — to panel informacyjny z kartami.

Przy ładowaniu strony automatycznie pobierz dane:
1. getWeather("Warszawa") — lub miasto z ustawień / geolokalizacji
2. getExchangeRate("EUR") + getExchangeRate("USD")
3. getHolidays("PL", 2026) → filtruj na nadchodzące
4. currentDateTime → data, dzień tygodnia

Dane pobieraj bezpośrednio z API (fetch w server component
lub useEffect) — NIE przez agenta, żeby było szybko.
Użyj tych samych URL-i co w narzędziach z Warsztatu 1:
- Open-Meteo: https://api.open-meteo.com/v1/forecast?...
- NBP: https://api.nbp.pl/api/exchangerates/rates/a/EUR/?format=json
- Nager.Date: https://date.nager.at/api/v3/publicholidays/2026/PL

Layout:

┌──────────────────────────────────────────────────┐
│  🌅 Dzień dobry! Dziś: niedziela, 6 lipca 2026  │
├──────────────────────┬───────────────────────────┤
│ 🌤️ POGODA            │ 💶 KURSY WALUT            │
│ Warszawa             │                           │
│ ☀️ 24°C              │ EUR: 4.2815 PLN  ↑ 0.02  │
│ Wiatr: 12 km/h       │ USD: 3.9120 PLN  ↓ 0.01  │
│ Wilgotność: 45%      │                           │
│                      │ Kurs z: 2026-07-04 (NBP)  │
├──────────────────────┼───────────────────────────┤
│ 📅 NADCHODZĄCE ŚWIĘTA│ 🤖 SZYBKIE AKCJE          │
│                      │                           │
│ 15 sie — Wniebowzię- │ [🌍 Zaplanuj podróż]     │
│         cie NMP      │ [🔄 Agent ReAct]          │
│ 1 lis — Wszystkich   │ [💬 Chat z agentem]       │
│         Świętych     │ [🧠 Tryb myślenia]       │
│ 11 lis — Niepodległo-│ [🎨 Generator grafik]     │
│          ści         │ [📚 Słownik AI]           │
│                      │                           │
│ Następne za: 40 dni  │                           │
└──────────────────────┴───────────────────────────┘

WAŻNE: Dane w kartach to PRAWDZIWE dane pobrane z API,
nie hardcoded!
```

### 2. Styl dashboardu

```
- Ciemny motyw (spójny z resztą)
- Karty z glassmorphism (backdrop-filter: blur,
  delikatny border, półprzezroczyste tło)
- Animacja fade-in kart (opacity 0→1, translate-y)
- Loading skeleton gdy dane się ładują
  (szare pulsujące placeholdery)
- Responsywny: na telefonie karty jedna pod drugą
- Ikona odświeżania w prawym górnym rogu → przeładowuje dane

Kolory kart:
- Pogoda: gradient blue → cyan (ciemny)
- Waluty: gradient green → emerald (ciemny)
- Święta: gradient orange → amber (ciemny)
- Szybkie akcje: gradient purple → pink (ciemny)
```

### 3. Szybkie akcje → otwierają odpowiednią stronę

```
Przyciski "Szybkie akcje" — linkuj TYLKO do stron które istnieją:
- 🌍 Zaplanuj podróż → /travel
- 🔄 Agent ReAct → /react
- 💬 Chat z agentem → / (strona główna z czatem)
- 🧠 Tryb myślenia → /think
- 🎨 Generator grafik → /generate
- 📚 Słownik AI → /fewshot

Każdy przycisk to link do odpowiedniej strony.
```

### 4. Auto-refresh

```
- Dane pogodowe odświeżaj co 15 minut (setInterval)
- Kursy walut odświeżaj co godzinę (NBP aktualizuje raz dziennie)
- Pokazuj "Ostatnia aktualizacja: 10:30" przy każdej karcie
- Przycisk 🔄 ręczne odświeżenie wszystkich danych
```

### 5. Nawigacja — dashboard jako strona startowa

```
Zmień routing:
- / → Dashboard (strona startowa)
- /chat → Chat z personą (przenieś obecną stronę główną)
- /think → Chain of Thought (z L2)
- /fewshot → Słownik AI (z L2)
- /format → Formatowanie (z L2)
- /search → Wyszukiwarka Google (z L3)
- /generate → Generator grafik (z L3)
- /vision → Analiza obrazów (z L3)
- /agent → Agent multi-tool (z L3)
- /react → Agent ReAct (z L4 W1)
- /travel → Asystent podróży (z L4 W2)

Nawigacja powinna być:
- Sidebar na desktopie (zawsze widoczny)
- Hamburger menu na telefonie
- Aktywna strona podświetlona
- Dashboard ma ikonę 🏠 i jest na górze
```

## Oczekiwany rezultat
- Dashboard ładuje się z prawdziwymi danymi w ~1 sekundę
- Pogoda, waluty, święta — wszystko aktualne
- Szybkie akcje prowadzą do odpowiednich stron
- Profesjonalny, ładny layout z animacjami
- Auto-refresh

## Test

1. Otwórz dashboard → pogoda, waluty, święta załadowane
2. Sprawdź pogodę na telefonie → ta sama temperatura co na dashboardzie
3. Sprawdź kurs euro w banku → ten sam co na dashboardzie (NBP)
4. Kliknij "Zaplanuj podróż" → przenosi do /travel
5. Kliknij "Agent ReAct" → przenosi do /react
6. Kliknij "Generator grafik" → przenosi do /generate
7. Kliknij 🔄 → dane się odświeżają
8. Otwórz na telefonie → responsywny layout

## Podsumowanie Lekcji 4

Po tych warsztatach masz:
- ✅ **10 narzędzi** (readWebPage i generateImage z L3 + 8 nowych: calculator, currentDateTime, getWeather, getExchangeRate, getHolidays, searchWikipedia, saveNote, getNotes)
- ✅ **Agent ReAct** który autonomicznie planuje i realizuje cele
- ✅ **Asystent podróży** który planuje wyjazdy z prawdziwymi danymi
- ✅ **Error handling** i zabezpieczenia z panelem diagnostycznym
- ✅ **Dashboard** z live data — pogoda, waluty, święta
- ✅ **Pełna nawigacja** z 11 stronami

**Żadnych mocków. Żadnych dodatkowych kluczy. Wszystko prawdziwe.**

Twój agent przeszedł drogę od "Cześć, kim jesteś?" do centrum dowodzenia z 10 narzędziami i prawdziwymi danymi.

## Praca domowa

1. **Nowe miasto na dashboardzie** — zmień domyślne miasto pogodowe
   na swoje (lub dodaj wybór miasta)
2. **Nowa waluta** — dodaj trzecią walutę do dashboardu
   (np. GBP, CHF, CZK)
3. **Test z rodziną** — pokaż dashboard i asystenta podróży
   komuś spoza IT. Zapisz reakcję.
4. **BONUS:** Dodaj do dashboardu kartę "Cytat dnia"
   z darmowego API (api.quotable.io lub podobne)
