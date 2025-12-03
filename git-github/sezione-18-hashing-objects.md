# 🛠️ **Sezione 18: Git dietro le quinte – Hashing & Oggetti**

---

## 📁 Il file di configurazione locale: .git/config

Ogni repository Git contiene una cartella nascosta `.git` con molti file e directory.
Uno dei più importanti è il file `config`, che gestisce le **impostazioni locali** del repository.

### 🔍 Dove si trova?
- Percorso: `.git/config` (dentro la cartella del repo)
- Contiene solo le configurazioni **locali** (valide solo per quel repo)

### 🛠️ Modificare le impostazioni locali
Puoi modificare le impostazioni con il comando:
```bash
git config --local user.name "Chicken Little"
git config --local user.email "chicken@gmail.com"
# Imposta nome e email solo per questo repository
```
Oppure puoi modificare direttamente il file `.git/config`.

### 🎨 Personalizzare i colori dell'output
Puoi cambiare i colori di vari comandi Git (branch, diff, status) direttamente nel file `config`:
```ini
[color]
	ui = true
[color "branch"]
	current = yellow bold
	local = cyan bold
[color "diff"]
	old = magenta bold
	new = green
```
Effetto: i branch e le differenze avranno colori personalizzati nell'output del terminale.

### 🧑‍💻 Esempio pratico
1. Apri `.git/config` e aggiungi:
   ```ini
   [color]
	   ui = true
   [color "branch"]
	   current = yellow bold
	   local = cyan bold
   ```
2. Salva e prova:
   ```bash
   git branch
   # Vedrai i branch colorati secondo la configurazione
   ```

### ℹ️ Altre impostazioni utili
- Puoi aggiungere alias, cambiare editor, ignorare maiuscole/minuscole, ecc.
- La documentazione ufficiale è molto ampia, ma puoi trovare esempi online.

> 💡 **Consiglio:** Usa il file locale per personalizzazioni specifiche di progetto. Per impostazioni globali, usa il file di config globale (`~/.gitconfig`).

---

## 📂 Dentro Git: la cartella refs

Un altro elemento fondamentale della cartella `.git` è la directory `refs`, che contiene tutti i **riferimenti** (puntatori) di Git: branch, tag e remoti.

### 📁 Struttura della cartella refs
- `.git/refs/heads/` → Un file per ogni branch locale, il nome del file è il nome del branch, il contenuto è l'hash del commit più recente (tip).
- `.git/refs/tags/` → Un file per ogni tag, il nome del file è il nome del tag, il contenuto è l'hash del commit taggato.
- `.git/refs/remotes/` → Un file per ogni branch remoto tracciato, organizzato per nome del remoto (es. origin/master).

### 🧑‍💻 Esempio pratico
Supponiamo di avere questi branch:
```bash
git branch
# master
# new-branch
# chicken
```
Dentro `.git/refs/heads/` troverai:
- master
- new-branch
- chicken
Ognuno contiene l'hash del commit più recente del branch corrispondente.

Se crei un nuovo branch:
```bash
git switch -c chicken
# Verrà creato il file .git/refs/heads/chicken
```

Per i tag:
```bash
git tag v1.0.0
# Verrà creato il file .git/refs/tags/v1.0.0 con l'hash del commit
```

Per i remoti:
Quando fai `git fetch` o `git pull`, Git aggiorna i file in `.git/refs/remotes/` per tenere traccia dei branch remoti.

### 🔎 Perché è importante?
- I file in `refs` sono i "puntatori" che Git usa per sapere dove si trovano branch e tag.
- Quando vedi un diagramma con frecce e etichette, in realtà sono file in questa cartella.
- Modificare questi file manualmente è sconsigliato, ma puoi esplorarli per capire meglio la struttura interna di Git.

---

---

## 📄 Dentro Git: il file HEAD

Il file `HEAD` (tutto maiuscolo) si trova nella cartella `.git` e rappresenta il **puntatore attuale** del repository:
- Di solito punta a un branch (es. `refs/heads/master`)
- Può puntare direttamente a un commit (modalità "detached HEAD")

### 🔍 Cosa contiene HEAD?
- Se sei su un branch: `ref: refs/heads/nome-branch`
- Se sei in detached HEAD: l'hash di un commit

### 🧑‍💻 Esempio pratico
1. Sei su master:
	- `.git/HEAD` contiene `ref: refs/heads/master`
2. Passi a un altro branch:
	- `.git/HEAD` contiene `ref: refs/heads/chicken`
3. Fai checkout di un commit:
	- `.git/HEAD` contiene direttamente l'hash del commit (detached HEAD)

