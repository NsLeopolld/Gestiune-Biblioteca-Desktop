# Prototip Figma

Link prototip: https://www.figma.com/proto/DE_COMPLETAT

Exporturile ecranelor (PNG/PDF) sunt în [`export/`](export/).

## Ecrane (frame-uri)

| Frame | Dimensiune |
|---|---|
| `0 Login` | 1440 × 900 |
| `1 Catalog` | 1440 × 900 |
| `2 Modal / Carte nouă` | 560 × 604 (overlay) |
| `2b Modal / Carte nouă - eroare` | 560 × 680 (overlay) |
| `3 Împrumut` | 1440 × 900 |
| `3b Retur` | 1440 × 900 |

- Catalog: bară laterală, căutare după titlu/autor/ISBN, filtre (gen, disponibilitate, an), buton Resetează, tabel cu numărul de exemplare disponibile, acțiuni Editează / Împrumută, paginare.
- Carte nouă (modal): Titlu*, Autor(i)*, ISBN*, An, Editură, Gen*, Nr. exemplare*, Limba; butoane Anulează / Salvează. Varianta „eroare” arată validarea ISBN-ului.
- Împrumut: alegerea cititorului, alegerea cărții și a exemplarului, verificarea disponibilității, termen 7/14/21 zile, data scadentă, Confirmă.
- Retur: împrumuturile active ale cititorului (la termen / întârziat), rezumat cu penalitatea (7 zile × 0,50 lei = 3,50 lei), Înregistrează returul.

## Legături în modul Prototype

| De la | Declanșator | Acțiune | Către |
|---|---|---|---|
| `0 Login` → „Intră în cont” | On click | Navigate to | `1 Catalog` |
| `1 Catalog` → „+ Carte nouă” | On click | Open overlay (centrat, fundal 40% negru, close on click outside) | `2 Modal / Carte nouă` |
| `1 Catalog` → Editează (creion) | On click | Open overlay | `2 Modal / Carte nouă` |
| `2 Modal` → Anulează / X | On click | Close overlay | - |
| `2 Modal` → Salvează | On click | Swap overlay | `2b Modal / Carte nouă - eroare` |
| `2b Modal` → Anulează / X | On click | Close overlay | - |
| `1 Catalog` → Împrumută (săgeți) | On click | Navigate to (Smart animate) | `3 Împrumut` |
| Meniu → „Împrumut / Retur” | On click | Navigate to | `3 Împrumut` |
| `3 Împrumut` → tab Retur | On click | Navigate to | `3b Retur` |
| `3b Retur` → tab Împrumut | On click | Navigate to | `3 Împrumut` |
| `3` / `3b` → „Înapoi la catalog”, Confirmă, Înregistrează returul, meniu „Catalog” | On click | Navigate to | `1 Catalog` |
| Meniu → Deconectare | On click | Navigate to | `0 Login` |

Punct de pornire al fluxului: `0 Login`.

## Export

1. Toate frame-urile: Export → PNG 2x, salvate în `export/`.
2. File → Export frames to PDF → `export/prototip.pdf`.
