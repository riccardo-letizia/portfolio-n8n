# Portfolio di automazioni n8n · Riccardo Letizia

Laureato in Ingegneria Gestionale (Politecnico di Bari). Sto costruendo un portfolio di automazioni con n8n per piccole e medie imprese: ogni progetto parte dall'analisi del processo e arriva a un workflow documentato e testato.

## Contenuto

- `bpmn/`: mappe BPMN 2.0 di processi reali, nella versione attuale (AS-IS) e in quella riprogettata (TO-BE). Si aprono con [bpmn.io](https://demo.bpmn.io).
- `workflows/`: workflow n8n esportati in JSON, ripuliti da credenziali e dati personali.

## Prenotazioni di un parrucchiere (mappe BPMN)

- **AS-IS:** le prenotazioni arrivano tutte per telefono. Circa 360 chiamate al mese da 3 minuti, cioè circa **18 ore al mese** di lavoro della segretaria.
- **TO-BE:** il cliente prenota da un modulo online e l'automazione registra la richiesta. La segretaria interviene solo sulle eccezioni, per esempio quando l'orario richiesto non è disponibile.

## Meteo Bari → Telegram

Ogni mattina alle 7:00 invia su Telegram la previsione del giorno per Bari: temperatura minima e massima e probabilità di pioggia.

```
[Schedule Trigger: ogni giorno alle 7:00] → [HTTP Request: API Open-Meteo] → [Telegram: invio del messaggio]
```

- **Gradino della scala dell'automazione:** regole, senza AI. Il percorso è noto in partenza e l'input arriva sempre nello stesso formato, quindi un modello AI non aggiungerebbe valore.
- **API usata:** [Open-Meteo](https://open-meteo.com), gratuita e senza chiave.

### Come provarlo

1. In n8n crea un nuovo workflow e importa `workflows/meteo-bari.json` dal menu **⋯ → Import**.
2. Crea una credenziale **Telegram** con il token del tuo bot (lo fornisce @BotFather) e selezionala nel nodo Telegram.
3. Nel nodo Telegram sostituisci `INSERISCI_IL_TUO_CHAT_ID` con il Chat ID della chat in cui vuoi ricevere il messaggio.
4. Esegui il workflow una volta con **Execute** per verificare il messaggio, poi pubblicalo.

### Limiti noti

- **Nessun monitoraggio.** Se n8n è spento alle 7:00, il messaggio non parte e nessuno se ne accorge. Soluzione prevista: un monitor esterno che riceve un segnale a fine workflow e avvisa se non arriva.
- **Nessuna gestione degli errori.** Se Open-Meteo non risponde, l'esecuzione fallisce senza avvisare.
- **Città fissa:** le coordinate di Bari sono scritte nell'URL della richiesta.
