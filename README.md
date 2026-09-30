# Aktywny październik 2026 — pliki publiczne (GitHub Pages)

To są pliki, które wgrywasz do **publicznego repozytorium** obsługującego stronę dla uczestników.
Panel admina (`tabela_admin.html`) **NIE** trafia tutaj — zostaje prywatnie na Twoim komputerze
(zawiera token GitHub i klucze Supabase).

> Wgraj ten plik do repo jako **`README.md`**.

## Co wgrać do repo (root / główny folder)

| Plik | Co to jest |
|---|---|
| `index.html` | Tablica wyników na żywo (strona główna dla uczestników) |
| `results.json` | Dane wyników — panel admina będzie go nadpisywał |
| `Regulamin_Pazdziernik_2026.html` | Pełny regulamin (październik 2026) |
| `sciagawka-punkty-pazdziernik-2026.html` | Ściągawka „jak liczyć punkty" |
| `przewodnik-pazdziernik-2026.html` | Przewodnik „jak to działa" |
| `kalkulator.html` | Kalkulator punktów dla uczestników |
| `druzyny.html` | Skład drużyn (opcjonalnie) |

⛔ **Nigdy nie wgrywaj `tabela_admin.html`** — zawiera token GitHub i klucze Supabase.

## Konfiguracja GitHub Pages

1. Wgraj powyższe pliki do repo (główny folder)
2. Settings → Pages → Source: **Deploy from a branch**
3. Branch: **main**, folder: **/ (root)** → Save
4. Po chwili strona będzie pod adresem `https://palito1980.github.io/NAZWA-REPO/`

## Połączenie z panelem admina

Panel admina (`tabela_admin.html`, prywatny) publikuje `results.json` do tego repo przez token GitHub.
W konfiguracji panelu ustaw:

```javascript
const GH_REPO = 'palito1980/NAZWA-REPO';   // user/repo — bez URL, bez /rest/v1
```

Jeśli nazwa repo zmieniła się względem wrześniowej edycji — zaktualizuj `GH_REPO` w panelu,
inaczej publikacja pójdzie do starego repo.

**Ważne dla października:** w panelu ustaw **`challengeStart = '2026-10-01'`**.
Silnik rozpoznaje tygodnie po dacie, więc bez tego skrócony Tydzień 1 i cele dni nie policzą się poprawnie.

## Ważne — spójność linków

Strona główna (`index.html`) linkuje do regulaminu, ściągawki i przewodnika. Upewnij się, że nazwy
w repo są **dokładnie** takie jak w linkach (`Regulamin_Pazdziernik_2026.html`,
`sciagawka-punkty-pazdziernik-2026.html`, `przewodnik-pazdziernik-2026.html`). Jeśli wolisz krótkie
nazwy (`regulamin.html` itd.), zmień je i **w plikach, i w linkach** razem.

## Skład drużyn (październik)

- **Drużyna A** (7 osób): Kuba, Marta, Grześ, Gosia, Angela, Ewa, AziAzi
- **Drużyna B** (7 osób): Mariusz, Madzia, Jarek, Wiola, Wojtek, Natalia, Sabina (Bratowa)

Komplet drużyny = liczba osób × cel tygodnia → 35 dni w Tygodniach 2–5, **28 dni w skróconym Tygodniu 1**.

## Zasady October 2026 — co się zmieniło względem września

Pełne zasady: `Regulamin_Pazdziernik_2026.html`. Najważniejsze zmiany, które są już w silniku
(`index.html`, `kalkulator.html`, panel admina):

- **5 tygodni rozliczeniowych, Tydzień 1 skrócony.** T1 = 1–4.10 (cel **4** dni, liczone 4 najlepsze),
  T2–T5 = cel 5 (liczone 5 najlepszych). Kara i Komplet liczone względem celu danego tygodnia.
- **DSQ = 2 lub mniej aktywnych dni w tygodniu** (§6.1). Grasz dalej indywidualnie, punkty ujemne się kasują.
- **Bonus biegowy liczony z całego tygodnia** (§4.2) — wszystkie dni z biegiem, nie tylko wliczone do wyniku.
  Progi bez zmian: 2/3/4 dni = +10/+25/+50.
- **Bonus za regularność usunięty.**
- **Trening na czas w dwóch progach:** 25 pkt (30–49 min) / 40 pkt (50+ min), maks 1/dzień.
- **Minima:** bieg 3 km, spacer 3 km, rower 10 km, pływanie 800 m — z **5% tolerancją GPS**.
- **Rower stacjonarny** liczony jak zwykły rower (×0,3, min 10 km, limit 75 pkt = 50 km).
- **Weryfikacja:** mapa trasy dla aktywności na zewnątrz; bieżnia i rower stacjonarny wymagają
  **dwóch dowodów** (dystans z wyświetlacza + zapis z zegarka/opaski z czasem i tętnem);
  zdjęcie roweru **po zatrzymaniu, nie w trakcie jazdy**.
- **Prywatność:** na publicznej tablicy widać tylko nick, drużynę i wynik; dowody (zrzuty, mapy)
  zostają na grupie WhatsApp.

## Uwagi techniczne

- Nic w plikach publicznych nie zawiera sekretów — są bezpieczne w publicznym repo.
- Strona odświeża wyniki automatycznie co 60 s (tylko gdy karta jest aktywna) — bez bazy danych,
  bez zużycia transferu Supabase. GitHub Pages serwuje `results.json` za darmo.
- Jeśli zmieniasz zasady w trakcie edycji, zmień je **razem** w `index.html`, `kalkulator.html`
  i panelu admina — silnik musi być identyczny we wszystkich trzech.
