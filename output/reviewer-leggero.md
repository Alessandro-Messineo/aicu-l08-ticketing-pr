# Reviewer Leggero - Create Ticket

## Findings

- **Diff assente.** Il reviewer e' chiamato a leggere un diff, ma `git status` mostra zero file modificati: nessuna patch e' stata applicata. Sono presenti solo due file untracked in `output/` (entry-point.md, prompt-patch-limitato.md). Impossibile verificare file toccati, modifiche inattese o stop condition sul codice.

- **Contract non rispettato: campo singolo vs due campi.** Il contract sketch definisce un payload valido con `title` e `description` (due campi distinti). Il prompt patch limitato descrive "un campo di input per il testo del problema" (campo singolo). La boundary map del contract elenca esplicitamente "form per la creazione del ticket con i campi title e description". Il data sketch classifica entrambi come `accettato` (input utente). Lo slice proposto riduce il contract a un solo campo senza motivazione.

- **Incoerenza styles.css tra entry-point map e prompt patch.** L'entry-point map classifica `src/styles.css` come `dubbio` e non lo elenca nella sezione "File Vietati". Il prompt patch lo include invece nella lista `File o aree vietate`. La mappa e il prompt non sono allineati.


## Verifiche Mancanti

- **Backend non raggiungibile non coperto.** L'issue originale include "simulo backend non raggiungibile e provo a inviare" nel piano di verifica manuale, e il contract sketch lo elenca nell'Error Model ("Errore visibile all'utente, nessun crash, nessuno stato inconsistente"). La verifica proposta nel prompt patch e nell'entry-point map non include questo caso.

- **Caratteri speciali non coperti.** L'issue originale prevede "digito un testo con caratteri speciali (es. emoji, <>/&) e lo invio". La verifica proposta nel prompt patch omette questo test.

- **Verifica solo su input vuoto, non su campo mancante.** La verifica proposta testa "campo vuoto" ma non il caso di payload JSON con campo title assente (previsto dall'Error Model del contract: "Campo richiesto mancante o vuoto").

## Decisione

- **Da correggere.** Bloccanti: (1) il contract prevede due campi (title, description) e il prompt patch ne pianifica uno solo — lo slice non rispetta il boundary concordato; (2) non esiste diff da revisionare, quindi la stop condition non e' verificabile. Minori: (3) verifiche mancanti (backend unreachable, caratteri speciali); (4) incoerenza styles.css tra mappa e prompt; (5) nome file divergente.
