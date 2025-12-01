# Sezione 11: GitHub - Le Basi

## Cosa fa GitHub per noi?

GitHub è principalmente una piattaforma online che ospita repository Git. Permette di salvare i nostri progetti nel cloud, accedervi da qualsiasi luogo, condividerli e collaborare con altre persone. La caratteristica fondamentale di GitHub è proprio la collaborazione: più utenti possono lavorare insieme sugli stessi progetti, proporre modifiche, discutere e migliorare il codice.

### Differenza tra Git e GitHub
- **Git** è un sistema di controllo versione che funziona localmente sul nostro computer. Non richiede internet né un account.
- **GitHub** è un sito web che ospita repository Git. Per usarlo serve una connessione internet e un account. GitHub facilita la collaborazione e la condivisione, ma Git può essere usato anche senza GitHub.

### Perché usare GitHub?
- **Backup:** Possiamo salvare il nostro lavoro su GitHub e recuperarlo in caso di problemi al computer.
- **Collaborazione:** Altri sviluppatori e collaboratori possono accedere al repository, proporre modifiche e lavorare insieme.
- **Crescita del progetto:** Se il progetto cresce, è possibile lavorare con decine o centinaia di collaboratori.

### Alternative a GitHub
Esistono altre piattaforme simili, come GitLab e Bitbucket, ma GitHub è la più diffusa e usata al mondo, sia da sviluppatori indipendenti che da grandi aziende.

### Costi e funzionalità
GitHub offre un piano gratuito molto completo: repository pubblici e privati illimitati, collaboratori illimitati e molte funzionalità utili. I piani a pagamento sono pensati soprattutto per aziende e grandi team, con funzioni avanzate di sicurezza e gestione.

### Altre funzionalità
Oltre all’hosting dei repository, GitHub offre:
- Discussioni e commenti sul codice
- Gestione delle modifiche e delle revisioni
- Ambiente di sviluppo online (Codespaces)
- Automazioni (GitHub Actions)
- Analisi di sicurezza automatica

In sintesi, GitHub è il luogo ideale per dare una "casa" al proprio codice, facilitare la collaborazione e sfruttare strumenti avanzati per lo sviluppo.
## Perché dovresti usare GitHub?

Oltre al backup e alla collaborazione, GitHub offre vantaggi fondamentali per chi fa parte della comunità degli sviluppatori:

- **Open Source:** GitHub è la casa dei progetti open source. Qui puoi trovare, studiare e contribuire a migliaia di progetti pubblici, come React o TensorFlow. Partecipare a progetti open source ti permette di imparare, migliorare le tue competenze e collaborare con una comunità globale.

- **Visibilità e lavoro:** Il tuo profilo GitHub può diventare una sorta di curriculum online. I datori di lavoro spesso guardano le tue attività, i progetti a cui hai contribuito e il codice che hai scritto. Contribuire a progetti noti può aumentare le tue opportunità lavorative.

- **Networking e mentorship:** Collaborando su GitHub puoi conoscere altri sviluppatori, trovare mentori e costruire relazioni professionali. Le discussioni e le revisioni del codice favoriscono lo scambio di idee e la crescita personale.

- **Aggiornamento continuo:** GitHub ha funzioni simili a un social network. Puoi seguire progetti, ricevere notifiche sulle novità e restare aggiornato sulle evoluzioni delle tecnologie che ti interessano.

In sintesi, usare GitHub non solo ti aiuta a gestire il codice, ma ti offre opportunità di crescita, visibilità e connessione con la comunità globale degli sviluppatori.

## Clonare repository GitHub con `git clone`

Clonare un repository significa copiare sul proprio computer tutti i file e la storia di un progetto che si trova online, tipicamente su GitHub. Il comando da usare è:

```
git clone URL-del-repository
```

Dove "URL-del-repository" è l’indirizzo del repository su GitHub (o su altre piattaforme come GitLab o Bitbucket). Questo comando crea una nuova cartella con tutti i file e la cronologia del progetto.

**Passaggi principali:**
- Assicurati di non essere già dentro una cartella gestita da Git (controlla con `git status`).
- Vai nella cartella dove vuoi scaricare il progetto.
- Esegui `git clone` seguito dall’URL del repository.
- Verrà creata una nuova cartella con il progetto e tutta la sua storia.

**A cosa serve clonare?**
- Per studiare il codice di altri progetti.
- Per sperimentare e modificare il codice localmente.
- Per contribuire a progetti open source: puoi fare modifiche e poi proporle agli autori.

