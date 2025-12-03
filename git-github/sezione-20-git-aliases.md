# Sezione 20: Writing Custom Git Aliases


## 🗂️ Il file di configurazione globale di Git

Prima di parlare degli alias, è importante capire dove e come Git salva le sue configurazioni.
Git gestisce le impostazioni su tre livelli:

- **Config locale**: in `.git/config` dentro ogni repository. Vale solo per quel repo.
- **Config globale**: in `~/.gitconfig` (nella home dell’utente). Vale per tutti i repo dell’utente.
- **Config di sistema**: in `/etc/gitconfig` (o simile). Vale per tutti gli utenti della macchina.

Nella pratica, quasi sempre si usano i primi due livelli.

### 📄 Dove si trova il file globale?
- Il file globale si chiama `.gitconfig` e si trova nella home directory dell’utente (`~/.gitconfig` su Linux/Mac, `C:\Users\tuo_utente\.gitconfig` su Windows).
- È un file di testo leggibile e modificabile anche manualmente.

### ⚙️ Modificare le impostazioni globali
Puoi modificare le impostazioni globali in due modi:
- **Da terminale**:
  ```bash
  git config --global user.name "Tuo Nome"
  git config --global user.email "tuo@email.com"
  ```
- **Modificando direttamente il file**:
  Apri `~/.gitconfig` con un editor di testo e cambia i valori desiderati.

### 📝 Esempio di file `.gitconfig`
```ini
[user]
    name = Tuo Nome
    email = tuo@email.com
[core]
    editor = code --wait
```

### ℹ️ Note sulla sintassi
- Le sezioni sono tra parentesi quadre (`[user]`, `[core]`, ecc.)
- Le proprietà sono scritte come `chiave = valore` e possono essere indentate (consigliato per chiarezza)
- Modifiche fatte da terminale aggiornano automaticamente il file `.gitconfig`

### 🎯 Quando usare la config globale?
- Per impostazioni che vuoi valide in tutti i tuoi repository (nome, email, editor, alias, ecc.)
- Se vuoi configurazioni diverse per un singolo repo, usa invece il file locale `.git/config`

Nel prossimo paragrafo vedremo come aggiungere alias utili direttamente nel file globale.


---

## ✨ Scrivere il primo alias Git

Un alias Git è un comando personalizzato, una scorciatoia che ti permette di risparmiare tempo e digitazioni. Puoi creare alias per comandi che usi spesso (es: `git status` → `git s`) o per comandi complessi con molte opzioni.

### 📝 Come si crea un alias?
Gli alias si configurano nella sezione `[alias]` del file `.gitconfig` globale (o locale). La sintassi è:

```ini
[alias]
    s = status
    l = log
    co = checkout
```

Dopo aver salvato, puoi usare i nuovi comandi:
```bash
git s      # equivale a git status
git l      # equivale a git log
git co     # equivale a git checkout
```

Puoi chiamare l’alias come vuoi (es: `st`, `stat`, `statpat`), basta che sia un nome valido.

### ⚡ Esempio pratico
1. Apri il file `~/.gitconfig` e aggiungi:
   ```ini
   [alias]
       s = status
       l = log
   ```
2. Salva il file.
3. Ora puoi usare:
   ```bash
   git s
   git l
   ```

### ℹ️ Note
- Gli alias sono solo scorciatoie: `git s` esegue `git status`.
- Se cambi il nome dell’alias, cambia anche il comando (es: `statpat = status` → `git statpat`).
- Se provi a usare un alias non definito, Git mostrerà un errore.

---

## 🖥️ Creare alias dal terminale

Oltre a modificare il file `.gitconfig`, puoi creare alias direttamente dal terminale usando il comando `git config --global`.

### 📝 Sintassi
```bash
git config --global alias.<nome-alias> "<comando>"
```

### ⚡ Esempio pratico
Per creare un alias chiamato `showmebranches` che esegue `git branch`:
```bash
git config --global alias.showmebranches "branch"
```
Ora puoi usare:
```bash
git showmebranches
```
che equivale a `git branch`.

