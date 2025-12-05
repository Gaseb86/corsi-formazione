# Guida: Creazione ed Esecuzione di una Funzione Azure con Python e VS Code

Questa guida descrive passo passo come creare, eseguire e testare una semplice funzione Azure con trigger HTTP utilizzando Python e l'estensione Azure Functions per Visual Studio Code.

## User Story 3: Creazione ed Esecuzione Prima Azure Function
**Descrizione:** Voglio creare una semplice funzione HTTP per capire il ciclo di vita dell'applicazione.

---

### Prerequisito: Installare l'Estensione Azure Functions

Prima di iniziare, assicurati di aver installato l'estensione **Azure Functions** per VS Code. Puoi trovarla nel Marketplace delle estensioni.

---

### Passaggio 1: Creazione del Progetto e della Funzione tramite VS Code

L'estensione per VS Code semplifica notevolmente la creazione del progetto.

1.  **Apri la Palette dei Comandi** (`Ctrl+Shift+P` o `Cmd+Shift+P` su Mac).
2.  Cerca e seleziona il comando **`Azure Functions: Create New Project...`**.
3.  Segui i passaggi guidati:
    *   **Seleziona una cartella** per il tuo progetto (es. `projects/AzureFunctionsProjectPython`).
    *   **Seleziona un linguaggio:** Scegli **Python**.
    *   **Seleziona un interprete Python** per creare un ambiente virtuale.
    *   **Seleziona un template:** Scegli **HTTP trigger**.
    *   **Dai un nome alla funzione:** Ad esempio, `HttpExample`.
    *   **Scegli il livello di autorizzazione:** Seleziona **Anonymous** per semplificare i test.

VS Code creerà automaticamente la struttura del progetto, un ambiente virtuale (`.venv`), i file di configurazione (`local.settings.json`, `host.json`) e il file della funzione (`HttpExample/__init__.py`).

---

### Passaggio 2: Esecuzione Locale e Debug in VS Code

Eseguire e debuggare la funzione è integrato in VS Code.

1.  **Apri la vista "Run and Debug"** dal pannello laterale (`Ctrl+Shift+D`).
2.  Fai clic sul pulsante verde **"Start Debugging"** (o premi `F5`).
3.  VS Code avvierà l'host delle Funzioni di Azure nel terminale integrato e collegherà il debugger.
4.  Nel terminale vedrai l'URL per invocare la tua funzione, simile a questo:
    `HttpExample: [GET,POST] http://localhost:7071/api/HttpExample`

---

### Passaggio 3: Testare la Funzione con `curl` e Postman

I passaggi per testare la funzione sono identici, indipendentemente dal linguaggio.

1.  **Test con `curl`**:
    Apri un nuovo terminale e invia una richiesta GET:
    ```powershell
    curl "http://localhost:7071/api/HttpExample?name=Copilot"
    ```
    La risposta attesa sarà: `Hello, Copilot. This HTTP triggered function executed successfully.`

2.  **Test con Postman (tramite Port Forwarding)**:
    *   Nel pannello inferiore di VS Code, vai alla scheda **"Porte"**.
    *   Assicurati che la porta `7071` sia inoltrata. In caso contrario, aggiungila.
    *   Copia l'URL inoltrato (es. `https://some-random-name.app.github.dev:7071`).
    *   In Postman, crea una richiesta **GET** all'URL completo:
      `https://some-random-name.app.github.dev:7071/api/HttpExample?name=Postman`
    *   Invia la richiesta per ricevere la stessa risposta.

---

### Passaggio 4: Analisi del Codice Python e dei Log

Diamo un'occhiata al codice generato e ai log prodotti.

**Codice (`HttpExample/__init__.py`):**
```python
import logging
import azure.functions as func

def main(req: func.HttpRequest) -> func.HttpResponse:
    logging.info('Python HTTP trigger function processed a request.')

    name = req.params.get('name')
    if not name:
        try:
            req_body = req.get_json()
        except ValueError:
            pass
        else:
            name = req_body.get('name')

    if name:
        return func.HttpResponse(f"Hello, {name}. This HTTP triggered function executed successfully.")
    else:
        return func.HttpResponse(
             "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response.",
             status_code=200
        )
```

**Analisi dei Log nel terminale di VS Code:**
```
info: Function.HttpExample[0]
      Executing 'Functions.HttpExample' (Reason='This function was programmatically called via the host APIs.', Id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx)
info: Host.Function.Console[0]
      Python HTTP trigger function processed a request.
info: Function.HttpExample[0]
      Executed 'Functions.HttpExample' (Succeeded, Id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx, Duration=123ms)
```

**Spiegazione dettagliata:**

1.  `Executing 'Functions.HttpExample'`:
    *   Indica che il trigger HTTP è stato ricevuto e l'esecuzione della funzione `HttpExample` è iniziata. L'`Id` univoco aiuta a tracciare la singola richiesta.

2.  `Python HTTP trigger function processed a request.`:
    *   Questo è il log personalizzato che abbiamo scritto nel nostro codice Python usando la libreria `logging`. È fondamentale per capire il flusso di esecuzione della logica di business.

3.  `Executed 'Functions.HttpExample'`:
    *   Indica che la funzione ha terminato il suo lavoro.
    *   **Succeeded:** Mostra che non ci sono stati errori.
    *   **Duration:** Misura il tempo di esecuzione, utile per l'analisi delle performance.
