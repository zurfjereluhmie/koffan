# System Tłumaczeń (i18n)

## Dodawanie nowego języka

### 1. Utwórz plik JSON

Skopiuj `en.json` jako szablon i utwórz nowy plik, np. `de.json` dla niemieckiego:

```bash
cp i18n/en.json i18n/de.json
```

### 2. Edytuj metadane

Na początku pliku zmień sekcję `meta`:

```json
{
  "meta": {
    "code": "de",        // Kod ISO 639-1 (2 litery)
    "name": "Deutsch",   // Nazwa języka w tym języku
    "flag": "DE"         // Kod kraju (wyświetlany jako flaga)
  },
  ...
}
```

### 3. Przetłumacz wszystkie klucze

Przetłumacz wartości (NIE klucze!) w każdej sekcji:

- `common` - przyciski: Dodaj, Anuluj, Zapisz, Usuń, Edytuj, Zamknij
- `nav` - nawigacja: Ustawienia, Wyloguj
- `list` - lista: tytuł, pusta lista, lista zakupów, gotowe, Kupione
- `items` - produkty: Co kupić?, Notatka, nazwa, nowy produkt, wybierz sekcję
- `sections` - sekcje: tytuł, nowa sekcja, lista sekcji, zarządzaj, wybierz, brak sekcji
- `actions` - akcje: w górę, w dół, przenieś, niepewne, pewne
- `settings` - ustawienia: tytuł, język
- `login` - logowanie: tytuł, podtytuł, hasło, placeholder, przycisk, błąd
- `confirm` - potwierdzenia: usunąć item, usunąć sekcje (z parametrami `{{name}}`, `{{count}}`)

### 4. Przebuduj aplikację

Pliki JSON są embedowane w binarkę, więc po dodaniu/zmianie tłumaczeń:

```bash
go build -o shopping-list-go
./shopping-list-go
```

### 5. Gotowe!

Nowy język automatycznie pojawi się w selektorze w Ustawieniach.

---

## Struktura pliku tłumaczeń

```json
{
  "meta": {
    "code": "xx",
    "name": "Nazwa języka",
    "flag": "XX"
  },
  "common": {
    "add": "...",
    "cancel": "...",
    "save": "...",
    "delete": "...",
    "edit": "...",
    "close": "..."
  },
  "nav": {
    "settings": "...",
    "logout": "..."
  },
  "list": {
    "title": "...",
    "empty_list": "...",
    "shopping_list": "...",
    "completed": "...",
    "bought": "..."
  },
  "items": {
    "what_to_buy": "...",
    "note": "...",
    "note_optional": "...",
    "name": "...",
    "new_product": "...",
    "select_section": "...",
    "section": "..."
  },
  "sections": {
    "title": "...",
    "new_section": "...",
    "section_list": "...",
    "manage": "...",
    "select": "...",
    "no_sections": "...",
    "add_first_section": "..."
  },
  "actions": {
    "move_up": "...",
    "move_down": "...",
    "move": "...",
    "uncertain": "...",
    "certain": "...",
    "remove_mark": "...",
    "mark_uncertain": "..."
  },
  "settings": {
    "title": "...",
    "language": "...",
    "coming_soon": "..."
  },
  "login": {
    "title": "...",
    "subtitle": "...",
    "password": "...",
    "password_placeholder": "...",
    "submit": "...",
    "error_invalid": "..."
  },
  "confirm": {
    "delete_item": "... \"{{name}}\"?",
    "delete_sections": "... {{count}} ...?",
    "delete_section": "... '{{name}}'?"
  }
}
```

## Kody języków (ISO 639-1)

| Kod | Język |
|-----|-------|
| pl | Polski |
| en | English |
| de | Deutsch |
| es | Español |
| fr | Français |
| it | Italiano |
| pt | Português |
| uk | Українська |
| cs | Čeština |
| sk | Slovenčina |
| ru | Русский |
| nl | Nederlands |
| sv | Svenska |
| no | Norsk |
| da | Dansk |
| fi | Suomi |
| ja | 日本語 |
| ko | 한국어 |
| zh | 中文 |

## Parametry w tłumaczeniach

Niektóre teksty zawierają parametry w formacie `{{param}}`:

- `{{name}}` - nazwa elementu (item, sekcja)
- `{{count}}` - liczba elementów

Przykład:
```json
"delete_item": "Delete \"{{name}}\"?"
```

W kodzie JS wywoływane jako:
```javascript
t('confirm.delete_item', { name: 'Mleko' })
// Wynik: Delete "Mleko"?
```
