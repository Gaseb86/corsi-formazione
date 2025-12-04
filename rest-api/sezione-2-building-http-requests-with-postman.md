# Sezione 2: Building HTTP Requests with Postman

## 👀 Overview della sezione

In questa sezione uniremo teoria e tanta pratica per imparare a lavorare con le API tramite il protocollo HTTP, il più usato al mondo per le API.

### Cosa imparerai:
- Cos’è HTTP e perché è fondamentale per le API
- Come funziona una richiesta HTTP (struttura, metodi, headers, body)
- Come inviare richieste e analizzare risposte usando Postman

HTTP non fa differenza tra una pagina web e una chiamata API: tutto passa attraverso lo stesso protocollo. Capire HTTP è la base per poter lavorare con qualsiasi API moderna.

---

## 📨 Struttura di un messaggio HTTP

Quando un client (es: browser, Postman, app) comunica con un server tramite HTTP, lo fa inviando una **richiesta** (HTTP request) e ricevendo una **risposta** (HTTP response).

### ✉️ HTTP Request (richiesta)
Contiene:
- **URL** (Uniform Resource Locator): l’indirizzo della risorsa (es: https://www.npr.org/sections/news)
- **Metodo** (o verbo): l’azione da compiere (es: GET, POST, PUT, DELETE)
- **Headers**: informazioni aggiuntive (es: tipo di client, formato dati)
- **Body**: i dati inviati al server (presente solo in alcuni metodi, es: POST)

Esempio:
```
POST /api/invoices HTTP/1.1
Host: example.com
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.2

{
  "customer": "Mario Rossi",
  "amount": 100
}
```

### 📩 HTTP Response (risposta)
Contiene:
- **Status code**: codice numerico che indica l’esito (es: 200 OK, 404 Not Found)
- **Headers**: informazioni aggiuntive sulla risposta (es: Content-Type)
- **Body**: i dati restituiti dal server (es: HTML, JSON, XML)

Esempio:
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "result": "Fattura creata con successo"
}
```

### 🗂️ Riepilogo
- La richiesta contiene: **URL, metodo, headers, body**
- La risposta contiene: **status code, headers, body**

> 💡 Nelle prossime lezioni vedremo ogni parte nel dettaglio, con esempi pratici in Postman!

---

## 🔨 HTTP Request Methods: GET, POST, PUT, DELETE...

I metodi HTTP (o verbi) indicano l’azione che il client vuole compiere sulla risorsa.

### I principali metodi:
- **GET**: recupera dati dal server (es: visualizzare una lista ordini)
- **POST**: crea nuovi dati sul server (es: inviare un nuovo ordine)
- **PUT**: aggiorna dati esistenti (es: modificare un ordine già inviato)
- **DELETE**: elimina dati (es: cancellare un ordine)

### 🛒 Esempio pratico: acquisto online
- **GET**: controlli lo stato dell’ordine → il server ti mostra i dettagli
- **POST**: invii la lista della spesa → il server crea l’ordine
- **PUT**: modifichi l’ordine (aggiungi latte, togli uova) → il server aggiorna l’ordine
- **DELETE**: cancelli l’ordine → il server lo elimina

### ℹ️ Altri metodi
Esistono altri metodi (PATCH, OPTIONS, HEAD…), ma i quattro sopra sono i più usati nelle API REST.

### 👑 Chi decide quale metodo usare?
Dipende dal server e dall’API: la documentazione dell’API ti dirà quale metodo usare per ogni operazione.
Le best practice sono:
- **GET** per leggere
- **POST** per creare
- **PUT** per aggiornare
- **DELETE** per eliminare

Ma il server può implementare regole diverse!

> 💡 Consulta sempre la documentazione dell’API per sapere quale metodo usare.


---

## 🚀 Introduzione a Postman: lo strumento per lavorare con le API

**Postman** è il tool più usato al mondo per sviluppare, testare e documentare API.
Oltre 10 milioni di persone e 500.000 aziende lo usano ogni giorno!

### 🔽 Installazione
- Scarica Postman gratis da [postman.com](https://www.postman.com/downloads/)
- Disponibile per Windows, Mac e Linux
- **Non usare l’estensione Chrome:** è obsoleta e non più supportata

### 👤 Account
- Puoi creare un account gratuito (consigliato, per salvare le tue richieste e collezioni)
- Oppure puoi usare l’app senza account (clicca su “Take me straight to the app”)

### 🖥️ Prime schermate
- Al primo avvio, Postman mostra una “launchpad” con le funzioni principali
- Puoi chiudere la schermata e iniziare subito a creare richieste

### 🛠️ Perché usare Postman?
- Permette di inviare richieste HTTP di ogni tipo (GET, POST, PUT, DELETE…)
- Puoi impostare URL, metodo, headers, body, parametri, ecc.
- Analizza facilmente le risposte del server
- Molto più potente e flessibile del browser per lavorare con le API

> 💡 Nelle prossime lezioni useremo Postman per esercitarci con le API e capire come funziona HTTP nella pratica!


---

## 🔎 Cosa sono i Query Parameters?

I **query parameters** sono valori che aggiungi all’URL per filtrare, cercare o personalizzare la risposta di un’API o di un sito web.

### 📚 Sintassi
- I parametri iniziano dopo il punto di domanda `?` nell’URL
- Ogni parametro ha la forma `chiave=valore`
- Più parametri si separano con `&`

Esempio:
```
https://api.example.com/search?name=John&age=17
```
Qui stai cercando tutti i risultati dove `name` è John e `age` è 17.

### 🖥️ Esempio pratico
- Ecosia: `https://www.ecosia.org/search?q=postman`
  - `q=postman` è il parametro che indica cosa cercare
