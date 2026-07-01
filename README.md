# Nota Spese
**La nota spese in un click.**

App web personale per tenere traccia delle spese e generare la **nota spese in PDF** da inviare al commercialista o all'azienda. Puoi inserire le spese a mano in pochi click, oppure **scattare o caricare la foto di una ricevuta (o un PDF) e lasciare che l'AI compili i campi** al posto tuo.

Il sito è statico (una sola pagina): non c'è un server da tenere acceso. I dati vivono su un database SQLite ospitato (Turso) e la lettura delle ricevute avviene tramite OpenRouter. Nessun costo fisso.

## Cosa fa

- Registro spese con categorie (vitto, trasporti, carburante, alloggio, software, ecc.).
- **Scansione AI**: carichi una foto o un PDF della ricevuta e i dati (data, importo, IVA, esercente…) vengono compilati in automatico.
- **Rimborsi chilometrici**: inserisci i km e la tariffa, il totale si calcola da solo.
- **Telepass / pedaggi, parcheggi** e altre categorie pronte all'uso.
- Vista per **mese** con subtotali e riepilogo (totale, IVA, spese per categoria).
- **PDF intestato**, con i tuoi dati e quelli dell'azienda destinataria del rimborso, e in appendice le ricevute allegate (numerate, 6 per pagina).
- Eliminazione in blocco delle spese di un intero mese.
- Dati **sincronizzati tra i dispositivi** (telefono e computer).

## Cosa serve per farla funzionare

Tre cose, tutte con piano gratuito:

1. **Un database Turso** (SQLite ospitato) — servono *URL* e *token*.
   - Crea un account su https://turso.tech, crea un database, copia il **Database URL** (`libsql://…`) e genera un **auth token**.
   - Non devi creare tabelle: l'app le crea da sola al primo avvio.

2. **Una chiave OpenRouter** (per la scansione AI) — facoltativa ma consigliata.
   - Crea un account su https://openrouter.ai, aggiungi un piccolo credito e crea una **API key**.
   - Modello consigliato (con visione): `google/gemini-2.5-flash`.
   - Senza chiave l'app funziona comunque: inserisci le spese a mano.

3. **Un hosting statico gratuito** — GitHub Pages oppure Cloudflare Pages.

## Come pubblicarla su GitHub Pages

1. Carica il file `index.html` nella **radice** di questa repository (Add file → Upload files → Commit).
2. Vai in **Settings → Pages**.
3. In **Source** scegli *Deploy from a branch*, branch `main`, cartella `/ (root)`, poi **Save**.
4. Dopo circa un minuto l'app è online su `https://TUONOME.github.io/nome-repo/`.

In alternativa **Cloudflare Pages**: crea un progetto e collega la repo (oppure carica il file). Anche qui hosting statico gratuito e URL sempre attivo.

## Primo avvio

Apri l'URL dell'app: comparirà la schermata **Collega il database**. Incolla URL e token di Turso (e la chiave OpenRouter, se la usi) e premi **Connetti**.

Le credenziali restano salvate **solo nel tuo browser**, su ogni dispositivo. Aprendo lo stesso indirizzo da un altro dispositivo e reinserendo le credenziali una volta sola, ritrovi le stesse spese: la sincronizzazione la fa Turso.

## Privacy e sicurezza

- L'URL è pubblico ma serve solo il codice della pagina: chi lo apre senza credenziali vede un'app vuota.
- I tuoi dati stanno su Turso; le chiavi (Turso e OpenRouter) restano nel browser, **non** nel codice pubblico.
- Non condividere il dispositivo con le credenziali già inserite.

## Note

- In alto, sotto "Nota Spese", è indicata la **versione** (es. `v9`): serve a capire se stai guardando l'ultima versione o una copia rimasta in cache. Dopo un aggiornamento ricarica forzando l'aggiornamento della pagina, oppure apri l'URL con un `?v=` diverso.
- **Costi**: hosting 0 €, database 0 € nel piano gratuito Turso, scansione AI a consumo su OpenRouter (pochi centesimi a ricevuta).

## Tecnologie

Pagina statica in HTML + React (via CDN, nessun build), database **Turso / libSQL** (SQLite), lettura ricevute via **OpenRouter**, PDF generato con **jsPDF**, anteprima dei PDF con **pdf.js**.
