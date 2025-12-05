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


