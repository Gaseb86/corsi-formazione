# Sezione 3: Working with REST APIs in Postman

## 🌐 What is REST?

**REST** (Representational State Transfer) è uno stile architetturale per la progettazione di API. Il termine indica un insieme di regole e principi che guidano come le API dovrebbero essere costruite e come dovrebbero comunicare.

- REST non è uno standard rigido né una specifica ufficiale: non esiste un ente che certifichi se un’API è davvero REST.
- È simile a uno stile architettonico in edilizia: riconosci le caratteristiche, ma non c’è un “manuale” obbligatorio.
- Molte API si definiscono REST o RESTful anche se non rispettano tutte le regole.

### 🏛️ REST come stile architetturale
- Come il “gothic style” in architettura, REST ha delle caratteristiche riconoscibili (URL chiari, uso dei verbi HTTP, risorse, statelessness, ecc.)
- Il termine RESTful si usa per indicare API che seguono (almeno in parte) i principi REST

> 💡 In sintesi: REST è un insieme di regole e idee per costruire API semplici, scalabili e facili da usare. Non è uno standard, ma uno stile riconoscibile!

---

## 📦 What is a resource?

Nelle REST API, una **risorsa** è qualsiasi informazione che può essere identificata e gestita tramite un URL.
Può essere:
- Un oggetto singolo (es: un ordine, un cliente, una pizza)
- Una collezione di oggetti (es: tutti gli ordini, tutti i clienti)
- Un dato reale (es: temperatura, lista prodotti)

### 📝 Esempi di risorse e URL
- `/orders` → tutti gli ordini (collezione)
- `/orders/93246` → ordine con ID 93246 (singolo oggetto)
- `/customers/6/orders/4` → ordine 4 del cliente 6

### 🔗 Endpoint
- Un **endpoint** è la parte finale dell’URL che identifica dove “ascolta” l’API per una risorsa o una collezione
- Gli endpoint sono spesso scritti al plurale: `/orders`, `/customers`, ecc.

### ⚡ Relazione tra risorse, endpoint e metodi HTTP
- **GET** `/orders` → ottieni tutti gli ordini
- **POST** `/orders` → crea un nuovo ordine
- **GET** `/orders/93246` → ottieni l’ordine con ID 93246
- **DELETE** `/orders/93246` → cancella l’ordine con ID 93246

### ℹ️ Note importanti
- Le risorse sono identificate dagli URL
- Gli endpoint sono i “rami” dell’API dove puoi interagire con le risorse
- Il metodo HTTP (GET, POST, PUT, DELETE) determina l’azione sulla risorsa

> 💡 Ricorda: nelle REST API, tutto ruota intorno alle risorse e agli endpoint che le identificano!

---

## 🚗 Hands-on: API Car Fleet Management

Nelle prossime lezioni lavoreremo con una semplice API per la gestione di un gruppo di auto (Car Fleet Management API).

### 🏷️ Risorse principali
- **Car**: informazioni su ogni auto (marca, modello, anno, costruttore)
- **Repair**: interventi di riparazione associati a una specifica auto
- **Statistics**: dati aggregati sulla flotta (es: età media delle auto)

Questa API ti permetterà di:
- Visualizzare la lista delle auto
- Aggiungere una nuova auto
- Gestire riparazioni
- Consultare statistiche sulla flotta

> 💡 Scopo: capire come funziona una REST API, come interagire con le risorse e come usare Postman per testare le operazioni principali.


## 🗂️ What is JSON?

**JSON** (JavaScript Object Notation) è un formato testuale standard per rappresentare e scambiare dati tra sistemi diversi.

### 📚 Caratteristiche principali
- Aperto e universale: usato da tutti i linguaggi di programmazione
- Basato su coppie chiave-valore
- Leggero e facile da leggere/scrivere

### 📝 Sintassi di base
- Gli oggetti JSON iniziano e finiscono con `{}`
- Le chiavi sono sempre stringhe tra virgolette
- I valori possono essere:
  - Stringhe: "Mario Rossi"
  - Numeri: 29
  - Booleani: true/false
  - Array: ["pizza", "pasta"]
  - Oggetti annidati: { "email": "mario@rossi.it" }
  - null

Esempio:
```json
{
  "firstName": "John",
  "age": 29,
  "hobbies": ["reading", "cycling"],
  "contact": {
    "email": "john@example.com"
  }
}
```

