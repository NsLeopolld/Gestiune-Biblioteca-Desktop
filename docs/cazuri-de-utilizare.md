# Cazuri de utilizare - Gestionarea unei biblioteci

Diagrama: [`../diagrams/use-case.png`](../diagrams/use-case.png) (sursă: [`use-case.dot`](../diagrams/use-case.dot), export PDF: [`use-case.pdf`](../diagrams/use-case.pdf)).

## Actori

| Actor | Rol |
|---|---|
| Bibliotecar | Actor principal. Gestionează fondul de carte, cititorii, împrumuturile și retururile. |
| Administrator | Specializare a Bibliotecarului (generalizare UML): are toate drepturile acestuia, plus gestionarea conturilor de bibliotecar. |
| Cititor | Actor secundar. Nu folosește aplicația direct, dar participă la împrumut și retur (prezintă legitimația, primește/predă cartea). |

## Lista cazurilor de utilizare

| ID | Caz de utilizare | Actor | Relații |
|---|---|---|---|
| UC1 | Autentificare | Bibliotecar | - |
| UC2 | Vizualizează catalogul cărților | Bibliotecar | extins de UC3 |
| UC3 | Filtrează / caută cărți | Bibliotecar | «extend» UC2 |
| UC4 | Înregistrează carte nouă | Bibliotecar | «include» UC6 |
| UC5 | Editează / șterge carte | Bibliotecar | «include» UC6 |
| UC6 | Validează datele cărții | - | inclus în UC4, UC5 |
| UC7 | Gestionează cititori | Bibliotecar | - |
| UC8 | Înregistrează împrumut | Bibliotecar, Cititor | «include» UC9 |
| UC9 | Verifică disponibilitatea exemplarului | - | inclus în UC8 |
| UC10 | Înregistrează retur | Bibliotecar, Cititor | extins de UC11 |
| UC11 | Calculează penalitate de întârziere | - | «extend» UC10, condiție: `[întârziere]` |
| UC12 | Vizualizează împrumuturi active / restante | Bibliotecar | - |
| UC13 | Gestionează conturile bibliotecarilor | Administrator | - |

## Scenarii principale

### UC2 + UC3 - Consultarea catalogului cu filtrare
- Precondiție: bibliotecarul este autentificat.
- Flux principal:
  1. Bibliotecarul deschide ecranul *Catalog*.
  2. Sistemul afișează lista cărților (titlu, autor, ISBN, gen, an, exemplare disponibile/total).
  3. *(extensie UC3)* Bibliotecarul introduce un text în câmpul de căutare și/sau alege filtre (gen, disponibilitate).
  4. Sistemul actualizează lista în timp real.
- Flux alternativ 3a: niciun rezultat → sistemul afișează mesajul „Nu s-au găsit cărți” și butonul „Resetează filtrele”.

### UC4 - Înregistrarea unei cărți noi
- Precondiție: bibliotecarul este în ecranul *Catalog*.
- Flux principal:
  1. Bibliotecarul apasă „+ Carte nouă”; se deschide fereastra modală *Carte nouă*.
  2. Completează: titlu, autor(i), ISBN, editură, an, gen, număr de exemplare.
  3. Apasă „Salvează”.
  4. *(include UC6)* Sistemul validează câmpurile obligatorii și formatul ISBN (10/13 cifre, cifră de control) și verifică unicitatea ISBN-ului.
  5. Sistemul salvează cartea, închide fereastra și afișează cartea nouă în catalog.
- Flux alternativ 4a: date invalide → câmpurile greșite sunt marcate cu roșu și cu un mesaj explicativ; fereastra rămâne deschisă.
- Flux alternativ 4b: ISBN existent → sistemul propune creșterea numărului de exemplare pentru cartea existentă.
- Flux alternativ 3a: „Anulează” → fereastra se închide fără salvare.

### UC8 - Înregistrarea unui împrumut
- Precondiție: cititorul este înregistrat; cartea există în catalog.
- Flux principal:
  1. Bibliotecarul selectează cartea în catalog și apasă „Împrumută” (sau deschide fereastra *Împrumut / Retur*, tab-ul *Împrumut*).
  2. Caută cititorul după nume sau număr de legitimație.
  3. *(include UC9)* Sistemul verifică dacă există cel puțin un exemplar disponibil și dacă cititorul nu are restanțe/limita de împrumuturi atinsă.
  4. Sistemul propune data scadentă (implicit +14 zile); bibliotecarul o poate ajusta.
  5. Bibliotecarul confirmă; sistemul salvează împrumutul și scade numărul de exemplare disponibile.
- Flux alternativ 3a: niciun exemplar disponibil → mesaj de eroare, butonul „Confirmă” este dezactivat.
- Flux alternativ 3b: cititorul are împrumuturi restante → avertizare; împrumutul este blocat până la retur.

### UC10 + UC11 - Înregistrarea unui retur
- Flux principal:
  1. Bibliotecarul deschide tab-ul *Retur* și caută împrumutul (după cititor sau carte).
  2. Selectează împrumutul și apasă „Înregistrează retur”.
  3. Sistemul marchează împrumutul ca închis și crește numărul de exemplare disponibile.
- Extensie UC11 `[data curentă > data scadentă]`: sistemul calculează penalitatea (zile de întârziere × tarif/zi) și o afișează pentru confirmare înainte de închidere.