Puoi verificare che l’alias sia stato aggiunto aprendo il file `~/.gitconfig`:
```ini
[alias]
    showmebranches = branch
```

### ℹ️ Note
- Gli alias creati con `--global` sono disponibili in tutti i tuoi repository.
- Se usi `--local` (senza `--global`), l’alias sarà valido solo nel repository corrente.
- Puoi eliminare un alias rimuovendolo dal file `.gitconfig` o usando:
  ```bash
  git config --global --unset alias.showmebranches
  ```

Nel prossimo paragrafo vedremo come creare alias che accettano argomenti.


---

## 🏷️ Alias con argomenti

Gli alias di Git possono accettare argomenti: tutto ciò che scrivi dopo l’alias viene passato al comando originale.

### 📝 Esempi pratici
- Alias per `git commit -m`:
  ```ini
  [alias]
      cm = commit -m
  ```
  Ora puoi scrivere:
  ```bash
  git cm "Messaggio di commit"
  # equivale a: git commit -m "Messaggio di commit"
  ```

- Alias per `git add`:
  ```ini
  [alias]
      a = add
  ```
  Puoi aggiungere uno o più file:
  ```bash
  git a file1.txt file2.js
  # equivale a: git add file1.txt file2.js
  ```

### ℹ️ Note
- Gli argomenti vengono passati automaticamente: non serve nessuna sintassi speciale.
- Puoi usare gli alias anche con più argomenti (es: file multipli, messaggi, opzioni, ecc.).
- Questo vale per la maggior parte dei comandi semplici.

> 💡 **Consiglio:** Usa alias brevi per i comandi che usi più spesso e che richiedono argomenti, come `add`, `commit -m`, `checkout`, ecc.

Nel prossimo paragrafo vedremo alcuni alias avanzati e utili condivisi dalla community.

---

## 🌐 Alias avanzati e utili dalla community

Oltre agli alias semplici, online trovi raccolte di alias avanzati che migliorano la produttività e aggiungono funzionalità. Ecco alcuni tra i più popolari:

### 🖥️ Alias per log colorato e compatto
```ini
[alias]
    ls = log --color --graph --pretty=format:'%C(yellow)%h%Creset - %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
```
Usa `git ls` per vedere la storia in modo leggibile e colorato.

### 🗂️ Alias per vedere file modificati nei commit
```ini
[alias]
    ll = log --name-status --oneline
```
Usa `git ll` per vedere i file cambiati in ogni commit.

### 🔧 Come modificare un alias già esistente
Puoi cambiare un alias in due modi:
- **Dal terminale:**
  ```bash
  git config --global alias.ll "log --name-status --oneline"
  ```
  (Sostituisci il comando con quello che preferisci)
- **Modificando il file `.gitconfig`:**
  Apri `~/.gitconfig` e cambia la riga corrispondente sotto `[alias]`.

Dopo aver salvato, il nuovo alias sarà subito attivo!

### 🏷️ Alias per rinominare branch (shell script)
```ini
[alias]
    done = !git branch | grep -v "\*" | xargs -I {} git branch -m {} done-{}
```
L’esclamativo `!` indica che l’alias esegue un comando di shell, non solo Git.

### 📋 Alias per elencare tutti gli alias definiti
```ini
[alias]
    la = !git config --get-regexp ^alias\.
```
Usa `git la` per vedere la lista di tutti gli alias configurati.

### ℹ️ Note e avvertenze
- Gli alias con `!` permettono di usare comandi di shell (es: grep, echo, xargs).
- Puoi trovare raccolte di alias su blog, forum, GitHub (es: il repo "git-alias").
- Attenzione: gli alias sono personali! Se lavori su altri computer, potrebbero non essere disponibili.
- Impara sempre i comandi originali prima di affidarti agli alias.

> 💡 **Risorsa utile:** Cerca su GitHub "git-alias" per una raccolta completa e documentata di alias avanzati.

Con questo hai una panoramica completa sugli alias Git: come crearli, usarli e trovare quelli più utili online!