### 🔄 Serializzazione e deserializzazione
- **Serializzare**: trasformare un oggetto (es: Python, Java) in una stringa JSON
- **Deserializzare**: trasformare una stringa JSON in un oggetto del linguaggio

### 🌍 Perché è così diffuso?
- Indipendente dal linguaggio e dal sistema operativo
- Supportato nativamente dai browser e da tutte le API moderne
- Ideale per scambiare dati tra server, client, mobile app, ecc.

> 💡 Ricorda: JSON è il formato più usato per le API REST.
Imparerai a leggerlo, scriverlo e validarlo in ogni esercizio pratico!

---

## 📖 API Documentation

La **documentazione API** è la “mappa del tesoro” per lavorare con qualsiasi API: contiene tutte le informazioni necessarie per usare correttamente gli endpoint, i metodi HTTP, i parametri e i formati dei dati.

### 📝 Cosa trovi nella documentazione API?
- Elenco degli endpoint disponibili
- Descrizione delle risorse e delle operazioni
- Metodi HTTP da usare (GET, POST, ecc.)
- Formato dei dati (es: JSON)
- Esempi di richieste e risposte

### 📚 Formati comuni di documentazione
- **HTML/PDF**: pagine web o file scaricabili
- **Swagger/OpenAPI**: interfaccia interattiva per esplorare e testare l’API
- **Postman Collection**: file JSON importabile in Postman, spesso con pulsante “Run in Postman”
- **RAML**: formato strutturato per descrivere API

### 🔍 Dove trovo la documentazione?
- Cerca “<nome servizio> API” su Google (es: “Twitter API”, “GitHub Jobs API”)
- Sezione “Developers” o “API” sul sito ufficiale del servizio
- Alcune API private richiedono account o accesso riservato

### ⚡ Come usarla?
- Leggi la documentazione prima di iniziare: scopri quali endpoint e parametri sono disponibili
- Segui gli esempi per costruire le richieste in Postman
- Consulta la documentazione per capire come gestire errori, autenticazione, formati dati

> 💡 Ricorda: senza documentazione, lavorare con un’API è impossibile! Impara a leggerla e a usarla come riferimento costante.

---

## 📝 What is Swagger?

**Swagger** è uno standard per descrivere la struttura delle REST API in modo formale e leggibile sia da persone che da software.

### 📚 Cos’è Swagger?
- Una **specifica** (in formato JSON o YAML) che elenca tutti gli endpoint, i parametri, i modelli di dati, i metodi HTTP e le risposte di un’API
- Permette di generare documentazione interattiva, testare le API e persino generare codice client/server

### 🖥️ Swagger UI
- Interfaccia web che legge la specifica Swagger/OpenAPI e la trasforma in una documentazione interattiva
- Puoi esplorare gli endpoint, vedere i modelli di dati, inviare richieste di prova direttamente dal browser

### 🔄 Swagger e OpenAPI
- Swagger è stato lo standard originale, ora evoluto in **OpenAPI** (lo standard ufficiale per descrivere REST API)
- La maggior parte delle API moderne usa OpenAPI/Swagger per la documentazione formale

### ⚡ Esempio pratico
- La Car Fleet Management API ha una documentazione Swagger UI: puoi vedere tutti gli endpoint, i modelli (car, repair, statistics), e testare le richieste
- La specifica Swagger (file JSON/YAML) è usata dai tool per generare la UI, la documentazione e il codice

> 💡 Ricorda: Swagger/OpenAPI rende le API facili da esplorare, testare e integrare. Se trovi una documentazione Swagger UI, puoi subito provare gli endpoint e capire come funziona l’API!

---

## 🚗 Come creare una GET request (Parte 1)

Vediamo come consultare tutti i veicoli disponibili nella Car Fleet Management API usando Postman e la documentazione Swagger.

### 1️⃣ Consulta la documentazione Swagger
- Apri la documentazione Swagger UI dell’API
- Cerca la sezione relativa alle **auto** (ad esempio `/cars`)
- Trova l’endpoint `GET /cars` (serve per ottenere la lista di tutte le auto)
- Clicca su **Try it out** e poi su **Execute**
- Vedrai la richiesta inviata e la risposta ricevuta (in formato JSON):

```json
[
  { "id": 1, "brand": "Ford", "model": "Fiesta" },
  { "id": 2, "brand": "Tesla", "model": "Model S" },
  { "id": 3, "brand": "Tesla", "model": "Model 3" }
]
```

