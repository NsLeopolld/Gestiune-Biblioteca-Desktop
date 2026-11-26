# Prototip Figma

Link prototip: [Figma prototype](https://www.figma.com/design/BhxGQDExxZLql5R8fKJJ7T/Gestionarea-unei-biblioteci?m=auto&t=HbYTlRVbfFy0hidi-1)

Exporturile ecranelor (PNG/PDF) sunt în [`export/`](export/).

## Ecrane (frame-uri)

| Frame | Export | Conținut |
|---|---|---|
| `Login` | [Login.png](<export/Login.png>) | autentificare bibliotecar |
| `Catalog` | [Catalog.png](<export/Catalog.png>) | catalogul principal: bară laterală, căutare după titlu/autor/ISBN, filtre (gen, disponibilitate, an), buton Resetează, tabel cu exemplarele disponibile, acțiuni Editează / Împrumută, paginare |
| `New Book` | [New Book.png](<export/New Book.png>) | fereastra modală „Carte nouă”: Titlu*, Autor(i)*, ISBN*, An, Editură, Gen*, Nr. exemplare*, Limba; Anulează / Salvează |
| `New Book Error` | [New Book Error.png](<export/New Book Error.png>) | aceeași fereastră, cu eroare de validare la ISBN |
| `Loan` | [Loan.png](<export/Loan.png>) | împrumut: alegerea cititorului, a cărții și a exemplarului, verificarea disponibilității, termen 7/14/21 zile, data scadentă, Confirmă |
| `Return` | [Return.png](<export/Return.png>) | retur: împrumuturile active (la termen / întârziat), penalitatea (7 zile × 0,50 lei = 3,50 lei), Înregistrează returul |

Toate ecranele, într-un singur PDF: [Gestionarea unei biblioteci.pdf](<export/Gestionarea unei biblioteci.pdf>)

## Legături în modul Prototype

| De la | Declanșator | Acțiune | Către |
|---|---|---|---|
| `Login` → „Intră în cont” | On click | Navigate to | `Catalog` |
| `Catalog` → „+ Carte nouă” | On click | Open overlay (centrat, fundal 40% negru, close on click outside) | `New Book` |
| `Catalog` → Editează (creion) | On click | Open overlay | `New Book` |
| `New Book` → Anulează / X | On click | Close overlay | - |
| `New Book` → Salvează | On click | Swap overlay | `New Book Error` |
| `New Book Error` → Anulează / X | On click | Close overlay | - |
| `Catalog` → Împrumută (săgeți) | On click | Navigate to (Smart animate) | `Loan` |
| Meniu → „Împrumut / Retur” | On click | Navigate to | `Loan` |
| `Loan` → tab Retur | On click | Navigate to | `Return` |
| `Return` → tab Împrumut | On click | Navigate to | `Loan` |
| `Loan` / `Return` → „Înapoi la catalog”, Confirmă, Înregistrează returul, meniu „Catalog” | On click | Navigate to | `Catalog` |
| Meniu → Deconectare | On click | Navigate to | `Login` |

Punct de pornire al fluxului: `Login`.

## Export

1. Toate frame-urile: Export → PNG 2x, salvate în `export/`.
2. File → Export frames to PDF → `export/Gestionarea unei biblioteci.pdf`.
