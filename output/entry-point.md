# Mappa Dei Punti Di Intervento (Entry-Point Map) - Create Ticket

## File Candidati

| File / area | Suggerito da | Evidenza verificata | Stato |
| --- | --- | --- | --- |
| server/index.js | repo | Contiene l'endpoint `POST /api/tickets` che attualmente risponde 501 (stub). Gestisce gia' `express.json()` per il parsing del body. Importa i dati da `tickets.js`. L'endpoint e' il punto di ingresso lato server per creare un ticket. | ammesso |
| server/data/tickets.js | repo | Contiene l'array `tickets` mock con la struttura reale dei ticket (campi: id, title, description, customer, priority, area, status, source, createdAt, updatedAt). Esporta `allowedPriorities` e `allowedAreas`. Serve per validare i campi e salvare nuovi ticket in memoria. | ammesso |
| src/api.js | AI / repo | Attualmente espone solo `fetchOpenTickets` (GET /api/tickets). Manca una funzione per inviare un nuovo ticket al backend (POST). Il task "creare ticket" richiede una chiamata POST dal frontend. | ammesso |
| src/App.jsx | AI / repo | Componente root React. Attualmente carica e mostra ticket esistenti (loading/error/ready). Non ha un form di input per creare nuovi ticket. Il task richiede che l'utente possa digitare testo e inviarlo per creare un ticket. | ammesso |
| src/components/TicketList.jsx | AI / repo | Renderizza la lista dei ticket usando `TicketCard`. La issue L05 dice: "il componente pronto a renderizzare il ticket verra' riutilizzato cosi' com'e', senza modifiche". Il non-goal vieta di "modificare ux/ui". | vietato |
| src/components/TicketCard.jsx | AI / repo | Renderizza la card del singolo ticket (id, priority, title, customer, updatedAt). La issue L05 dice: "le informazioni mostrate nel componente esistente vengono popolate dai dati del ticket creato senza modificarne struttura o stile". | vietato |
| src/styles.css | AI / repo | Contiene tutti gli stili dell'app. La issue L05 impone: "layout, colori, font e componenti visibili dell'app rimangono identici a prima dell'intervento". Potrebbe servire uno stile minimo per il form, ma si possono usare stili inline o classi esistenti per evitare modifiche a questo file. | dubbio |
| src/main.jsx | repo | Entry point React, importa `App` e `styles.css`. Nessun collegamento diretto al task di creazione ticket. | vietato |
| index.html | repo | Entry point HTML. Nessun collegamento al task. | vietato |
| vite.config.mjs | repo | Configurazione Vite con proxy `/api` verso `http://127.0.0.1:3001`. Nessun collegamento al task. | vietato |
| package.json | repo | Dipendenze e script del progetto. Nessun collegamento al task. | vietato |

## File Ammessi Per Il Primo Slice

- server/index.js
- server/data/tickets.js
- src/api.js
- src/App.jsx

## File Vietati O Fuori Scope

- src/components/TicketList.jsx - non-goal esplicito: non modificare UX/UI, componente esistente riutilizzato cosi' com'e'
- src/components/TicketCard.jsx - non-goal esplicito: struttura e stile del componente esistente non vanno modificati
- src/main.jsx - nessun ruolo nel task; entry point che non richiede modifiche
- index.html - nessun ruolo nel task
- vite.config.mjs - nessun ruolo nel task; proxy gia' configurato correttamente
- package.json - nessun ruolo nel task; dipendenze sufficienti

## Primo Slice Proposto

```txt
Implementare POST /api/tickets lato server con validazione minima
(titolo e descrizione obbligatori, non vuoti) e salvataggio in memoria
nell'array tickets esistente. Aggiungere createTicket in api.js per la
chiamata POST. Aggiungere in App.jsx un form minimo con un campo di
input per il testo del problema e un pulsante di invio. All'invio, il
nuovo ticket compare nell'elenco senza ricaricare la pagina.
```

## Perche' Questo Slice E' Piccolo

- L'endpoint POST esiste gia' come stub 501: basta sostituire l'implementazione
- Il salvataggio e' in memoria (push nell'array esistente), nessuna migration DB
- Il form e' un singolo campo di input senza redesign UI
- Nessuna modifica a componenti esistenti (TicketList, TicketCard)
- Nessuna auth, nessuna rotta nuova, nessuna dipendenza aggiuntiva

## Verifica Manuale Proposta

```txt
1. Avviare dev server (pnpm dev).
2. Aprire l'app nel browser.
3. Digitare un testo nel campo di input e premere invio.
4. Verificare che il nuovo ticket appaia nell'elenco "Ticket aperti"
   con il testo inserito e che il contatore si aggiorni.
5. Provare a inviare con il campo vuoto: verificare che non venga creato
   nessun ticket e che appaia un messaggio di errore.
6. Verificare che TicketList e TicketCard rimangano visivamente identici
   (side-by-side con versione precedente).
```