### 2️⃣ Fai la stessa richiesta in Postman
- Copia l’URL dell’endpoint dalla documentazione Swagger
- Apri Postman e crea una nuova tab
- Incolla l’URL nella barra degli indirizzi
- Imposta il metodo su **GET**
- Premi **Send**
- Vedrai la stessa risposta JSON con la lista delle auto

### 3️⃣ Usa le variabili d’ambiente in Postman
- In Postman, vai su **Manage Environments**
- Crea un nuovo ambiente chiamato ad esempio `Car Fleet Management API`
- Aggiungi una variabile chiamata `base_url` con il valore dell’host (es: `https://api.cars.example.com`)
- Salva l’ambiente e selezionalo dal menu in alto a destra
- Modifica l’URL della richiesta in: `{{base_url}}/cars`
- Postman sostituirà automaticamente la variabile con il valore corretto

### 4️⃣ Salva la richiesta in una Collection
- Clicca su **Save** per salvare la richiesta
- Crea una nuova Collection chiamata `Car Fleet Management API`
- Dai un nome alla richiesta, ad esempio `Get all cars`
- In questo modo potrai riutilizzare la richiesta in futuro

> 💡 **Nota didattica:**
> - Il metodo **GET** serve per ottenere dati dal server
> - La risposta è un array di oggetti (auto), ogni oggetto ha proprietà come `id`, `brand`, `model`
> - Usare le variabili d’ambiente rende le richieste più flessibili e riutilizzabili

Nella prossima parte vedremo come filtrare o ottenere una singola auto tramite l’endpoint con parametro.

---

## 🚗 Come creare una GET request (Parte 2: con parametro)

Vediamo come ottenere i dettagli di una singola auto tramite l’endpoint con parametro path.

### 1️⃣ Consulta la documentazione Swagger
- Trova l’endpoint `GET /cars/{id}`
- Noterai che `{id}` è un **parametro path**: va sostituito con l’ID dell’auto che vuoi cercare
- Clicca su **Try it out**, inserisci un valore per `id` (es: `3`), poi **Execute**
- La risposta sarà un singolo oggetto auto:

```json
{ "id": 3, "brand": "Tesla", "model": "Model 3" }
```

### 2️⃣ Fai la richiesta in Postman
- Crea una nuova tab in Postman
- Inserisci l’URL: `{{base_url}}/cars/3` (sostituisci `3` con l’ID desiderato)
- Imposta il metodo su **GET**
- Premi **Send**
- Riceverai la risposta con la singola auto

### 3️⃣ Gestisci i path parameters in Postman
- Puoi scrivere l’URL come `{{base_url}}/cars/:id` e usare la sezione **Path Variables** di Postman
- Inserisci il valore di `id` (es: `2`)
- Cambia facilmente l’ID senza modificare l’URL

### 4️⃣ Gestione degli errori
- Se inserisci un ID che non esiste (es: `20`), riceverai **status code 404** (Not Found)
- Questo indica che l’auto non è presente nel database

### 5️⃣ Salva la richiesta in una Collection
- Salva la richiesta con nome `Get single car`
- Ora hai due richieste: una per la lista di tutte le auto, una per la singola auto

> 💡 **Nota didattica:**
> - Gli endpoint con parametri path (`/cars/{id}`) sono molto comuni nelle API REST
> - Permettono di ottenere, modificare o cancellare una risorsa specifica
> - La risposta per una singola risorsa può contenere più dettagli rispetto alla lista
> - Gestire i path parameters in Postman rende le richieste più flessibili e veloci da modificare

Nella prossima parte vedremo come gestire errori e come lavorare con altri metodi HTTP (POST, PUT, DELETE).

---

## 🏋️‍♂️ Assignment - GET

Mettiamoci alla prova! Usa la documentazione Swagger e Postman per:
- Ottenere la lista delle riparazioni di una specifica auto: `GET /cars/{carId}/repairs`
- Ottenere i dettagli di una singola riparazione: `GET /cars/{carId}/repairs/{repairId}`

### Obiettivi
- Prova entrambi gli endpoint sia in Swagger UI che in Postman
- Usa i path parameters corretti (carId e repairId)
- Salva le richieste nella tua Collection

---

## ✅ Assignment solution - GET