- Filtri aggiuntivi: `https://www.ecosia.org/search?q=API&freshness=Day`
  - `freshness=Day` filtra i risultati per le ultime 24 ore

### ℹ️ Note importanti
- I nomi dei parametri sono decisi dall’API o dal sito: devi usare quelli previsti dalla documentazione
- Alcuni parametri sono obbligatori, altri opzionali
- In Postman puoi aggiungere i query parameters in un pannello dedicato, ma sono sempre parte dell’URL

> 💡 Ricorda: i query parameters servono per passare dati e filtrare risultati.Consulta sempre la documentazione dell’API per sapere quali parametri puoi usare!

---

## 🛤️ Cosa sono i Path Parameters?

I **path parameters** (o variabili di percorso) sono valori che compaiono direttamente nella struttura dell’URL, al posto di una parte fissa, per identificare una risorsa specifica.

### 📚 Sintassi
- I path parameters sono inseriti tra gli slash `/` nell’URL
- Non hanno una chiave esplicita: il valore stesso identifica la risorsa

Esempio:
```
https://api.example.com/students/John/grades?order=ASC
```
Qui `John` è un path parameter che identifica lo studente, mentre `order=ASC` è un query parameter.

### 🖥️ Esempio pratico con Postman
- API Open Library: `https://openlibrary.org/people/vesper/lists.json`
  - `vesper` è il path parameter (username)
  - Puoi sostituirlo con altri username per vedere le loro liste
- In Postman, puoi usare la sintassi `:username` nell’URL (es: `/people/:username/lists.json`) e compilare il valore nel pannello “Path Variables”

### 🔄 Differenza tra path e query parameters
- **Path parameters**: identificano una risorsa specifica, fanno parte del percorso
- **Query parameters**: filtrano o modificano la richiesta, vengono dopo il `?` nell’URL

### ℹ️ Note importanti
- I path parameters sono decisi dall’API: consulta la documentazione per sapere dove e come usarli
- Puoi avere più path parameters in un URL
- In Postman, path e query parameters hanno pannelli separati per facilitarne la gestione

> 💡 Ricorda: path parameters servono per identificare risorse specifiche (es: utenti, prodotti, ordini) direttamente nel percorso dell’URL!

---

## 🏷️ Cosa sono gli HTTP Headers?

Gli **headers** sono informazioni aggiuntive (metadati) che accompagnano ogni richiesta e risposta HTTP. Servono a fornire dettagli su come gestire, interpretare o descrivere i dati trasmessi.

### 📚 Sintassi
- Ogni header ha una chiave e un valore: `Chiave: Valore`
- Sono presenti sia nella richiesta che nella risposta

Esempio:
```
GET / HTTP/1.1
Host: www.google.com
User-Agent: PostmanRuntime/7.32.2
Accept-Language: fr
Cache-Control: no-cache
```