```bash
git switch chicken
# HEAD ora punta a refs/heads/chicken
cat .git/HEAD
# ref: refs/heads/chicken

git checkout 5fb123
# HEAD ora punta direttamente al commit 5fb123 (detached HEAD)
cat .git/HEAD
# 5fb123...
```

### ℹ️ Perché è importante?
- HEAD indica sempre "dove sei" nel repository
- In modalità detached HEAD puoi esplorare la storia senza muovere i branch
- Quando committi, HEAD determina dove verrà aggiunto il nuovo commit

---
---

## 📦 Dentro Git: la cartella objects

La cartella `.git/objects` è il **cuore di Git**: qui vengono salvati tutti i dati, la storia, i file e i commit del repository.

### 📁 Struttura della cartella objects
- Contiene molte sottocartelle con nomi esadecimali (es. `a3`, `f7`, ...)
- Ogni sottocartella contiene file binari compressi
- Questi file non sono leggibili direttamente: sono ottimizzati per spazio e velocità

### 🔑 Cosa contiene?
Git salva **oggetti** di 4 tipi principali:
1. **Blob**: il contenuto dei file
2. **Tree**: la struttura delle cartelle e file
3. **Commit**: la storia delle modifiche
4. **Tag annotati**: etichette ufficiali con metadati

Tutti questi oggetti sono identificati da un **hash** (SHA-1), che hai già visto come "commit hash".

### 🧑‍💻 Esempio pratico
Se esplori `.git/objects`, troverai:
- Sottocartelle con due lettere (es. `a3/`, `f7/`)
- Dentro, file binari che rappresentano oggetti Git

> ℹ️ **Nota:** Non puoi leggere direttamente questi file, ma sono fondamentali per la storia e la sicurezza di Git.

### 🗂️ Come funziona?
- Git **non** salva solo le differenze tra i file (diff), ma salva **istantanee complete** (snapshot) dello stato del progetto ad ogni commit.
- Questo rende Git molto veloce e affidabile.

### 🚩 Cosa vedremo dopo?
Nei prossimi paragrafi vedrai come funziona l'hashing, e come sono fatti i vari oggetti (blob, tree, commit, tag).

---

## 🔢 Crash Course sulle funzioni di hashing

Per capire come Git salva e identifica i dati, serve una breve introduzione alle **funzioni di hashing**.

### 🧩 Cos'è un hash?
Un **hash** è una stringa (di solito esadecimale) di lunghezza fissa, generata da una funzione che prende in input dati di qualsiasi dimensione.

Esempio:
- Input: "I love chickens" → Output: `27d54...` (40 caratteri)
- Input: "LOL" → Output: `7cf...` (40 caratteri)

### 🔒 Proprietà delle funzioni di hashing crittografiche
1. **Deterministica**: stesso input → stesso output
2. **One-way**: dall'output non si può risalire all'input
3. **Sensibile alle modifiche**: piccole variazioni nell'input producono output completamente diversi
4. **Evitare collisioni**: è molto improbabile che due input diversi producano lo stesso output

### 🛡️ Hashing in sicurezza e Git
Le funzioni di hashing sono usate in sicurezza (password, firme digitali, criptovalute) e in Git per identificare in modo univoco file, commit e oggetti.

### 🏷️ SHA-1: l'algoritmo usato da Git
- Git usa l'algoritmo **SHA-1** per generare hash di 40 caratteri esadecimali
- Ogni commit, file, oggetto in Git ha un hash SHA-1
- In futuro Git potrebbe cambiare algoritmo, ma il principio resta lo stesso

### 🧑‍💻 Esempio pratico
Prova a generare hash SHA-1 online:
- Input: `H` → Output: `...27d54...`
- Input: `HE` → Output: `...7cf...` (completamente diverso)
- Input: testo lunghissimo → Output: sempre 40 caratteri

> ℹ️ **Nota:** Non serve conoscere i dettagli matematici di SHA-1, basta sapere che ogni oggetto in Git è identificato in modo univoco dal suo hash.

---

---


---

## 🗝️ Git come Key-Value Store

Git è fondamentalmente un **key-value data store**: ogni volta che salvi qualcosa (file, commit, struttura, tag), Git genera una **chiave unica** (hash SHA-1) che ti permette di recuperare quel contenuto in futuro.

### 🔑 Come funziona?
- Salvi un file, una cartella, un commit, un tag → Git calcola un hash SHA-1
- L'hash diventa la "chiave" per quel contenuto
- Puoi chiedere a Git di recuperare il contenuto usando la chiave

> 💡 **Analogia:** Come il coat check di un locale: lasci il cappotto, ricevi una chiave, e puoi ritirarlo solo con quella chiave.