### 1️⃣ Prova in Swagger UI
- Trova l’endpoint `GET /cars/{carId}/repairs`
  - Inserisci un carId valido (es: `1`)
  - Clicca su **Execute**
  - Ricevi una lista di riparazioni per quell’auto:

```json
[
  { "repairId": 3, "repairDate": "2023-01-10" },
  { "repairId": 5, "repairDate": "2023-03-22" }
]
```

- Trova l’endpoint `GET /cars/{carId}/repairs/{repairId}`
  - Inserisci un carId valido (es: `1`) e un repairId valido (es: `3`)
  - Clicca su **Execute**
  - Ricevi i dettagli della riparazione:

```json
{ "repairId": 3, "carId": 1, "repairDate": "2023-01-10", "description": "Cambio olio" }
```

### 2️⃣ Prova in Postman
- Crea una nuova richiesta: `{{base_url}}/cars/:carId/repairs`
  - Inserisci il valore di `carId` nei Path Variables (es: `1`)
  - Premi **Send**
  - Ricevi la lista delle riparazioni
  - Salva la richiesta come `Get all repairs`

- Crea una nuova richiesta: `{{base_url}}/cars/:carId/repairs/:repairId`
  - Inserisci i valori di `carId` e `repairId` nei Path Variables (es: `1` e `3`)
  - Premi **Send**
  - Ricevi i dettagli della riparazione
  - Salva la richiesta come `Get repair for a car`

### 3️⃣ Errori comuni
- Se ometti un parametro obbligatorio, riceverai un errore **400 Bad Request**
- Se usi un repairId che non appartiene a quell’auto, riceverai **404 Not Found**
- I path parameters sono fondamentali per identificare la risorsa giusta

### 4️⃣ Consigli pratici
- Usa i Path Variables di Postman per cambiare facilmente i parametri
- Salva sempre le richieste nella Collection per riutilizzarle
- Importa la Collection e l’ambiente forniti per velocizzare i test

> 💡 **Nota didattica:**
> - Gli endpoint annidati (`/cars/{carId}/repairs/{repairId}`) sono comuni per risorse collegate
> - Le risposte possono essere più dettagliate quando richiedi una singola risorsa
> - Gestire correttamente i parametri è essenziale per lavorare con le API REST

---

## ❌ Invalid JSON: errori comuni e come risolverli

Quando lavori con le API, uno degli errori più frequenti è inviare JSON non valido. Ecco cosa significa e come evitarlo.

### 🔎 Cos’è un JSON non valido?
- Il JSON deve rispettare regole precise di sintassi (standard)
- Se non segui queste regole, il server non riuscirà a capire il messaggio
- Il server non corregge il tuo JSON: devi inviare dati corretti

### ⚠️ Errori comuni
1. **Stringhe senza doppie virgolette**
   - ❌ `{ "firstname": John }` (non valido)
   - ✅ `{ "firstname": "John" }` (valido)
2. **Uso di virgolette singole**
   - ❌ `{ 'firstname': 'John' }` (non valido)
   - ✅ `{ "firstname": "John" }` (valido)
3. **Mancanza di virgole tra coppie chiave/valore**
   - ❌ `{ "firstname": "John" "age": 29 }` (non valido)
   - ✅ `{ "firstname": "John", "age": 29 }` (valido)
4. **Virgola finale non necessaria**
   - ❌ `{ "firstname": "John", "age": 29, }` (non valido)
   - ✅ `{ "firstname": "John", "age": 29 }` (valido)
5. **Parentesi graffe non chiuse**
   - ❌ `{ "contact": { "email": "john@example.com" }` (non valido)
   - ✅ `{ "contact": { "email": "john@example.com" } }` (valido)

