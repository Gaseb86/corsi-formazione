# Sezione 1: Introduction to APIs

## 📜 Breve storia delle API

Le API (Application Programming Interface) sono nate con l’obiettivo di riutilizzare funzionalità e ridurre errori, già dagli anni ‘50, quando i computer occupavano intere stanze. Il concetto di libreria come raccolta di programmi riutilizzabili è il primo passo verso le API.

Negli anni ‘70 nasce l’idea di interfaccia: un modo per separare l’applicazione dall’hardware, permettendo di sostituire parti del sistema senza modificare tutto. Un’interfaccia è come una presa elettrica: standardizzata, permette di collegare dispositivi diversi.

## 🌐 API di rete: RPC, XML-RPC, SOAP, REST, GraphQL

- **1980s: RPC (Remote Procedure Call)**
  - Permette a un computer di invocare funzioni su un altro computer tramite la rete.
  - Esempio: Computer A chiede a Computer B di sommare 5 + 6; B esegue e restituisce il risultato.
  - Sun RPC è una delle prime implementazioni.

- **1998: XML-RPC**
  - Usa XML per codificare i messaggi tra client e server.
  - Permette a software diversi di comunicare grazie a un formato standard.

- **1999: SOAP (Simple Object Access Protocol)**
  - Usa XML per inviare/ricevere messaggi secondo regole precise.
  - Molto usato in aziende e sistemi legacy, ancora oggi presente.

- **2000: REST (Representational State Transfer)**
  - Non è un protocollo, ma uno stile architetturale per progettare API.
  - Oggi è lo standard per le API web.

- **2015: GraphQL**
  - Introdotto da Facebook come alternativa a REST.
  - Permette di descrivere e richiedere dati in modo flessibile.

## 📈 Trend e diffusione
- SOAP era molto popolare, ma oggi è in calo.
- REST è lo standard più diffuso per le API web moderne.
- GraphQL è in forte crescita, soprattutto nei nuovi progetti.

## 💡 Cosa ricordare
- Le API esistono da decenni e non sono una novità.
- Oggi le API di rete sono fondamentali per la comunicazione tra sistemi diversi.
- REST e GraphQL sono le tecnologie più rilevanti per lo sviluppo moderno, ma SOAP è ancora presente in sistemi legacy.

## 🤔 Perché servono le API? Esempio di chiamata RPC

Le API nascono dalla necessità di far collaborare programmi diversi, spesso scritti in linguaggi diversi e che girano su server separati. In pratica, le API permettono di:
- Recuperare dati da fonti esterne (es: database, servizi online)
- Delegare calcoli o azioni a sistemi specializzati
- Unificare l’accesso a risorse e funzioni, anche se non sono locali

### 🧑‍💻 Esempio: chiamata locale vs. chiamata remota

#### 1. Chiamata locale (tutto nello stesso programma)
```javascript
function add(a, b) {
  return a + b;
}

function run() {
  const result = add(1, 4);
  console.log(result); // 5
}
run();
```
Qui tutto avviene localmente: il programma chiama la funzione `add` e ottiene il risultato.

#### 2. Chiamata remota (RPC)
Supponiamo che la funzione `add` sia su un altro server, magari scritta in C++ e non accessibile direttamente. Usiamo una chiamata RPC:
```javascript
function makeRpcCall(a, b) {
  // Esempio semplificato: chiama un servizio HTTP che somma i numeri
  fetch(`https://api.example.com/add?a=${a}&b=${b}`)
    .then(response => response.json())
    .then(data => console.log(data.result));
}

function run() {
  makeRpcCall(1, 5); // Il calcolo avviene su un altro server
}
run();
```
Qui il programma delega il calcolo a un altro sistema, che può essere scritto in qualsiasi linguaggio e girare ovunque.

### 🔗 Cosa ci permette di fare un’API?
- Recuperare dati (es: nome cliente, prodotti) da database o servizi esterni
- Eseguire azioni (es: calcolare tasse, accendere una luce) su sistemi remoti
- Costruire applicazioni moderne che integrano funzionalità di altri sistemi

> Le API sono il ponte tra applicazioni, servizi e dispositivi diversi. Permettono di costruire software più potente, flessibile e integrato.

