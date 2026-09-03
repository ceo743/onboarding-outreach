# Wizard di onboarding clienti outreach

Pagine statiche su GitHub Pages, dominio `onboarding.davidecaiazzo.it`.

- `outreach/index.html` — template generico. Per un cliente nuovo: copia in `outreach-{slug}/`, cambia `CLIENT_NAME`, `CLIENT_SLUG`, `GATE_EMAIL` e popola i `draft` delle domande.
- `outreach-{slug}/index.html` — pagina del singolo cliente, URL `onboarding.davidecaiazzo.it/outreach-{slug}/`.
- `settori-sales-navigator.js` — elenco dei 462 settori di Sales Navigator, raggruppati (19 gruppi, con sottogruppi). Caricato da tutte le pagine con `<script src="../settori-sales-navigator.js">`.

## Tipi di domanda

Ogni domanda in `SECTIONS` accetta un campo `type`:

| `type` | Cosa mostra |
|---|---|
| assente | area di testo normale |
| `settori` | selettore dei settori Sales Navigator: gruppi apribili, ricerca, contatore, "seleziona tutti" per sottogruppo |
| `links` | elenco di campi link con "+ aggiungi un altro link" |

Campo `hint` opzionale: riga di spiegazione sotto la domanda.

**Settori**: la risposta viene salvata come stringa con separatore **punto e virgola** (`; `), non virgola — molti nomi di settore contengono già una virgola (es. "Fabbricazione di macchinari per l'agricoltura, l'edilizia e l'industria mineraria"). Se si cambia separatore vanno aggiornati sia il salvataggio sia la rilettura, altrimenti le selezioni si spezzano.

## Aggiornare l'elenco dei settori

Fonte: foglio Drive "Settori sales Navigator". Se LinkedIn aggiunge o rinomina categorie, rigenerare `settori-sales-navigator.js` mantenendo la struttura `[{gruppo, voci}]` oppure `[{gruppo, sottogruppi:[{nome, voci}]}]`. Le pagine dei clienti non vanno toccate: leggono tutte lo stesso file.

## Regole
- Colori sempre dalle variabili del tema (`--paper`, `--paper-raised`, `--ink`, `--ink-soft`, `--line`, `--accent`): le pagine hanno anche il tema scuro, i colori fissi lo rompono.
- Le risposte si salvano in `localStorage`, su Firestore (`onboarding_wizard/{slug}`) e via webhook Zapier. Per provare modifiche NON usare la pagina di un cliente vero: fare una copia locale con le scritture remote disattivate.