### 🖥️ Esempio pratico con Postman
- Puoi vedere e modificare gli headers nella tab “Headers”
- Alcuni headers sono aggiunti automaticamente (es: User-Agent, Cache-Control)
- Puoi aggiungere header personalizzati (es: `Accept-Language: fr` per ricevere la risposta in francese)
- Gli headers della risposta sono visibili nella tab “Headers” della sezione Response

### 📦 Analogia
Come le etichette su un pacco: alcune sono obbligatorie (indirizzo), altre opzionali (fragile, contenuto speciale)

### ℹ️ Note importanti
- Gli headers sono solo testo: il server deve riconoscere la chiave per reagire
- Esiste una lista standard di headers, ma puoi aggiungere anche personalizzati
- La documentazione dell’API ti dirà quali headers sono richiesti o supportati
- In Postman puoi vedere il formato “grezzo” dei messaggi nella console

> 💡 Ricorda: gli headers sono fondamentali per controllare il comportamento delle richieste e delle risposte HTTP. Impara a riconoscere i più comuni (Content-Type, Accept, Authorization, ecc.)!

---

## 🏷️ HTTP headers: Content-Type

Il **Content-Type** è uno degli header più importanti: indica il tipo di contenuto che viene inviato o ricevuto nel body della richiesta o della risposta HTTP.

### 📚 A cosa serve?
- Permette al client e al server di sapere subito che tipo di dati stanno gestendo (HTML, JSON, XML, ecc.)
- Aiuta strumenti come Postman a visualizzare correttamente la risposta

### 📝 Esempi di Content-Type
- `text/html` → pagina web HTML
- `application/json` → dati in formato JSON
- `application/xml` o `text/xml` → dati in formato XML

### 🖥️ Esempio pratico con Postman
- Nella tab “Headers” puoi aggiungere `Content-Type: application/json` quando invii dati JSON
- Se la risposta contiene `Content-Type: application/json`, Postman mostrerà la risposta in formato “Pretty” JSON
- Se manca il Content-Type, Postman non sa come formattare la risposta e la mostra come testo semplice

### ℹ️ Note importanti
- Il Content-Type può essere presente sia nella richiesta che nella risposta
- Se invii dati (es: POST, PUT), imposta sempre il Content-Type corretto
- La documentazione dell’API ti dirà quale Content-Type usare

> 💡 Ricorda: il Content-Type è fondamentale per la corretta interpretazione dei dati tra client e server!

---

## 🏷️ HTTP headers: Authorization

L’header **Authorization** è fondamentale per la sicurezza delle API: serve a inviare le credenziali (token, password, chiavi) che permettono di identificare chi sta facendo la richiesta.

### 📚 A cosa serve?
- Permette di autenticare l’utente o l’applicazione che chiama l’API
- Senza Authorization, molte API rispondono con errore 401 Unauthorized

### 📝 Esempi di Authorization header
- **Bearer Token** (il più comune per le API moderne):
  ```
  Authorization: Bearer <token>
  ```
- **Basic Auth** (meno usato, base64 di user:password):
  ```
  Authorization: Basic <base64(user:password)>
  ```

### 🖥️ Esempio pratico con Postman
- Vai nella tab “Authorization” e scegli “Bearer Token”
- Inserisci il token richiesto dall’API
- Postman aggiungerà automaticamente l’header `Authorization: Bearer <token>`
- Puoi anche aggiungerlo manualmente nella tab “Headers”

### ℹ️ Note importanti
- Le API specificano sempre nella documentazione quale tipo di Authorization usare
- Non inviare mai credenziali sensibili nei query parameters o nel body
- L’Authorization header è usato solo nella richiesta, non nella risposta

> 💡 Ricorda: senza Authorization, molte API non ti permettono di accedere ai dati! Consulta sempre la documentazione per sapere che tipo di autenticazione serve.

---

## 🏷️ HTTP headers: Cookie (Cookies)

I **cookie** sono piccoli dati che il server può salvare sul client (di solito il browser) tramite HTTP headers.
Anche se sono poco usati nelle API moderne, è importante conoscerli.

### 📚 Come funzionano?
- Il server invia un header `Set-Cookie` nella risposta per chiedere al client di salvare un cookie
- Il client (browser o Postman) salva il cookie e lo invia nelle richieste successive tramite l’header `Cookie`

