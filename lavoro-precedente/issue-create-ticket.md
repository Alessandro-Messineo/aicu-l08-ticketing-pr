# Issue: Create ticket with validation

## Request

```txt
Serve creare ticket dal supporto.
```

## Fatti (Facts)

- siamo in un app di ticketing con un back end sviluppato in java 
- lato front c'è già un componente pronto a renderizzare il ticket; verra riutilizzato cosi com'e, senza modifiche
- si deve creare la stuttura back per creare il nuovo ticket
- il ticket verrà salvato nel DB

## Assunzioni (Assumptions)

- il backend deve restituire uno status di errore (es. 400) se il ticket non viene creato, e uno status di successo (es. 201) con il ticket creato in caso positivo
- le informazioni mostrate nel componente esistente vengono popolate dai dati del ticket creato senza modificarne struttura o stile

## Domande Aperte (Questions)

- devono essere aggiunti campi al ticket (es. una sezione note)?
- chi deve visualizzare e gisetire i ticket?
- deve esserci la possibilità di modificare il ticket una volta creato?
- quanti ticket possono essere creati?
- cosa deve vedere l'utente in caso di errore di rete o backend non disponibile durante la creazione?

## Decisione (Decision)

Per questo slice, "creare ticket" significa:

```txt
Utente che aprendo l'app posso creare un ticket e scrivere del problema in modo da risolverlo
```

## Fuori Scope / Non-Obiettivi (Non-Goals)

- non modificare ux/ui
- non creare pagine aggiuntive


## Criteri Di Accettazione (Acceptance Criteria)

1. l'utente digita del testo nel campo di input e, all'invio, un nuovo ticket compare nell'elenco
2. un ticket vuoto non viene creato
3. layout, colori, font e componenti visibili dell'app rimangono identici a prima dell'intervento (verifica visuale side-by-side)

## Piano Di Verifica Manuale (Manual Test Plan)

- digito un testo nel campo, lo invio e verifico che il ticket appaia nell'elenco.
- con il campo ti testo vuoto, provo a inviare: verifico che non venga creato nessun ticket.
- digito un testo con caratteri speciali (es. emoji, <>/&) e lo invio: verifico che il ticket appaia correttamente nell'elenco.
- simulo backend non raggiungibile e provo a inviare: verifico che l'utente veda un messaggio di errore, senza crash o stato inconsistente.

