+++
title = "Post Pokazowy Markdown"
description = "Praktyczny wpis do sprawdzenia, jak renderują się elementy Markdowna w aktualnym motywie Hugo."
date = 2026-04-16T00:00:00Z
draft = true
tags = ["markdown", "hugo", "demo"]
categories = ["testy"]
+++

Ten wpis działa jako checklista wizualna Markdowna. Jeśli coś wygląda źle, ta strona pomaga szybko namierzyć problem.

---

## Nagłówki

### Nagłówek poziomu 3

#### Nagłówek poziomu 4

##### Nagłówek poziomu 5

## Wyróżnienia i formatowanie inline

- *Kursywa*
- **Pogrubienie**
- ***Pogrubienie + kursywa***
- ~~Przekreślenie~~
- Kod inline: `SELECT * FROM demo_table LIMIT 10;`

## Linki

- Link wewnętrzny: [O mnie](/pl/about/)
- Link wewnętrzny: [Kontakt](/pl/contact/)
- Link zewnętrzny: [Dokumentacja Hugo](https://gohugo.io/documentation/)

## Cytat

> Dobra dokumentacja zmniejsza liczbę pytań od użytkowników.
>
> Dobre przykłady zmniejszają nieporozumienia.

## Listy

### Lista nieuporządkowana

- Ingestia danych
- Transformacje danych
- Kontrole jakości
- Publikacja danych

### Lista uporządkowana

1. Zbierz wymagania
2. Zbuduj prostą wersję
3. Zweryfikuj wyniki
4. Iteruj

### Lista zagnieżdżona

- Platformy
  - Snowflake
  - Azure Synapse
  - PostgreSQL
- Języki
  - SQL
  - Python
  - R

### Task list

- [x] Dodane front matter
- [x] Dodane różne przykłady Markdowna
- [x] Sprawdzenie wyglądu w jasnym i ciemnym motywie
- [ ] Ewentualne poprawki stylów

## Tabela

| Funkcja | Przykład | Status |
| --- | --- | --- |
| Pogrubienie | `**tekst**` | Sprawdzone |
| Blok kodu | fenced code block | Sprawdzone |
| Przypis | `[^1]` | Sprawdzone |

## Bloki kodu

```bash
hugo server -D
```

```python
def validate_row_count(current_count: int, previous_count: int) -> bool:
    return current_count >= previous_count


print(validate_row_count(1024, 1000))
```

```json
{
  "pipeline": "daily_reporting",
  "source": "raw_events",
  "target": "analytics_mart",
  "refresh_minutes": 15
}
```

## Obraz

![Test zdjęcia profilowego](/images/avatar.jpg "Test renderowania avatara")

## Shortcode notice

{{< notice tip "Wskazówka" >}}
Używaj tej strony po każdej zmianie CSS, aby szybko sprawdzić, czy bloki Markdowna nadal renderują się poprawnie.
{{< /notice >}}

{{< notice warning "Uwaga" >}}
Jeśli punktorowanie list zniknie ponownie, najpierw sprawdź override CSS i zmiany w motywie.
{{< /notice >}}

## Shortcode mermaid

{{< mermaid >}}
flowchart TD
    A[Surowe dane] --> B[Staging]
    B --> C[Transformacje]
    C --> D[Jakość danych]
    D --> E[Raportowanie]
{{< /mermaid >}}

## Przypisy

To jest zdanie z przypisem.[^1]

[^1]: Przypisy są przydatne tam, gdzie komentarz nie powinien przerywać głównego toku tekstu.
