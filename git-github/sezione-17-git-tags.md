# 🏷️ **Sezione 17: Git Tags – Segnare i momenti importanti nella storia**
---

## 💡 L'idea dietro i Git Tag

I **Git tag** sono uno strumento semplice ma potentissimo per "etichettare" un commit specifico nella storia del repository.
Un tag è come un segnalibro che indica un momento importante: una versione, una release, un traguardo.

### 🔖 Cos'è un tag?

- Un **tag** è un'etichetta che punta a un commit preciso
- A differenza di un branch, il tag **non si sposta**: resta sempre su quel commit
- Puoi taggare qualsiasi commit, non solo quelli su `main`

> 📌 **Esempio:**
> - Tag `v1.0.0` → indica la prima release stabile
> - Tag `v2.1.0` → nuova versione con funzionalità aggiunte

### 🛠️ A cosa servono i tag?

- Segnare versioni di rilascio (release)
- Evidenziare bugfix importanti
- Marcare traguardi nello sviluppo

> 💬 **Pensalo come un post-it digitale**: "Da qui in poi è la versione 3.1.0!"

### 🔄 Differenza tra branch e tag

| Oggetto  | Si sposta? | Descrizione |
|----------|------------|-------------|
| Branch   | ✅         | Si aggiorna con nuovi commit |
| Tag      | ❌         | Resta fisso sul commit creato |

### 📦 Tipi di tag

1. **Lightweight tag:** solo un nome, semplice e veloce
2. **Annotated tag:** include messaggio, autore, data (preferito nei progetti seri)

> ℹ️ **Nota:** Gli annotated tag sono preferiti perché includono più informazioni e sono più "ufficiali".


### 📝 Sintesi

- I tag sono usati soprattutto per marcare versioni (versioning)
- Puoi chiamarli come vuoi (`v1.0.0`, `beta`, `hotdog`, ...)
- Sono fondamentali per la gestione delle release nei progetti open source

---

## 🧮 Una nota su Semantic Versioning

La maggior parte dei tag viene usata per **versionare** i rilasci di software.
Il sistema più diffuso è **Semantic Versioning** (SemVer):

### 🔢 Cos'è Semantic Versioning?

Un sistema di numerazione delle versioni che segue la sintassi:

`MAJOR.MINOR.PATCH`

Esempio: `v2.1.3`

| Numero   | Significato                  | Quando si incrementa?                |
|----------|------------------------------|--------------------------------------|
| MAJOR    | Cambiamenti incompatibili    | Quando ci sono breaking changes      |
| MINOR    | Nuove funzionalità           | Quando aggiungi feature compatibili  |
| PATCH    | Bugfix e piccole modifiche   | Per correzioni senza nuove feature   |

### 📋 Regole principali

- La prima release pubblica è di solito `1.0.0`
- Un bugfix incrementa solo PATCH: `1.0.1`, `1.0.2`...
- Una nuova feature incrementa MINOR e resetta PATCH: `1.1.0`, `1.2.0`...
- Un cambiamento incompatibile incrementa MAJOR e resetta gli altri: `2.0.0`, `3.0.0`...

### 🛠️ Esempi reali

- **Bootstrap:** `v5.0.0`, `v4.5.2` (patch), `v4.6.0` (minor)
- **React:** `16.8.6` (patch), `16.9.0` (minor), `17.0.0` (major)

> ℹ️ **Nota:** Spesso si usa la lettera `v` davanti al numero, ma non è obbligatoria.
> Puoi aggiungere suffissi come `-beta`, `-rc` per versioni di test.


### 🎯 Perché è importante?
- Aiuta chi usa il software a capire la portata delle modifiche
- Rende la storia delle release chiara e prevedibile
- È lo standard per la maggior parte dei progetti open source

---

## 👀 Visualizzare e cercare i tag

Vediamo come **elencare** e **filtrare** i tag in un repository Git.

### 📋 Elencare tutti i tag

```bash
git tag
```
Mostra la lista di tutti i tag presenti nel repository.

### 🔎 Filtrare e cercare tag

Puoi cercare tag che corrispondono a un pattern:

```bash
git tag -l 'v17*'
```
Mostra tutti i tag che iniziano con `v17`.

```bash
git tag -l '*beta*'
```
Mostra tutti i tag che contengono la parola `beta`.