### 🧑‍💻 Esempio pratico
Supponiamo di avere due versioni di un file `App.js`:
- Ogni versione viene salvata con un hash diverso
- Puoi chiedere a Git di mostrarti il contenuto associato a un hash

```bash
git show <hash>
# Mostra il contenuto associato a quell'hash
```

### 🗂️ Hash ovunque
- Gli hash SHA-1 non servono solo per i commit, ma anche per file (blob), strutture (tree), tag, ecc.
- Tutto in Git è identificato e recuperato tramite hash

### 📦 Riassunto
- Git memorizza dati e ti restituisce una chiave (hash)
- Puoi recuperare i dati usando la chiave
- Questo rende Git veloce, sicuro e affidabile

Nei prossimi paragrafi vedrai come Git usa questi hash per gestire blob, tree, commit e tag.

---

## 🧪 Hashing manuale con git hash-object

Il comando `git hash-object` permette di vedere come Git genera e gestisce gli hash SHA-1 per qualsiasi contenuto.

### 🔍 Come funziona?
- `git hash-object <file>`: calcola l'hash SHA-1 del contenuto del file, ma **non lo salva** nel database di Git
- `echo "testo" | git hash-object --stdin`: calcola l'hash di un testo passato da terminale
- `git hash-object -w <file>` o `echo "testo" | git hash-object -w --stdin`: calcola l'hash **e lo salva** nella cartella `.git/objects`

### 🧑‍💻 Esempio pratico
```bash
echo "hello" | git hash-object --stdin
# Restituisce l'hash SHA-1 di "hello" (non lo salva)

echo "hello" | git hash-object -w --stdin
# Restituisce l'hash e lo salva in .git/objects
# Verrà creata una sottocartella (prime 2 cifre dell'hash) e un file (le restanti 38 cifre)
```
Se ripeti il comando con lo stesso input, ottieni sempre lo stesso hash (deterministico).

### 📦 Dove viene salvato?
- `.git/objects/ce/0136...` → contiene la versione compressa e binaria di "hello"
- `.git/objects/dd/7e1...` → contiene la versione compressa e binaria di "goodbye"

### ℹ️ Note
- Questi file sono **blob**: la forma più semplice di oggetto Git
- Di solito non usi mai `git hash-object` manualmente, ma è utile per capire come Git salva i dati

Nel prossimo paragrafo vedrai come recuperare questi dati con git cat-file.

---

## 📤 Recuperare dati con git cat-file

Il comando `git cat-file` permette di **leggere il contenuto** di un oggetto Git (blob, commit, tree, tag) a partire dal suo hash.

### 🛠️ Come funziona?
- `git cat-file -p <hash>`: mostra il contenuto "prettificato" dell'oggetto associato all'hash
- Puoi usare hash di blob, commit, tree, tag

### 🧑‍💻 Esempio pratico
Supponiamo di aver salvato due versioni di `dogs.txt`:
```bash
git hash-object -w dogs.txt
# Ottieni un hash, es: 39e275...
git cat-file -p 39e275...
# Mostra la prima versione: "Rusty\nWyatt"

# Modifica il file, aggiungi "Cheyenne"
git hash-object -w dogs.txt
# Ottieni un nuovo hash, es: fd915...
git cat-file -p fd915...
# Mostra la seconda versione: "Rusty\nWyatt\nCheyenne"
```
Puoi anche ripristinare una versione:
```bash
git cat-file -p fd915... > dogs.txt
# Ripristina la versione corrispondente all'hash
```

### ℹ️ Note
- Puoi recuperare qualsiasi oggetto Git se hai il suo hash
- Non serve aver fatto commit: basta aver salvato il blob con hash-object -w
- Puoi cancellare il file originale, Git conserva la versione finché la cartella .git esiste

Nel prossimo paragrafo vedrai cosa sono i blob e come funzionano.

---

## 🧱 Deep Dive: Git Object – Blob

Un **blob** (Binary Large Object) è il tipo di oggetto Git che contiene il **contenuto di un file**.

### 🔍 Caratteristiche dei blob
- Un blob è solo il contenuto del file (non il nome)
- Ogni blob ha un hash SHA-1 unico
- Più versioni di uno stesso file generano blob diversi
- I blob sono la base di tutto: ogni file, ogni versione, ogni modifica crea un nuovo blob

### 🧑‍💻 Esempio pratico
Abbiamo creato blob con:
```bash
echo "hello" | git hash-object -w --stdin
echo "goodbye" | git hash-object -w --stdin
git hash-object -w dogs.txt
# Ogni comando genera un blob e un hash
```
Puoi recuperare il contenuto con:
```bash
git cat-file -p <hash-del-blob>
# Mostra il contenuto del blob
```

