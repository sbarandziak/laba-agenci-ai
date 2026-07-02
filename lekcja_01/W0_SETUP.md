# Warsztat 0: Przygotowanie środowiska

> 📋 **Skopiuj i wklej do swojego AI coding assistanta:**
> *"Przeczytaj plik W0_SETUP.md i pomóż mi przygotować środowisko. Sprawdź czy mam wszystko zainstalowane."*

## Co potrzebujesz

### 1. Node.js (wymagane)

Sprawdź czy masz — otwórz terminal i wpisz:
```
node --version
```

- Widzisz `v18.x.x` lub wyżej → masz, idź dalej
- Widzisz błąd → zainstaluj:
  1. Wejdź na **nodejs.org**
  2. Pobierz wersję **LTS** (duży zielony przycisk)
  3. Zainstaluj (next → next → finish)
  4. **Zamknij i otwórz terminal ponownie**
  5. Sprawdź: `node --version`

### 2. Klucz API Google AI Studio (wymagane, darmowe)

1. Wejdź na **aistudio.google.com**
2. Zaloguj się kontem Google
3. Kliknij **"Get API Key"** → **"Create API key"**
4. Skopiuj klucz i zapisz go w bezpiecznym miejscu
5. **Nie udostępniaj klucza nikomu!**

### 3. AI coding assistant (jedno z poniższych)

| Narzędzie | Jak uruchomić |
|-----------|---------------|
| **Claude Code** | Terminal → wpisz `claude` → wskaż folder |
| **Antigravity** | Otwórz folder w VS Code / Cursor z Antigravity |
| **Codex (GitHub)** | github.com → Open in Codex → blank workspace |

### 4. Pliki warsztatowe (ten folder)

Rozpakuj ZIP (lub sklonuj repo) do folderu na dysku, np:
```
C:\Users\TwojeImie\moj-agent\
```

## Weryfikacja — poproś AI coding assistanta

Wklej ten prompt do swojego AI assistanta:

```
Sprawdź moje środowisko:
1. Uruchom: node --version (potrzebuję 18+)
2. Uruchom: npm --version  
3. Stwórz pusty folder "moj-agent" i wejdź do niego
4. Uruchom: npm init -y
5. Zainstaluj: npm install next@latest react react-dom ai @ai-sdk/react @ai-sdk/google
6. Stwórz plik .env.local z treścią: GOOGLE_GENERATIVE_AI_API_KEY=tutaj_wklej_klucz
7. Powiedz mi czy wszystko się zainstalowało poprawnie

Jeśli coś nie działa — powiedz mi co zrobić.
```

## Oczekiwany rezultat

Po tym kroku masz:
- ✅ Node.js 18+
- ✅ Klucz API Google (w .env.local)
- ✅ Folder `moj-agent` z zainstalowanymi pakietami
- ✅ AI coding assistant gotowy do pracy

**Jeśli masz to wszystko → przejdź do W1_CHATBOT.md**

---

## Jak samodzielnie uruchomić agenta (po warsztatach)

Gdy chcesz wrócić do swojego agenta po zajęciach:

```
1. Otwórz terminal
2. Wejdź do folderu projektu:    cd moj-agent
3. Uruchom agenta:               npm run dev
4. Otwórz przeglądarkę:          http://localhost:3000
```

Żeby zatrzymać agenta: `Ctrl + C` w terminalu.

Żeby uruchomić ponownie — powtórz krok 3.
