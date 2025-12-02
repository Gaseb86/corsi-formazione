# Sezione 13: Github Grab Bag: Odds & Ends

## Github Repo visibility: Public Vs. Private

Su GitHub puoi scegliere se rendere un repository pubblico o privato:

- **Pubblico:** Tutti possono vedere, cercare e clonare il repository. Nessuno può modificarlo o fare push, a meno che non sia stato aggiunto come collaboratore.
- **Privato:** Solo il proprietario e i collaboratori esplicitamente invitati possono vedere e accedere al repository. Gli altri utenti non vedranno il repository né potranno accedervi.

Quando crei un nuovo repository, puoi scegliere la visibilità. Puoi anche cambiarla in seguito dalle impostazioni del repository (Settings → Options → Danger Zone → Change repository visibility).

Attenzione: se rendi privato un repository pubblico, chiunque lo stava seguendo o aveva messo una stella perderà l’accesso. Wiki, pull request e altre funzioni pubbliche saranno limitate.

Consiglio: per progetti personali o demo, inizia con un repository privato e rendilo pubblico solo quando vuoi condividerlo.

## Adding Github Collaborators

Per permettere ad altri utenti di collaborare su un repository (cioè poter fare push), devi aggiungerli come collaboratori:

- Vai su Settings → Manage Access del repository
- Cerca il loro username o email GitHub
- Invia l’invito: il collaboratore riceverà una mail e dovrà accettare
- Una volta accettato, potrà vedere e fare push sul repository (anche se privato)

**Attenzione:**
- Solo il proprietario può gestire collaboratori e accedere alle impostazioni
- I collaboratori non possono eliminare il repository o gestire altri collaboratori
- In organizzazioni o aziende, i permessi possono essere più granulari

Consiglio: aggiungi collaboratori solo di cui ti fidi, perché potranno modificare il codice e fare push direttamente.

## What are READMEs?

Il file README (di solito README.md) è un file speciale che si trova nella radice del repository e serve a spiegare il progetto agli utenti che lo visitano.

Cosa dovrebbe contenere:

GitHub mostra automaticamente il contenuto del README nella pagina principale del repository, rendendolo la "porta d’ingresso" per chiunque voglia capire o usare il progetto.

Il README è scritto in Markdown (estensione .md), un linguaggio semplice per formattare testo, link, elenchi, titoli e altro.

Consiglio: cura il README, è la prima cosa che chi visita il tuo progetto leggerà e può fare la differenza tra un progetto usato e uno ignorato.

## Come aggiungere un README a un progetto

Vediamo passo-passo come aggiungere un file README.md a un repository Git, con un esempio pratico:

### 1. Assicurati di avere le ultime modifiche
Prima di aggiungere nuovi file, è buona pratica aggiornare la tua copia locale:

```bash
git pull origin main
```

### 2. Crea il file README.md
Il file README.md va nella radice del progetto. Puoi crearlo con un editor di testo o direttamente da terminale:

```bash
echo "# Nome del progetto\n\nBreve descrizione del progetto." > README.md
```
Oppure apri README.md in VS Code e scrivi:

```markdown
# bookish disco

bookish disco è un nome di repository generato casualmente da GitHub. Questo progetto non fa nulla, è solo una demo per un corso su Git/GitHub.
```

### 3. (Opzionale) Migliora la formattazione
Puoi aggiungere grassetto, link, elenchi, ecc. Esempio:

```markdown
# bookish disco

**bookish disco** è un nome di repository generato casualmente da GitHub. Questo progetto non fa nulla, è solo una demo per un corso su Git/GitHub.
```

### 4. Aggiungi e committa il README
Salva il file, poi aggiungilo e crea un commit:

```bash
git add README.md
git commit -m "Aggiungi README file"
```

### 5. Fai push su GitHub
Invia le modifiche al repository remoto:

```bash
git push origin main
```

### 6. Collaboratori: come ricevere il README
Se un collaboratore vuole ricevere il nuovo README, basta eseguire:

```bash
git pull origin main
```

Ora il file README.md sarà visibile sia localmente che su GitHub, dove verrà mostrato automaticamente nella pagina principale del repository.

**Nota:** Il README è spesso la prima cosa che vedono i recruiter o chi visita il tuo progetto. Anche se non è obbligatorio all’inizio, è una buona abitudine aggiungerlo presto!

## A Markdown Crash Course

Markdown è un linguaggio di markup semplice che permette di formattare testo in modo leggibile e veloce, trasformandolo in HTML. Su GitHub, i file README.md sono scritti in Markdown e vengono automaticamente convertiti e visualizzati come pagine ben formattate.

### Elementi principali di Markdown:
- **Titoli:**
  ```
  # Titolo principale
  ## Sottotitolo
  ### Titolo di terzo livello
  ```
- **Grassetto e corsivo:**
  ```
  **grassetto**
  *corsivo*
  ```
- **Liste puntate e numerate:**
  ```
  - Primo elemento
  - Secondo elemento
  1. Primo
  2. Secondo
  ```
- **Link:**
  ```
  [Testo del link](https://www.sito.com)
  ```
- **Immagini:**
  ```
  ![Alt text](https://url-immagine.com)
  ```
- **Blocchi di codice:**
  ```
  `codice inline`
  
  ```js
  console.log("Hello!")
  ```
  ```
- **Citazioni:**
  ```
  > Questo è un blocco citazione
  ```
- **Linee orizzontali:**
  ```
  ---
  ```

Markdown supporta anche tabelle, emoji, e altre funzionalità avanzate. Su GitHub, puoi vedere l’anteprima dei file Markdown direttamente nell’interfaccia web o tramite estensioni in VS Code.

Consiglio: usa Markdown per rendere i tuoi README chiari, ordinati e facili da leggere!