Clonare un repository ti dà accesso a tutti i file, ai commit e ai contributi fatti nel tempo. È un’operazione fondamentale per chi vuole lavorare con progetti condivisi o open source.

### Clonare repository non GitHub

Il comando `git clone` funziona con qualsiasi repository Git ospitato online, non solo quelli su GitHub. Puoi clonare repository da GitLab, Bitbucket o anche da server privati aziendali.

**Permessi di clonazione:**
- Se un repository è pubblico e visibile, puoi clonarlo liberamente e modificarlo sul tuo computer.
- Non puoi però inviare (push) le tue modifiche direttamente su repository che non possiedi: per contribuire, dovrai seguire un workflow specifico (come le pull request).
- Se il repository è privato, non potrai vederlo né clonarlo senza autorizzazione.

In sintesi, `git clone` è un comando di Git, non di GitHub, e ti permette di lavorare con qualsiasi progetto ospitato online, a patto che tu abbia accesso al repository.

## Configurazione di GitHub e SSH su Windows

### 1. Registrazione su GitHub
Vai su [github.com](https://github.com) e crea un account scegliendo username, email e password. Usa una email reale, perché dovrai confermarla. È consigliato usare la stessa email che hai configurato in Git (`git config user.email`) per collegare correttamente le tue attività locali al profilo GitHub.

### 2. Configurazione della chiave SSH
Per interagire con GitHub dal terminale senza dover inserire username e password ogni volta, si usa una chiave SSH. Ecco come fare su Windows:

**a. Verifica se hai già una chiave SSH:**
Apri PowerShell e digita:
```
ls ~/.ssh
```
Se vedi file come `id_ed25519.pub` o `id_rsa.pub`, hai già una chiave. Altrimenti, puoi crearne una nuova.

**b. Genera una nuova chiave SSH:**
Nel terminale, esegui:
```
ssh-keygen -t ed25519 -C "la-tua-email@esempio.com"
```
Premi Enter per accettare il percorso predefinito e inserisci una passphrase (opzionale, ma consigliata per sicurezza).

**c. Aggiungi la chiave all’SSH agent:**
Avvia l’agent:
```
eval $(ssh-agent -s)
```
Poi aggiungi la chiave:
```
ssh-add ~/.ssh/id_ed25519
```

**d. Copia la chiave pubblica:**
Usa questo comando per copiare la chiave negli appunti:
```
cat ~/.ssh/id_ed25519.pub | clip
```

**e. Aggiungi la chiave a GitHub:**
Vai su GitHub → Settings → SSH and GPG keys → New SSH key. Incolla la chiave copiata, dai un nome (es. "Laptop Windows") e salva.

### Note importanti
- Se usi una passphrase, ti verrà chiesta quando usi la chiave.
- La configurazione SSH va fatta una sola volta per ogni macchina.
- Se usi un nome file diverso per la chiave, ricordati di specificarlo nei comandi.

Questa configurazione ti permette di lavorare in modo sicuro e comodo con GitHub da Windows, senza dover inserire le credenziali ogni volta che esegui operazioni come push o pull.

## Creare il primo repository su GitHub

Per pubblicare il tuo codice su GitHub, puoi seguire due approcci principali:

### 1. Hai già un repository locale
Se hai già un progetto gestito con Git sul tuo computer:
1. Accedi a GitHub e crea un nuovo repository vuoto (clicca su "New" o sul pulsante verde "Create repository").
2. Dai un nome al repository, scegli se renderlo pubblico o privato e aggiungi una descrizione (opzionale).
3. Una volta creato, GitHub ti mostrerà le istruzioni per collegare il tuo repository locale a quello remoto:
	 - Aggiungi il remote:
		 ```
		 git remote add origin https://github.com/tuo-username/nome-repo.git
		 ```
	 - Poi esegui il push:
		 ```
		 git push -u origin master
		 ```
	 (Sostituisci "master" con il nome del tuo branch principale, ad esempio "main")

### 2. Vuoi iniziare da zero su GitHub
Se non hai ancora un repository locale:
1. Crea un nuovo repository vuoto su GitHub.
2. Clona il repository appena creato sul tuo computer:
	 ```
	 git clone https://github.com/tuo-username/nome-repo.git
	 ```
3. Entra nella cartella appena clonata e inizia a lavorare normalmente con Git.

**Nota:** Se cloni un repository da GitHub, il collegamento tra locale e remoto è già configurato. Se invece hai già un progetto locale, devi aggiungere manualmente il remote.

Questi passaggi ti permettono di pubblicare il tuo lavoro su GitHub e iniziare a collaborare online.

## Git remotes: collegare il repository locale a GitHub

Un "remote" in Git è semplicemente un riferimento (un nome) associato a un URL che indica dove si trova un repository remoto, ad esempio su GitHub, GitLab o Bitbucket. Il remote più comune si chiama `origin`.

### Come vedere i remoti configurati
Per vedere i remoti già configurati nel tuo repository:
```
git remote -v
```
Se hai appena creato il repository locale con `git init`, non ci saranno remoti. Se invece hai clonato un repository, il remote `origin` sarà già impostato.

### Come aggiungere un remote
Se hai creato un repository locale e vuoi collegarlo a GitHub:
```
git remote add origin https://github.com/tuo-username/nome-repo.git
```
`origin` è solo un nome convenzionale, puoi scegliere qualsiasi nome, ma `origin` è lo standard.

### Come rinominare o rimuovere un remote
- Per rinominare:
    ```
    git remote rename vecchio-nome nuovo-nome
    ```
- Per rimuovere:
    ```
    git remote remove nome-remote
    ```

### Perché i remoti sono utili?
I remoti ti permettono di:
- Inviare (push) il tuo codice su GitHub
- Scaricare (pull/fetch) aggiornamenti dal repository remoto
- Collaborare con altri sviluppatori

Nei progetti open source avanzati, puoi avere più remoti (ad esempio, uno per il repository principale e uno per il tuo fork). Ma per la maggior parte dei casi, basta `origin`.


## Pushing: caricare il codice su GitHub con `git push`

Una volta collegato il repository locale a GitHub tramite un remote (di solito chiamato `origin`), puoi caricare il tuo codice su GitHub usando il comando `git push`.

### Sintassi di base
```
git push <remote> <branch>
```
Esempio tipico:
```
git push origin master
```
Oggi il branch principale si chiama spesso `main`, quindi puoi usare:
```
git push origin main
```

### Cosa succede quando fai push?
- Tutti i commit del branch selezionato vengono caricati su GitHub.
- Se hai più branch, puoi caricare anche quelli:
	```
	git push origin nome-branch
	```
- Dopo il push, su GitHub vedrai i file aggiornati, i nuovi commit e i branch disponibili.

### Note importanti
- GitHub non si aggiorna automaticamente: ogni volta che fai modifiche locali, devi eseguire `git push` per sincronizzare.
- Puoi fare push su qualsiasi branch, non solo su quello principale.
- Se hai configurato SSH, non ti verrà chiesta la password ad ogni push.

In sintesi, `git push` è il comando che rende visibile il tuo lavoro su GitHub e permette la collaborazione con altri sviluppatori.

## Esplorare un repository su GitHub

Quando il tuo codice è su GitHub, puoi:

- **Visualizzare i file:** Puoi leggere e navigare tra i file del progetto direttamente dal browser.
- **Cambiare branch:** Puoi passare da un branch all’altro per vedere le differenze tra le versioni del progetto.
- **Vedere i commit:** Cliccando sul numero dei commit, puoi vedere la lista di tutte le modifiche fatte nel tempo, con messaggi, hash e dettagli su quali file sono stati modificati.
- **Analizzare le modifiche:** Puoi vedere quali righe sono state aggiunte, rimosse o modificate in ogni commit.
- **Commentare i commit:** Puoi lasciare commenti su singoli commit, utile per la collaborazione e la revisione del codice.

Ricorda: se non vedi le modifiche che ti aspetti, controlla di essere sul branch giusto! Su GitHub puoi sempre cambiare branch per vedere lo stato aggiornato dei file e dei commit.

In futuro imparerai anche a gestire pull request e confrontare le modifiche tra branch, strumenti fondamentali per la collaborazione.


## Esercizio pratico: add, commit, push su più branch

Il workflow di base per lavorare con Git e GitHub è:
1. Fai modifiche ai file locali
2. Aggiungi le modifiche con `git add`
3. Salva le modifiche con `git commit`
4. Carica le modifiche su GitHub con `git push`

Puoi ripetere questi passaggi su qualsiasi branch:
- Passa al branch desiderato con `git switch nome-branch`
- Fai le modifiche, aggiungi e committa
- Esegui `git push origin nome-branch` per caricare il branch su GitHub

Ricorda:
- Ogni branch può avere commit diversi che esistono solo localmente finché non vengono pushati
- Puoi scegliere quali branch caricare su GitHub
- Di solito si lavora su branch di sviluppo/feature e si merge nel branch principale prima di fare il push

Questo workflow ti permette di gestire più versioni del progetto e collaborare in modo efficace.

## Branch locali e remoti: approfondimento su `git push`

Quando usi `git push`, puoi:
- Creare un nuovo branch remoto su GitHub se non esiste ancora
- Aggiornare un branch remoto già esistente

Di default, il comando:
```
git push origin master
```
prende il branch locale `master` e lo sincronizza con il branch remoto `master` su GitHub. Se il branch remoto non esiste, viene creato.

Puoi anche spingere un branch locale su un branch remoto con nome diverso:
```
git push origin nome-branch-locale:nome-branch-remoto
```
Esempio:
```
git push origin cats:master
```
Questo comando prende il branch locale `cats` e lo carica sul branch remoto `master`.

Questa flessibilità permette di gestire situazioni particolari, ma nella maggior parte dei casi si preferisce mantenere lo stesso nome tra branch locale e remoto.

Ricorda: ogni push aggiorna solo il branch specificato, e puoi avere branch locali che non sono ancora stati caricati su GitHub.


## Cosa significa `git push -u` (upstream)

L'opzione `-u` (o `--set-upstream`) nel comando `git push` serve per collegare il branch locale a quello remoto, creando una "traccia" tra i due. In pratica, dice a Git che il branch locale deve essere sincronizzato con il branch remoto specificato.

### Vantaggi
- Dopo aver usato `git push -u origin nome-branch`, puoi semplicemente usare `git push` o `git pull` senza dover specificare ogni volta il remote e il branch.
- Il branch locale "sa" qual è il suo upstream, cioè il branch remoto di riferimento.

### Esempio
```
git push -u origin master
```
Questo comando:
- Carica il branch locale `master` su GitHub (remote `origin`, branch `master`)
- Imposta l'upstream: da ora in poi, puoi usare solo `git push` o `git pull` su quel branch

### Note
- È consigliato usare `-u` la prima volta che si fa push di un branch nuovo
- Puoi anche collegare branch con nomi diversi, ma di solito si preferisce mantenere lo stesso nome

In sintesi, `git push -u` semplifica il lavoro quotidiano con Git, rendendo più facile sincronizzare branch locali e remoti.

## Workflow alternativo: clonare prima da GitHub

Un altro modo per iniziare a lavorare con GitHub è creare prima un repository vuoto su GitHub e poi clonarlo sul tuo computer.

### Passaggi principali
1. Crea un nuovo repository su GitHub (puoi scegliere se renderlo pubblico o privato).
2. Copia l’URL del repository.
3. Dal terminale, vai nella cartella dove vuoi lavorare e esegui:
	```
	git clone URL-del-repository
	```
4. Entra nella nuova cartella creata e inizia a lavorare normalmente con Git.

Il remote `origin` sarà già configurato automaticamente.

Da qui in poi, il workflow è identico:
- Fai modifiche
- `git add` per aggiungere i file
- `git commit` per salvare le modifiche
- `git push` per caricare tutto su GitHub

Questo approccio è utile se vuoi partire da zero e avere subito il collegamento tra il tuo repository locale e quello remoto su GitHub.

## Main & Master: branch di default su GitHub

Dal 2020, GitHub ha deciso di usare `main` come nome di default per il branch principale, invece di `master`. Nei repository nuovi, se aggiungi un file iniziale (come un README), il branch creato sarà `main`.

### Cosa cambia?
- Nei progetti nuovi su GitHub, il branch principale sarà `main`.
- Nei progetti esistenti, potresti trovare ancora `master` come branch principale.
- Puoi rinominare il branch principale da `master` a `main` con:
	```
	git branch -M main
	git push origin main
	```
- Su GitHub puoi anche impostare quale branch è il default dalle impostazioni del repository.

### Da ricordare
- `main` e `master` sono solo nomi: il funzionamento non cambia.
- Sempre più progetti usano `main`, ma `master` è ancora molto comune.
- Se cambi il nome del branch, ricordati di aggiornare anche il default su GitHub se necessario.

In sintesi, non c’è differenza tecnica tra `main` e `master`: sono solo convenzioni. Scegli quella che preferisci o che è richiesta dal tuo team/progetto.