> ℹ️ **Nota:** L'opzione `-l` serve per filtrare i tag con pattern (wildcard).

### 🧑‍💻 Esempio pratico

Supponiamo di aver clonato il repository di React:
```bash
git clone https://github.com/facebook/react.git
cd react
git tag
# Elenca tutti i tag (ce ne sono centinaia!)
git tag -l 'v17*'
# Elenca solo i tag delle versioni 17
git tag -l '*beta*'
# Elenca solo i tag beta
```

> 💡 **Consiglio:** I tag sono usati soprattutto per versioni, ma puoi chiamarli come vuoi!

---


---

## 🕵️‍♂️ Confrontare e lavorare con i tag

### 🏷️ Checkout di un tag

Puoi "tornare indietro nel tempo" e lavorare su una versione specifica usando il checkout di un tag:

```bash
git checkout v15.3.1
# Oppure
git switch --detach v15.3.1
```
> ⚠️ **Nota:** Quando fai checkout di un tag, entri in "detached HEAD" (non sei su un branch).

Se vuoi continuare a lavorare su quella versione, crea un nuovo branch:
```bash
git switch -c branch_da_tag
# Ora puoi lavorare normalmente
```

### 🔀 Differenze tra tag (git diff)

Puoi confrontare due versioni/tag per vedere cosa è cambiato:

```bash
git diff v17.0.0 v17.0.1
# Mostra le differenze tra la release 17.0.0 e la patch 17.0.1

git diff v16.14.0 v17.0.0
# Mostra le differenze tra l'ultima minor di 16 e la major 17
```

> 💡 **Consiglio:** Usare i tag per confrontare versioni ti aiuta a capire cosa è cambiato tra rilasci!

---



---

## 🏷️ Creare Lightweight Tag

I **lightweight tag** sono il modo più semplice per creare un tag: è solo un nome che punta a un commit.

### 🛠️ Come si crea un lightweight tag?

```bash
git tag v17.0.2
# Crea il tag v17.0.2 sull'ultimo commit (HEAD)
```
Puoi creare un tag su un commit specifico:
```bash
git tag v17.0.3 <commit-hash>
# Crea il tag v17.0.3 su un commit specifico
```

### 🧑‍💻 Esempio pratico

Supponiamo di aver fatto una modifica e un commit:
```bash
git add README.md
git commit -m "Fix typo in README"
git tag v17.0.2
# Ora il tag v17.0.2 punta a questo commit
```
Fai un'altra modifica:
```bash
git add README.md
git commit -m "Update README"
git tag v17.0.3
# Ora il tag v17.0.3 punta al nuovo commit
```
Puoi vedere tutti i tag:
```bash
git tag
# Elenca tutti i tag
```
E confrontare le differenze tra due tag:
```bash
git diff v17.0.2 v17.0.3
# Mostra cosa è cambiato tra le due versioni
```

> ℹ️ **Nota:** I lightweight tag sono semplici, ma spesso si preferiscono gli annotated tag per le release ufficiali.

---


---

## 🏷️ Creare Annotated Tag

Gli **annotated tag** sono tag "ufficiali" che includono:
- Nome del tag
- Autore e data
- Messaggio descrittivo

### 🛠️ Come si crea un annotated tag?

Usa l'opzione `-a` per creare un annotated tag:
```bash
git tag -a v17.1.0
# Crea il tag v17.1.0 sull'ultimo commit (HEAD) e apre l'editor per il messaggio
```
Puoi aggiungere direttamente il messaggio con `-m`:
```bash
git tag -a v17.1.0 -m "Aggiunta nuova feature minor release"
# Crea il tag v17.1.0 con messaggio inline
```

### 🧑‍💻 Esempio pratico

Supponiamo di aver aggiunto una nuova funzionalità:
```bash
echo "// Nuova feature" > feature.js
git add feature.js
git commit -m "Add new feature"
git tag -a v17.1.0 -m "Nuova minor release: aggiunta feature"
# Ora il tag v17.1.0 è annotato con messaggio e metadati
```

### 👀 Visualizzare i dettagli di un tag annotato

Per vedere tutte le informazioni di un tag annotato:
```bash
git show v17.1.0
# Mostra autore, data, messaggio e commit associato
```
Puoi usarlo anche su tag di altri progetti:
```bash
git show v17.0.0
# Mostra i dettagli del tag v17.0.0
```