Link utili:
- [Prova md](https://markdown-it.github.io/)
- [Tutta la sinassi md](https://daringfireball.net/projects/markdown/basics)

## Github Gists: condividere snippet di codice

I **GitHub Gists** sono uno strumento semplice per condividere rapidamente frammenti di codice, note, configurazioni o qualsiasi file di testo. Sono simili a servizi come Pastebin, ma integrati nell’ecosistema GitHub.

### Caratteristiche principali:
- Puoi creare gists pubblici (visibili a tutti) o segreti (visibili solo a chi ha il link)
- Ogni gist può contenere uno o più file, di qualsiasi estensione
- Puoi commentare, modificare, scaricare, condividere e anche "forkare" un gist
- I gists hanno una cronologia delle revisioni e puoi vedere le differenze tra versioni

### Come creare un gist
1. Vai su [gist.github.com](https://gist.github.com) oppure dal tuo profilo GitHub clicca su "Your gists"
2. Inserisci il nome del file (es: `esempio.md` o `script.js`)
3. Scrivi il contenuto del file
4. (Opzionale) Aggiungi una descrizione
5. Scegli se renderlo pubblico o segreto
6. Clicca su "Create public gist" o "Create secret gist"

### Esempio pratico
Supponiamo di voler condividere una configurazione SSH:

1. Vai su gist.github.com
2. Inserisci come nome file: `config-ssh.md`
3. Incolla le istruzioni o il codice
4. Crea il gist e condividi il link con chi vuoi

### Quando usare i gists?
- Per condividere rapidamente snippet di codice su forum, chat, email
- Per salvare appunti o soluzioni che vuoi ritrovare facilmente
- Per collaborare su piccoli script senza creare un intero repository

**Nota:** I gists sono in realtà dei mini-repository Git dietro le quinte, ma l’interfaccia è molto semplificata rispetto a un normale repository GitHub.

**Consiglio:** Se devi condividere un singolo file o una piccola raccolta di script, usa un gist. Se invece il progetto cresce, passa a un repository completo!

## Github Pages: pubblicare siti statici gratis

**GitHub Pages** è una funzionalità di GitHub che permette di ospitare gratuitamente siti web statici direttamente da un repository. È ideale per portfolio, documentazione, demo di progetti, giochi JavaScript, e molto altro.

### Caratteristiche principali
- Hosting gratuito per siti statici (solo HTML, CSS, JavaScript)
- Non supporta linguaggi server-side (Python, Node, PHP, ecc.)
- Ogni repository può avere il suo sito associato
- L’URL sarà del tipo `username.github.io/nome-repo`
- Puoi anche avere un sito personale unico: `username.github.io`
- Possibilità di personalizzare il dominio (avanzato)

### Esempi pratici
- Documentazione di una libreria (es: Faker → `fakerjs.github.io`)
- Demo di un gioco (es: 2048-AI → `ovolve.github.io/2048-AI`)
- Portfolio personale → `tuonome.github.io`

### Tipi di Github Pages
- **Project site:** Un sito per ogni repository (`username.github.io/nome-repo`)
- **User/Organization site:** Un solo sito personale per account (`username.github.io`)

### Quando usare GitHub Pages?
- Per mostrare progetti, portfolio, demo, documentazione
- Per condividere facilmente siti statici senza costi

### Limiti
- Solo siti statici (no backend, database, login, ecc.)
- Non adatto a siti con molto traffico o esigenze avanzate

**Consiglio:** Se vuoi pubblicare la documentazione di un progetto, una demo o il tuo portfolio, GitHub Pages è una soluzione semplice e gratuita!

## Guida pratica: pubblicare un sito con Github Pages

Vediamo come creare e pubblicare un sito statico con GitHub Pages, partendo da zero:

### 1. Crea o scegli un repository
Puoi usare un repository esistente o crearne uno nuovo su GitHub (es: "chickens").

### 2. Prepara i file localmente
Inizia con una cartella locale, aggiungi i file che vuoi (es: `chickens.txt`, `index.html`).

### 3. Inizializza Git e fai il primo commit
```bash
git init
git add .
git commit -m "Initial commit"
```

### 4. Imposta il branch principale come "main"
```bash
git branch -M main
```

### 5. Collega il repository remoto e fai push
```bash
git remote add origin https://github.com/tuonome/chickens.git
git push -u origin main
```

### 6. Crea il branch per GitHub Pages (es: gh-pages)
```bash
git switch -c gh-pages
```

### 7. Aggiungi il file index.html
Assicurati che ci sia un file `index.html` nella radice del progetto. Esempio:

```html
<!-- index.html -->
<html>
  <head>
    <title>Chickens!</title>
    <link rel="stylesheet" href="app.css">
  </head>
  <body>
    <h1>Chickens!</h1>
    <p>Un sito demo con GitHub Pages.</p>
  </body>
</html>
```

Puoi aggiungere anche un file CSS (`app.css`) se vuoi.

### 8. Fai commit e push del branch gh-pages
```bash
git add .
git commit -m "Aggiungi index.html e app.css"
git push origin gh-pages
```

### 9. Attiva GitHub Pages dalle impostazioni del repository
- Vai su GitHub → Settings → Pages
- Scegli il branch da pubblicare (es: gh-pages)
- Scegli la cartella (di solito "root")
- Salva: vedrai l’URL del sito generato (`tuonome.github.io/chickens`)

### 10. Aggiorna il sito
Per modificare il sito, aggiorna i file su gh-pages, fai commit e push. Le modifiche saranno visibili dopo pochi minuti.

**Nota:** Puoi usare anche il branch main se contiene index.html, oppure una cartella "docs".

**Consiglio:** Usa il branch gh-pages per separare il sito dal codice del progetto!