### 📝 Esempio di headers
- Risposta dal server:
  ```
  Set-Cookie: sessionid=abc123; Path=/; Domain=.google.com; Expires=...
  ```
- Richiesta successiva dal client:
  ```
  Cookie: sessionid=abc123
  ```

### 🖥️ Esempio pratico con Postman
- Fai una richiesta a google.com: nella risposta vedrai uno o più header `Set-Cookie`
- Nelle richieste successive, Postman aggiunge automaticamente l’header `Cookie` con i valori ricevuti
- Puoi visualizzare e gestire i cookie tramite l’interfaccia di Postman

### ℹ️ Note importanti
- I cookie sono usati soprattutto per autenticazione e tracciamento nelle web app
- Nelle API moderne si preferiscono token (es: Authorization) invece dei cookie
- I cookie sono sempre associati a un dominio
- Le API che richiedono cookie lo specificano nella documentazione

> 💡 Ricorda: i cookie sono headers HTTP speciali, usati soprattutto dai browser. Nelle API moderne si usano raramente, ma è utile saperli riconoscere!

---

## 📝 HTTP body

L’**HTTP body** è la parte principale della richiesta o della risposta: contiene i dati veri e propri che vogliamo inviare o ricevere.

### 📚 Quando si usa?
- Nelle richieste: solo con alcuni metodi (POST, PUT, PATCH), non con GET
- Nelle risposte: quasi sempre, perché il server restituisce dati

### 📝 Cosa può contenere?
- Testo semplice
- Dati strutturati (JSON, XML)
- File, immagini, audio, ecc. (più raro nelle API)

### 🖥️ Esempio pratico con Postman
1. Seleziona il metodo POST
2. Vai nella tab “Body” e scegli “raw”
3. Scrivi il contenuto (es: JSON)
   ```json
   {
     "name": "Valentine"
   }
   ```
4. Seleziona “JSON” dal menu a destra per formattare correttamente
5. Postman aggiungerà automaticamente l’header `Content-Type: application/json`
6. Invia la richiesta e controlla la risposta

### ⚠️ Attenzione alla validità dei dati
- Se il formato (es: JSON) non è valido, il server potrebbe non capire la richiesta
- Postman aiuta a evidenziare errori di sintassi

### ℹ️ Note importanti
- Il body è opzionale nelle richieste, ma quasi sempre presente nelle risposte
- Segui sempre la documentazione dell’API per sapere che formato usare

> 💡 Ricorda: il body è il “contenuto” della richiesta/risposta. Per le API moderne, il formato più usato è JSON!

---

## 🟢 HTTP status code (200, 301, 401, 403, 404, ...)

Gli **HTTP status code** sono codici numerici inviati dal server nella risposta per indicare l’esito della richiesta. Solo il server può inviarli.

### 📚 A cosa servono?
- Permettono al client di capire subito se la richiesta è andata a buon fine o se c’è stato un errore
- Facilitano la gestione degli errori senza dover analizzare il body della risposta

### 🗂️ Le principali classi di status code
- **1xx**: Informativi (raro nelle API)
- **2xx**: Successo
  - 200 OK: richiesta riuscita
  - 201 Created: risorsa creata
- **3xx**: Redirect (raro nelle API)
  - 301 Moved Permanently: risorsa spostata
- **4xx**: Errore del client
  - 400 Bad Request: richiesta malformata
  - 401 Unauthorized: non autenticato
  - 403 Forbidden: non autorizzato
  - 404 Not Found: risorsa non trovata
- **5xx**: Errore del server
  - 500 Internal Server Error: errore generico del server

### 🖥️ Esempio pratico con Postman
- Dopo aver inviato una richiesta, Postman mostra il codice di stato in alto nella risposta
- Passa il mouse sopra il codice per vedere una breve spiegazione
- 200 = tutto ok, 404 = risorsa non trovata, 401/403 = problemi di autenticazione/autorizzazione

### ℹ️ Note importanti
- Se il server è offline/non risponde, non riceverai nessun status code (errore di rete)
- Consulta sempre la documentazione dell’API per sapere quali status code aspettarti

> 💡 Ricorda: i codici di stato sono fondamentali per capire subito l’esito di una richiesta API!