### 🛠️ Come validare il JSON
- Postman ha un validatore integrato: se il JSON è errato, vedrai un avviso rosso nell’editor
- Se invii JSON non valido, il server potrebbe restituire una risposta nulla o un errore
- Puoi usare siti come [jsonlint.com](https://jsonlint.com) per validare e formattare il tuo JSON

### 🧑‍💻 Esempio pratico in Postman
- Se invii JSON non valido, Postman ti mostra l’errore (es: “expected comma” o “value expected”)
- Se la risposta contiene `json: null`, significa che il server non ha capito i dati
- Correggi l’errore seguendo le regole sopra

### 💡 Consigli didattici
- Controlla sempre che non ci siano avvisi rossi nell’editor di Postman
- Usa validator online se non riesci a trovare l’errore
- Un JSON valido è fondamentale per lavorare con le API

> Se la tua richiesta non funziona, controlla prima la validità del JSON!

---

## 🚗 Come creare una POST request

Vediamo come aggiungere una nuova auto alla Car Fleet Management API usando Postman.

### 1️⃣ Consulta la documentazione Swagger
- Trova l’endpoint `POST /cars` (serve per aggiungere una nuova auto)
- Swagger mostra la struttura JSON richiesta per il body della richiesta

### 2️⃣ Crea la richiesta in Postman
- Apri una nuova tab in Postman
- Inserisci l’URL: `{{base_url}}/cars`
- Imposta il metodo su **POST**
- Vai su **Body** > seleziona **raw** > scegli **JSON** dal menu a tendina
- Inserisci il JSON della nuova auto, ad esempio:

```json
{
  "build": 0,
  "id": 0,
  "manufacturer": "string",
  "model": "string"
}
```

- Premi **Send**
- La risposta conterrà la nuova auto, inclusa l’ID generata dal server:

```json
{
  "build": 0,
  "id": 0,
  "manufacturer": "string",
  "model": "string"
}
```

### 3️⃣ Note pratiche
- L’ID non è obbligatoria: viene generata dal server
- Puoi aggiungere più auto ripetendo la richiesta con dati diversi
- Dopo aver aggiunto una nuova auto, puoi fare una GET su `/cars` per vedere la lista aggiornata

### 4️⃣ Salva la richiesta
- Salva la richiesta come `Add new car` nella tua Collection

> 💡 **Nota didattica:**
> - Il metodo **POST** serve per creare nuove risorse
> - Il body deve essere in formato JSON valido
> - Postman ti aiuta a formattare e validare il JSON

Nella prossima parte vedremo come gestire errori comuni nelle richieste POST e come modificare una risorsa con PUT.

---

## ⚠️ Common errors nelle API

Quando lavori con le API e Postman, ci sono alcuni errori tipici che puoi incontrare. Ecco i più comuni e come evitarli:

### 1️⃣ Errore di path (404 Not Found)
- Se scrivi l’endpoint sbagliato (es: `/car` invece di `/cars`), riceverai **404 Not Found**
- Le API sono case sensitive: `/Cars` ≠ `/cars`
- Controlla sempre la documentazione e copia l’URL esatto

### 2️⃣ Errori nei nomi dei campi JSON
- Se usi un campo con nome sbagliato (es: `Manufacturer` invece di `manufacturer`), il server potrebbe:
  - Restituire un errore
  - Ignorare il campo e non salvarlo
- I nomi dei campi devono essere identici a quelli richiesti dalla documentazione

### 3️⃣ Errori di sintassi JSON
- Mancanza di virgole, virgolette, parentesi graffe
- Postman mostra un avviso rosso se il JSON non è valido
- Il server restituirà **400 Bad Request** se il JSON è errato

### 4️⃣ Consigli pratici
- Copia e incolla i nomi dei campi e gli endpoint dalla documentazione
- Se qualcosa non funziona, riparti da zero e ricostruisci la richiesta
- Fai attenzione a maiuscole/minuscole e alla sintassi
- Se ricevi un errore, controlla prima la validità del JSON e la correttezza dell’endpoint

> 💡 Sbagliare fa parte del processo di apprendimento! Più errori risolvi, più diventi esperto nell’uso delle API.

---

## 🏋️‍♂️ Assignment - POST

Metti in pratica la creazione di una riparazione per un’auto tramite due endpoint diversi:
- `POST /cars/repairs` (aggiungi una riparazione specificando il carId nel body)
- `POST /cars/{carId}/repairs` (aggiungi una riparazione specificando il carId nell’URL)

### Obiettivi
- Consulta la documentazione Swagger per vedere la struttura richiesta
- Prova entrambi gli endpoint in Postman
- Presta attenzione a dove inserire il carId (body o URL)
- Salva le richieste nella tua Collection

---

## ✅ Assignment solution - POST

### 1️⃣ Endpoint: `POST /cars/repairs`
- In Postman, crea una nuova richiesta `POST` su `{{base_url}}/cars/repairs`
- Nel body (JSON), inserisci:

```json
{
  "carId": 4,
  "repairDate": "2025-12-15",
  "description": "Cambio olio"
}
```

- Premi **Send**: la risposta confermerà l’aggiunta della riparazione
- Puoi verificare con una GET su `/cars/4/repairs` che la riparazione sia stata aggiunta

### 2️⃣ Endpoint: `POST /cars/{carId}/repairs`
- Duplica la richiesta precedente
- Cambia l’URL in `{{base_url}}/cars/4/repairs` (sostituisci `4` con l’ID desiderato)
- Nel body (JSON), inserisci solo i dati della riparazione (senza carId):

```json
{
  "repairDate": "2025-12-16",
  "description": "Cambio pneumatici"
}
```

- Premi **Send**: la risposta confermerà l’aggiunta della riparazione
- Verifica con una GET su `/cars/4/repairs` che la riparazione sia presente

### 🔄 Differenze tra i due endpoint
- Nel primo caso, il carId è nel body
- Nel secondo caso, il carId è nell’URL
- Il risultato è lo stesso: una riparazione associata all’auto

### 💡 Consigli didattici
- Segui la documentazione per capire dove inserire i parametri
- Prova entrambe le modalità per capire le differenze
- Salva le richieste per riutilizzarle e testare altri casi

> Sperimenta, sbaglia e impara: è il modo migliore per diventare esperto con le API!

---

## 🔄 GET vs POST & Cos’è una Cache

### 🚙 GET
- Serve per **ottenere dati** dal server (es: lista auto, dettagli riparazione)
- I parametri si specificano nell’URL (query o path parameters)
- Non ha un body
- Può essere **cacheata**: la risposta può essere salvata per richieste future

### 🛠️ POST
- Serve per **creare nuovi dati** (es: aggiungere auto, aggiungere riparazione)
- I parametri possono essere sia nell’URL che nel body
- Il body contiene i dati da creare (tipicamente in JSON)
- **Non viene cacheata**: ogni richiesta crea una nuova risorsa

### 🗄️ Cos’è una cache?
- Un sistema che memorizza le risposte più richieste per velocizzare le future richieste
- Quando un client fa una richiesta GET, la risposta può essere salvata nella cache
- Se la stessa richiesta viene fatta di nuovo, la cache restituisce la risposta senza interrogare il database principale
- Riduce il carico sul server e velocizza le risposte

#### Schema semplificato:
```
Client → Cache → Server → Database
```
- Se la cache ha la risposta, la invia subito al client
- Se la cache non ha la risposta, chiede al server/database e poi la memorizza

### 💡 Perché solo GET è cacheabile?
- GET recupera dati che possono essere uguali per più utenti
- POST crea nuovi dati: la risposta è unica per ogni richiesta, quindi non ha senso cachearla

> **In sintesi:**
> - Usa GET per leggere dati, POST per crearli
> - Solo GET può essere cacheata
> - La cache rende le API più veloci e scalabili

---

## ✏️ Come creare una PUT request

Vediamo come aggiornare una risorsa (auto) esistente usando il metodo PUT in Postman.

### 1️⃣ Consulta la documentazione Swagger
- Trova l’endpoint `PUT /cars` (serve per aggiornare un’auto)
- La documentazione mostra la struttura JSON richiesta

### 2️⃣ Crea la richiesta in Postman
- Duplica la richiesta GET o POST su `/cars`
- Cambia il metodo in **PUT**
- Vai su **Body** > seleziona **raw** > scegli **JSON**
- Incolla l’oggetto auto che vuoi aggiornare, ad esempio:

```json
{
  "id": 3,
  "manufacturer": "Tesla",
  "model": "Cybertruck",
  "build": 2021
}
```

- Premi **Send**
- La risposta confermerà l’aggiornamento dell’auto
- Verifica con una GET su `/cars` che l’auto sia stata aggiornata

### 3️⃣ Regole importanti per PUT
- Devi inviare **tutti i dati** della risorsa che vuoi aggiornare
- Devi includere l’**ID** nel body: senza ID la richiesta non è valida
- L’ID deve esistere nel database, altrimenti ricevi **404 Not Found**

### 4️⃣ Nota su POST vs PUT
- Alcune API permettono di aggiornare anche con POST, ma non è una regola
- PUT è il metodo corretto per aggiornare una risorsa esistente

### 💡 Consigli didattici
- Copia la struttura dell’oggetto dalla risposta GET per evitare errori
- Se ricevi un errore, controlla che l’ID sia presente e corretto
- Salva la richiesta come `Update car` nella tua Collection

> Usa PUT per aggiornare risorse esistenti, POST per crearne di nuove!


