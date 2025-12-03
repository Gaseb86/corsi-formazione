# 🧹 **Sezione 16: Pulire la storia con Interactive Rebase**

---

## 🎯 Introduzione all'Interactive Rebase

Abbiamo visto come usare `git rebase` per combinare branch in modo lineare. Ora vedremo il secondo uso del rebase: **pulire e riscrivere la storia dei commit**.

### ❓ Cosa puoi fare con l'Interactive Rebase?

- ✏️ **Modificare messaggi di commit**
- 🔄 **Cambiare il contenuto di un commit**
- 🗑️ **Eliminare commit interi**
- 📋 **Riordinare commit**
- 🔗 **Combinare più commit in uno solo**

> 💡 **Ricorda:** Come sempre, usa il rebase solo su commit che **non hai ancora condiviso** con altri!

---

## 🔀 Due modi di usare `git rebase`

1. **Come alternativa al merge:** Per combinare branch in modo lineare (visto nella sezione precedente)
2. **Come strumento di pulizia:** Per riscrivere, riorganizzare e pulire la storia dei commit

### 📝 Quando usare Interactive Rebase?

Hai lavorato su un branch per settimane e hai fatto tanti commit:
- Alcuni sono incompleti o "a metà"
- Altri hanno messaggi poco chiari
- Alcuni sono bugfix temporanei che vorresti nascondere

Prima di condividere il branch con il team o fare una Pull Request, puoi usare l'Interactive Rebase per **pulire la storia** e renderla più professionale!

---

## 🛠️ Sintassi base di Interactive Rebase

```bash
git rebase -i HEAD~4
```

- `-i` = **interactive** (modalità interattiva)
- `HEAD~4` = **vai indietro di 4 commit** dalla posizione attuale

Questo comando apre un editor dove puoi scegliere cosa fare con ogni commit: modificare, eliminare, riordinare, combinare, ecc.

> ⚠️ **Nota:** Non stai cambiando branch! Stai solo riscrivendo la storia del branch su cui ti trovi.

### 🔎 Come funziona

Invece di creare semplicemente nuovi commit identici agli originali, l'Interactive Rebase ti permette di **intervenire** su ogni commit:
- **Cambia il messaggio**
- **Elimina il commit**
- **Combina più commit insieme**
- **Riordina i commit**

---


---

## ✏️ Modificare un messaggio di commit con Interactive Rebase

Vediamo come usare `git rebase -i` per rinominare (reword) un messaggio di commit e pulire la storia prima di condividere il branch.

### 1️⃣ Scenario tipico

Hai una serie di commit, alcuni con messaggi poco chiari o non conformi alle regole del progetto:

- `initial commit`
- `I added project files` (messaggio in passato, non conforme)
- altri commit...

### 2️⃣ Avvia l'Interactive Rebase

Supponiamo di voler rinominare il secondo commit:

```bash
git rebase -i HEAD~9
# (vai indietro di 9 commit, modifica la lista secondo necessità)
```

Si apre l'editor con la lista dei commit:

```
pick 1234567 I added project files
pick ...
```

Sostituisci `pick` con `reword` sul commit che vuoi rinominare:

```
reword 1234567 I added project files
pick ...
```

Salva e chiudi l'editor. Si aprirà una nuova finestra per modificare il messaggio:

```
add project files
```

Salva e chiudi. Git ricostruirà la storia con il nuovo messaggio.

### 3️⃣ Risultato

- Il commit selezionato ha ora un messaggio chiaro e conforme
- Tutti i commit successivi sono stati riscritti (nuovi hash)
- La storia è più pulita e professionale

> 💡 **Nota:** Cambiare un commit modifica anche tutti i commit successivi (nuovi hash), ma il contenuto rimane invariato.

---

Supponiamo che tu abbia fatto questi 4 commit sul tuo branch:
1. `add navbar`
2. `fix typo`
3. `add footer`
4. `fix navbar bug`

Con `git rebase -i HEAD~4` puoi:
- Combinare "add navbar" e "fix navbar bug" in un unico commit
- Eliminare "fix typo" se era un errore stupido
- Rinominare i messaggi per renderli più chiari

Risultato: una storia pulita e professionale!

> 💡 **Consiglio:** Usa Interactive Rebase prima di condividere il tuo lavoro, così il team vede solo una cronologia chiara e ordinata.

---

---

## 🔗 Unire e "smushare" commit con Interactive Rebase (fixup & squash)

Spesso capita di fare più commit per una stessa modifica (es: aggiunta di Bootstrap CSS e poi JS, o correzioni di typo ripetute). Prima di condividere il branch, puoi **unire** questi commit per una storia più pulita.

### 1️⃣ Fixup: unire commit eliminando il messaggio

Supponiamo di avere:
- `add bootstrap` (aggiunta CSS)
- `whoops forgot to add bootstrap js script` (aggiunta JS)

Vogliamo che entrambi siano un unico commit, con il messaggio del primo.

```bash
git rebase -i HEAD~8
# Sostituisci 'pick' con 'fixup' sul commit da unire
```

Esempio nell'editor:
```
pick abc123 add bootstrap
fixup def456 whoops forgot to add bootstrap js script
pick ...
```
Salva e chiudi. Il secondo commit verrà "smushato" nel primo, il suo messaggio sparirà, ma il contenuto sarà incluso.

### 2️⃣ Squash: unire commit mantenendo entrambi i messaggi

Se invece vuoi unire due commit e mantenere i messaggi, usa `squash`:
```
pick abc123 add top navbar
squash def456 fix navbar typos
pick ghi789 fix another navbar typo
```
Git ti chiederà di scegliere il messaggio finale.

### 3️⃣ Unire più commit ripetuti

Puoi usare più `fixup` di seguito per "smushare" tanti commit in uno solo:
```
pick abc123 add top navbar
fixup def456 fix navbar typos
fixup ghi789 fix another navbar typo
```
Risultato: un solo commit con tutte le correzioni!

### 4️⃣ Risultato

- La storia è più pulita e leggibile
- Tutte le modifiche sono incluse, ma i commit intermedi sono spariti
- Puoi rinominare il commit finale con `reword` se vuoi

> 💡 **Nota:** I cambiamenti non vengono persi, sono solo "fusi" in un unico commit!

---


---

## 🗑️ Eliminare un commit con Interactive Rebase (drop)

A volte capita di fare un commit che vuoi **rimuovere completamente** (non solo il messaggio, ma anche le modifiche). Ecco come fare:

### 1️⃣ Individua il commit da eliminare

Supponiamo di avere un commit con messaggio "my cat made this commit" che aggiunge del codice inutile.

### 2️⃣ Avvia l'Interactive Rebase

Vai indietro di 2 commit (o quanto serve):
```bash
git rebase -i HEAD~2
```
Nell'editor vedrai:
```
pick abc123 my cat made this commit
pick def456 altro commit
```
Sostituisci `pick` con `drop` sul commit da eliminare:
```
drop abc123 my cat made this commit
pick def456 altro commit
```
Salva e chiudi.

### 3️⃣ Risultato

- Il commit selezionato è stato **rimosso** dalla storia
- Le modifiche introdotte da quel commit sono sparite
- La storia è più pulita e coerente

> 💡 **Nota:** Puoi usare `drop` su qualsiasi commit che vuoi eliminare, ma attenzione: le modifiche spariranno!

---