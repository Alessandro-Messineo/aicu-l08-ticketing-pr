# Prompt Patch Limitato

## Prima Di Compilare

Un prompt patch limitato e' l'istruzione operativa che userai nel lab per autorizzare solo il primo slice.

Serve a dire al builder:

- quale task affrontare;
- quali file puo' toccare;
- cosa resta fuori scope;
- quale verifica proporre;
- quando fermarsi.

Non usarlo per chiedere la feature completa o per autorizzare file non verificati.

Usa questo prompt nel lab L08, dopo il gate umano.

```txt
Dato questo task:
"Serve creare ticket dal supporto."

Usa questi input:
- issue: issue-create-ticket.md
- contract sketch: contract-sketch-create-ticket.md
- data sketch: data-sketch-create-ticket.md
- mappa dei punti di intervento: entry-point.md

Applica solo il primo slice approvato:
Implementare POST /api/tickets lato server con validazione minima
(titolo e descrizione obbligatori, non vuoti) e salvataggio in memoria
nell'array tickets esistente. Aggiungere createTicket in api.js per la
chiamata POST. Aggiungere in App.jsx un form minimo con un campo di
input per il testo del problema e un pulsante di invio. All'invio, il
nuovo ticket compare nell'elenco senza ricaricare la pagina.

File o aree ammesse:
- server/index.js
- server/data/tickets.js
- src/api.js
- src/App.jsx

File o aree vietate:
- src/components/TicketList.jsx
- src/components/TicketCard.jsx
- src/main.jsx
- src/styles.css
- index.html
- vite.config.mjs
- package.json

Non aggiungere:
- auth;
- allegati;
- notifiche;
- owner avanzato;
- dashboard;
- migration;
- redesign;
- refactor generale;
- campi priority o area (respinti dal data sketch);
- modifica, cancellazione del ticket (non-goal da issue e contract).

Prima di modificare, conferma:
- task;
- file che toccherai;
- cosa resta fuori scope;
- verifica manuale proposta.

Applica solo la patch minima approvata.
Fermati se servono file o decisioni fuori piano.
```


## Verifica Attesa

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
