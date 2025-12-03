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