### 🗂️ Visualizzazione
Un blob è solo il contenuto:
```
// Contenuto di un file
function hello() {
	return "Hello!";
}
```
Il nome del file non è incluso nel blob!

### ℹ️ Differenza con commit
- Un commit è un oggetto più complesso che collega blob, tree e metadati
- Un blob è solo il contenuto, senza informazioni su nome, struttura o storia

> 💡 **Nota:** I blob sono i mattoni fondamentali di Git. Ogni file, ogni versione, ogni modifica crea un nuovo blob.

Nel prossimo paragrafo vedrai cosa sono i tree e come collegano i blob ai nomi dei file e alle cartelle.

---

## 🌳 Deep Dive: Git Object – Tree

Un **tree** è il tipo di oggetto Git che rappresenta la **struttura di una directory**: collega i blob (contenuti dei file) ai nomi dei file e alle cartelle.

### 🔍 Caratteristiche dei tree
- Un tree contiene riferimenti (hash) a blob e ad altri tree
- Ogni entry ha: tipo (blob/tree), hash, nome (file o cartella)
- I tree permettono a Git di ricostruire la struttura di directory e file
- Ogni tree ha un hash SHA-1 unico

### 🧑‍💻 Esempio pratico
Supponiamo di avere questa struttura:
```
project/
├── index.html
├── main.js
└── styles/
	├── app.css
	└── nav.css
```
Git crea:
- Un tree per la root (project)
- Un tree per styles/
- Blob per ogni file
Il tree root collega i blob (index.html, main.js) e il tree styles.

### 🗂️ Visualizzazione
Un tree contiene:
- Tipo: blob/tree
- Hash: hash del blob/tree
- Nome: nome del file o cartella

Esempio:
```
tree 98287
|-- blob 1F7A7  index.html
|-- blob BE321  main.js
|-- tree 98287  styles
	|-- blob 10ABB app.css
	|-- blob FFE77 nav.css
```

### 🛠️ Visualizzare un tree con git cat-file
```bash
git cat-file -p <hash-del-tree>
# Mostra la struttura del tree
git cat-file -T <hash>
# Mostra il tipo dell'oggetto (tree, blob, commit, tag)
```
Puoi anche visualizzare il tree di un commit:
```bash
git cat-file -p master^{tree}
# Mostra la struttura della directory al commit più recente su master
```

### ℹ️ Note
- I tree sono fondamentali per la gestione di progetti con molte cartelle e file
- Ogni commit in Git punta a un tree che rappresenta lo stato del progetto in quel momento

Nel prossimo paragrafo vedrai come i commit collegano tutto e rappresentano la storia del progetto.

---

## 📝 Deep Dive: Git Object – Commit

Il **commit** è l'oggetto Git che rappresenta un punto nella storia del progetto: collega la struttura (tree), i contenuti (blob) e la storia (parent).

### 🔍 Struttura di un commit
- Hash SHA-1 unico
- Riferimento al **tree** (snapshot della directory)
- Riferimento al **parent** (commit precedente, se esiste)
- Metadati: autore, committer, data, messaggio

### 🧑‍💻 Esempio pratico
Supponiamo di avere una repo con due file:
```bash
git add dogs.txt
git commit -m "Initial commit"
# Crea il primo commit
git add cats.txt
git commit -m "Add cats file"
# Crea il secondo commit
```
Ogni commit è un oggetto nella cartella `.git/objects`.
Puoi visualizzare la struttura:
```bash
git cat-file -p <hash-del-commit>
# Mostra: tree, parent, autore, messaggio
git cat-file -T <hash>
# Mostra il tipo (commit)
```
Puoi anche visualizzare il tree associato:
```bash
git cat-file -p <hash-del-tree>
# Mostra i file e le cartelle in quel commit
```

### 🔗 Collegamento tra commit
- Ogni commit (tranne il primo) punta al parent
- La catena dei commit forma la storia del progetto
- Ogni commit punta a un tree che rappresenta lo stato del progetto in quel momento

### 🗂️ Workflow interno
Quando committi:
1. Git crea un tree con lo stato attuale (index)
2. Crea un commit che punta a quel tree e al parent
3. Hash di tutto → nuovo commit
4. HEAD si sposta sul nuovo commit

### ℹ️ Note
- Cambiando un file → nuovo blob → nuovo tree → nuovo commit
- Se un file non cambia, il blob rimane lo stesso tra i commit
- I commit sono la base della storia e della collaborazione in Git

> 💡 **Nota:** Gli annotated tag sono un altro tipo di oggetto Git, usati per etichettare commit importanti (vedi sezione tag).

---

---

---

---

---

---