> ℹ️ **Nota:** Gli annotated tag sono preferiti per le release ufficiali perché includono più informazioni e sono riconosciuti da GitHub per le release.

---

## 🏷️ Taggare un commit precedente

Finora abbiamo creato tag sull'ultimo commit (HEAD), ma puoi aggiungere un tag anche su **commits passati** usando il loro hash.

### 🛠️ Come si tagga un commit precedente?

1. Trova l'hash del commit con:
	```bash
	git log --oneline
	# Copia l'hash del commit che vuoi taggare
	```
2. Crea il tag (lightweight o annotated):
	```bash
	git tag mytag <commit-hash>
	# Crea un lightweight tag su quel commit

	git tag -a v17.2.0 <commit-hash> -m "Release su commit precedente"
	# Crea un annotated tag su quel commit
	```

### 🧑‍💻 Esempio pratico

Supponiamo di voler taggare un commit vecchio:
```bash
git log --oneline
# ...trova l'hash, ad esempio: 1a2b3c4
git tag mytag 1a2b3c4
# Ora il tag 'mytag' punta a quel commit
git tag
# Vedrai 'mytag' nella lista dei tag
```

> ℹ️ **Nota:** Puoi usare questa tecnica per marcare versioni storiche, bugfix o traguardi anche dopo che sono stati creati.

---

## 🏷️ Spostare (forzare) un tag esistente

Di solito i tag sono **immutabili**: una volta creati, puntano sempre allo stesso commit. Ma se hai fatto un errore, puoi spostare un tag su un altro commit usando l'opzione `-f` (**force**).

### 🛠️ Come si forza un tag?

Supponiamo che il tag `v17.0.3` punti al commit sbagliato. Per spostarlo:
```bash
git tag -f v17.0.3 <nuovo-commit-hash>
# Sposta il tag v17.0.3 sul nuovo commit
```
Se provi a creare un tag con lo stesso nome senza `-f`, Git ti darà errore:
```bash
git tag v17.0.3 <commit-hash>
# Errore: il tag esiste già!
```

### 🧑‍💻 Esempio pratico

```bash
git log --oneline
# Trova il nuovo commit su cui vuoi spostare il tag
git tag -f v17.0.3 1a2b3c4
# Ora il tag v17.0.3 punta al commit 1a2b3c4
git log --oneline --decorate
# Verifica che il tag sia stato aggiornato
```

> ⚠️ **Attenzione:** Spostare i tag è sconsigliato se il tag è già stato condiviso (pushato) con altri, perché può creare confusione!

---

## 🏷️ Eliminare un tag

Per eliminare un tag locale, usa l'opzione `-d`:

### 🛠️ Come si elimina un tag?

```bash
git tag -d deleteme
# Elimina il tag 'deleteme' dal repository locale
```

### 🧑‍💻 Esempio pratico

Supponiamo di aver creato un tag:
```bash
git tag deleteme
git tag
# Vedrai 'deleteme' tra i tag
git tag -d deleteme
# Ora il tag è stato eliminato
git tag
# Non vedrai più 'deleteme'
```

> ℹ️ **Nota:** Questo comando elimina solo il tag locale. Se il tag è stato già pushato su remoto, va eliminato anche dal remoto (vedi sezione successiva).

---

## 🏷️ Condividere (pushare) i tag su remoto

> ⚠️ **Importante:** Quando fai `git push`, **i tag non vengono inclusi automaticamente**! Devi pusharli esplicitamente.

### 🛠️ Come si pushano i tag?

**1. Pushare un singolo tag:**
```bash
git push origin v17.1.0
# Push del tag 'v17.1.0' su remoto 'origin'
```

**2. Pushare tutti i tag:**
```bash
git push origin --tags
# Push di tutti i tag locali su remoto 'origin'
```

Puoi sostituire 'origin' con il nome del tuo remoto (es. 'colt').

### 🧑‍💻 Esempio pratico

Supponiamo di aver creato vari tag e di volerli condividere:
```bash
git push origin v17.1.0
# Push di un singolo tag
git push origin --tags
# Push di tutti i tag
```

> ℹ️ **Nota:** Se hai più remoti, puoi scegliere dove pushare i tag. I tag sono fondamentali per le release su GitHub e altri servizi.

---

---

---

---

