# Guida: Creazione ed Esecuzione della Prima Funzione Azure

Questa guida descrive passo passo come creare, eseguire e testare una semplice funzione Azure con trigger HTTP, come richiesto dalla User Story 3.

## User Story 3: Creazione ed Esecuzione Prima Azure Function
**Descrizione:** Voglio creare una semplice funzione HTTP per capire il ciclo di vita dell'applicazione.

---

### Passaggio 1: Inizializzazione del Progetto e Creazione della Funzione

Per prima cosa, prepariamo l'ambiente di sviluppo locale.

1.  **Apri un terminale** in VS Code.
2.  **Crea una nuova cartella** per il tuo progetto e naviga al suo interno. È buona norma tenere i progetti organizzati.
    ```powershell
    mkdir projects\AzureFunctionsProject
    cd projects\AzureFunctionsProject
    ```
3.  **Inizializza un nuovo progetto** di Funzioni di Azure. Questo comando crea i file di configurazione di base del progetto (`local.settings.json`, `host.json`). Ti verrà chiesto di scegliere un runtime per i worker.
    ```powershell
    func init
    ```
    Per questo esempio, seleziona `dotnet` quando richiesto.

4.  **Crea una nuova funzione con trigger HTTP**. Questo comando genera il codice boilerplate per una funzione che risponde a richieste HTTP.
    ```powershell
    func new --name HttpExample --template "HTTP trigger"
    ```
    Verrà creata una nuova cartella `HttpExample` contenente il file C# con la logica della funzione.

---

### Passaggio 2: Esecuzione Locale e Test con `curl`

Ora che il codice è stato generato, eseguiamolo in locale per testarlo.

1.  **Avvia l'host locale** delle Funzioni di Azure. Questo comando compila il codice e avvia un server di sviluppo che simula l'ambiente Azure.
    ```powershell
    func start
    ```
    Nel terminale vedrai l'URL completo per invocare la tua funzione, che sarà simile a questo:
    `HttpExample: [GET,POST] http://localhost:7071/api/HttpExample`

2.  **Apri un secondo terminale** per testare la funzione senza fermare il server. Useremo `curl` per inviare una richiesta HTTP. L'URL di default si aspetta un parametro `name` nella query string.
    ```powershell
    curl "http://localhost:7071/api/HttpExample?name=Copilot"
    ```
    La risposta attesa nel terminale sarà: `Hello, Copilot. This HTTP triggered function executed successfully.`

---

### Passaggio 3: Configurazione del Port Forwarding per Postman

Per testare la funzione da un'applicazione esterna a VS Code come Postman (in esecuzione sul tuo PC fisico), è necessario esporre la porta del servizio in esecuzione nel codespace.

1.  Nel pannello inferiore di VS Code, vai alla scheda **"Porte"**.
2.  Se la porta `7071` non è già elencata, fai clic sul pulsante **"Inoltra una porta"** e digitala.
3.  VS Code renderà la porta pubblicamente accessibile e ti fornirà un URL inoltrato, come `https://some-random-name.app.github.dev:7071`.
4.  Apri **Postman** sul tuo computer.
5.  Crea una nuova richiesta **GET** e incolla l'URL fornito, aggiungendo il percorso della funzione e il parametro.
    Esempio: `https://some-random-name.app.github.dev:7071/api/HttpExample?name=Postman`
6.  Invia la richiesta. La risposta dovrebbe essere identica a quella ricevuta tramite `curl`.

---

### Passaggio 4: Analisi dei Log

Ogni volta che la funzione viene invocata, l'host delle Funzioni di Azure scrive dei log dettagliati nel terminale in cui è in esecuzione `func start`. Questi log sono essenziali per il debug.

Ecco un esempio dell'output:
```
info: Function.HttpExample[0]
      Executing 'HttpExample' (Reason='This function was programmatically called via the host APIs.', Id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx)
info: C# HTTP trigger function processed a request.
info: Function.HttpExample[0]
      Executed 'HttpExample' (Succeeded, Id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx, Duration=123ms)
```

**Spiegazione dettagliata dei log:**

1.  `Executing 'HttpExample'`:
    *   **Cosa significa:** È il log di inizio esecuzione. Indica che il trigger (in questo caso, una richiesta HTTP) è stato ricevuto e la funzione `HttpExample` sta per essere eseguita.
    *   **Reason:** Spiega perché la funzione è stata attivata.
    *   **Id:** Un GUID (Globally Unique Identifier) che identifica in modo univoco questa specifica esecuzione. È utile per correlare i log di inizio e fine della stessa chiamata.

2.  `C# HTTP trigger function processed a request.`:
    *   **Cosa significa:** Questo è un log informativo generato direttamente dal codice della funzione. Aprendo il file `HttpExample.cs`, troverai una riga simile a `log.LogInformation("C# HTTP trigger function processed a request.");`. Puoi (e dovresti) aggiungere log personalizzati come questo per tracciare il flusso logico della tua applicazione.

3.  `Executed 'HttpExample'`:
    *   **Cosa significa:** È il log di fine esecuzione. Indica che la funzione ha completato il suo lavoro.
    *   **Succeeded:** Lo stato finale. Può essere `Succeeded` o `Failed`. Se è `Failed`, di solito è accompagnato da un'eccezione o un messaggio di errore.
    *   **Id:** Lo stesso ID del log di inizio, per una facile correlazione.
    *   **Duration:** Il tempo totale, in millisecondi, impiegato dalla funzione per completare l'esecuzione. È un dato cruciale per monitorare le performance.
