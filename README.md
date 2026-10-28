Sono Riccardo Letizia. Ingegnere gestionale, esperto in automazioni.
Nella prima cartella BPMN abbiamo la mappa as-is e to-be del processo. 
Nella seconda cartella, invece, abbiamo l'intero workflow, quindi la sua struttura riguarda il meteo di Bari. 
Come funziona: Ogni giorno alle 7:00 in punto su Telegram arriva il meteo di Bari con la previsione della pioggia, la sua data e la temperatura. Il gradino è 1, Perché il percorso è noto in partenza e l'input è standardizzato. 
Come è strutturato il processo? Abbiamo uno schedule ogni mattina alle 7:00. Poi un HTTP request con le API di Open Meteo prende la previsione di Bari e poi automaticamente viene mandato un messaggio su Telegram All'ID che forniamo.
Una volta importato il file, bisogna mettere le credenziali del proprio chat ID nella sezione chat ID, dove adesso c'è "inserisci il tuo chat ID". 
Tra le limitazioni abbiamo il fatto che, se il server N8n è spento, non arriverà nessun messaggio al nostro bot. 