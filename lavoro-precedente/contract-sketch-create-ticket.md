# Contratto Iniziale (Contract Sketch) - Create Ticket

## Prima Di Compilare

Un contratto iniziale (contract sketch) e' una descrizione leggera di input, output e risposte attese.

Serve a rendere verificabile `create ticket` prima di chiedere codice all'AI.

Compila solo la superficie minima:

- cosa entra;
- cosa esce;
- cosa viene rifiutato;
- quale errore ti aspetti.

Non trasformarlo in una specifica API completa, uno schema di un database o un piano di una patch.

Quando compili, ogni esempio deve rispondere (almeno) a tre domande:

- perche' questo input e' valido o invalido?
- quale risposta mi aspetto?
- quale parte della issue o del fuori scope giustifica la scelta?

## Request

```txt
Serve creare ticket dal supporto.
```

## Boundary Map

| Superficie | Cosa riguarda | Nota |
| --- | --- | --- |
| UI | L'utente vede un form per la creazione del ticket con i campi title e description | |
| API / azione | chiamata di tipo POST quando il form sarà inviato | [nota] |
| Dati | id, title, description, customer, priority | [nota] |
| Verifica | verificare che il ticket venga creato correttamente e sia visibile nell'elenco dei ticket e contenga tutti i dati inseriti. | [nota] |

## Action

Per questo slice, `create ticket` significa:

```txt
un utente compila i campi e invia il form e viene generato il ticket che sarà salvato nel db e visualizzato dall'operatore
```

## Payload Valido

```json
{
    "title": "Problema di accesso",
    "description": "L'utente non riesce ad accedere al portale."
}
```

Perche' e' valido:

- contiene i campi minimi per descrivere il problema dell'utente
- `customer` e `priority` sono generati dal sistema e non servono nel payload

## Risposta Attesa Di Successo

```txt
201 Created
```

Campi attesi:

- title confermato
- description confermato
- id generato
- customer generato
- priority generato
- createdAt generato

## Payload Invalido

```json
{
    "title": "",
    "description": ""
}
```

Motivo del rifiuto:

```txt
campi title e description sono stringhe vuote pertanto non è possibile risalire al problema dell'utente
```

Risposta attesa:

```txt
400 Bad Request — errore di validazione su title e description
```

## Error Model Minimo

| Caso | Motivo | Risposta attesa |
| --- | --- | --- |
| Campo richiesto mancante o vuoto | Il ticket senza title o description non e' interpretabile dall'operatore | 400 Bad Request — campi vuoti |
| Backend non raggiungibile o errore di rete | Il servizio backend non risponde (timeout, connection refused, DNS) — il ticket non puo' essere creato | Errore visibile all'utente (es. messaggio "Servizio non disponibile"), nessun crash, nessuno stato inconsistente |

## Non-Goals Confermati

- autenticazione e autorizzazione 
- modifica, cancellazione del ticket


