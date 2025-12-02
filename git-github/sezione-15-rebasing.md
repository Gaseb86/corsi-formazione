# 🧩 **Sezione 15: Rebasing, il comando più temuto di Git?**


---

## ❓ Perché il Rebasing fa paura? È davvero così?

> 👨‍🏫 **Esperienza personale:**
>
> Quando ho iniziato a usare Git, mi è stato detto di evitare il comando `git rebase` a tutti i costi. "Non preoccuparti, può davvero incasinare il lavoro tuo e del team. Non è per principianti!". E in parte è vero: rebasing può essere rischioso se non sai cosa stai facendo.

Per anni ho usato Git senza mai fare un rebase. Mi sono sempre arrangiato con i merge e, se proprio serviva, cercavo soluzioni su Stack Overflow. Non è un comando essenziale per chi inizia, e si può lavorare tranquillamente solo con i merge.

Un giorno, però, insegnando in un bootcamp, uno studente mi ha chiesto del rebase davanti a tutta la classe. Non ero preparato! Così ho studiato, ho fatto ricerche e ora uso il rebase regolarmente.

> 💡 **Morale:** Il rebase può essere molto utile, ma bisogna sapere quando NON usarlo. Esiste una regola d'oro che vedremo in questa sezione.

---

## 🔀 Merge vs Rebase: due filosofie

La comunità Git è divisa: alcuni usano sempre il rebase, altri lo evitano. Alcune aziende lo richiedono, altre lo vietano. Il rebase è un'alternativa al merge per combinare branch:

- **Workflow 1:** Usare `git rebase` invece di `git merge` per integrare branch.
- **Workflow 2:** Usare il rebase per "pulire" la propria storia di commit (history cleanup).

Entrambi i metodi hanno pro e contro. In questa sezione vedremo quando e come usare il rebase, e soprattutto quando evitarlo!

> 📝 **Nota:** Puoi lavorare benissimo solo con i merge, ma conoscere il rebase ti dà più strumenti e flessibilità. Oggi è sempre più diffuso!

---

## ⚔️ Merging vs Rebasing: confronto pratico

---

### 🔎 Il problema dei merge commit

Immagina di lavorare su un progetto con 10 sviluppatori. Tutti lavorano su nuove feature, bugfix, ecc. Tu crei un branch `feature`, lavori e fai commit. Nel frattempo, altri colleghi fanno merge su `main` (o `master`).

Per tenere il tuo branch aggiornato, devi fare spesso `git merge main` sul tuo branch. Ogni volta che lo fai, Git crea un **merge commit**:

```
main:   A---B---C------D---E
				\     /   /
feature:         F---G---H
				     |   |
				     M1  M2
```
M1, M2 = merge commit

Se il progetto è molto attivo, il tuo branch si riempie di merge commit che non raccontano nulla del tuo lavoro. La storia diventa "sporca" e difficile da leggere.

> ⚠️ **Svantaggio:** I merge commit rendono la storia meno lineare e più difficile da analizzare.

---

### 🧹 Rebasing: storia pulita e lineare

Con il rebase, invece di fare merge, "sposti" tutti i tuoi commit sopra l'ultima versione di `main`. La storia diventa lineare:

```
git switch feature
git rebase main

main:   A---B---C---D---E
						\
feature:                 F'
```
F', G', H' = i tuoi commit riscritti sopra la nuova base

Non ci sono merge commit! Tutti i tuoi cambiamenti sono "in fila" dopo quelli di `main`.

> ✨ **Vantaggio:** La storia è più pulita, leggibile e focalizzata sui cambiamenti reali.

---

### 📊 Tabella di confronto

| Metodo      | Pro                        | Contro                       |
|------------|----------------------------|------------------------------|
| Merge      | Semplice, sicuro           | Storia "sporca", tanti merge |
| Rebase     | Storia lineare, leggibile  | Riscrive la storia, rischi   |

---

### 📝 Conclusione

Entrambi i metodi portano allo stesso risultato: il tuo branch contiene tutte le modifiche di `main` e le tue. La differenza è **come** viene rappresentata la storia.

> 💡 **Consiglio:** Usa il rebase per una storia pulita, ma solo se sai cosa stai facendo! Nei team, segui sempre le regole condivise.

---

## 🧑‍💻 Demo: Setup & Merging (workflow tradizionale)

Vediamo come si presenta la storia dei commit usando solo i merge, prima di passare al rebase.

### 1️⃣ Setup iniziale

```bash
mkdir RebaseDemo
cd RebaseDemo
git init
touch website.txt
git add website.txt
git commit -m "initial commit"
echo "NAV BAR ADDED" >> website.txt
git commit -am "add navbar"
```

### 2️⃣ Creazione branch feature

```bash
git switch -c feat
touch feature.txt
echo "feature" > feature.txt
git add feature.txt
git commit -m "begin feature"
echo "ONE" >> feature.txt
git commit -am "work on feature"
```

### 3️⃣ Nuovo lavoro su master

```bash
git switch master
echo "FOOTER ADDED" >> website.txt
git commit -am "add footer"
```

### 4️⃣ Merge master su feature

```bash
git switch feat
git merge master
# Si genera un merge commit
```

### 5️⃣ Altri commit su feature

```bash
echo "TWO" >> feature.txt
git commit -am "more work on feature"
```

### 6️⃣ Nuovo lavoro su master

```bash
git switch master
echo "LOGIN FORM ADDED" >> website.txt
git commit -am "add login form"
```

### 7️⃣ Altro merge master su feature

```bash
git switch feat
git merge master
# Si genera un altro merge commit
```

### 🔎 Risultato

La storia del branch `feat` ora contiene:
- I tuoi commit
- I commit di master
- Diversi merge commit che "sporcano" la storia

> ⚠️ **Nota:** Su progetti grandi, la storia può diventare molto difficile da leggere!

---



## 🧑‍💻 Demo: Rebasing in pratica

Vediamo ora come il rebase riscrive la storia e rende la cronologia lineare, eliminando i merge commit.

### 1️⃣ Rebasing dopo i merge

Supponiamo di essere sul branch `feat` dopo aver fatto diversi merge da `master`:

```bash
git switch feat
git rebase master
# Tutti i commit del branch feat vengono riscritti sopra l'ultimo commit di master
```

**Risultato:**

```
master:   A---B---C---D---E---F (image gallery)
							  \
feat:                          G'--H'--I'
```
G', H', I' = i tuoi commit riscritti

Non ci sono più merge commit! La storia è lineare e pulita.

### 2️⃣ Rebasing invece del merge

Se su `master` viene aggiunto un nuovo commit (es: "add image gallery") e vuoi aggiornare il tuo branch `feat`:

```bash
git switch master
echo "IMAGE GALLERY ADDED" >> website.txt
git commit -am "add image gallery"
git switch feat
git rebase master
# Tutti i commit di feat vengono riscritti sopra l'ultimo commit di master
```

**Risultato:**

La storia rimane lineare, senza merge commit. I commit del branch `feat` sono "spostati" sopra l'ultimo commit di master.

### 🔎 Differenza tra merge e rebase

- **Merge:** Crea merge commit, la storia si ramifica e si sporca.
- **Rebase:** Riscrive la storia, la cronologia è lineare e leggibile.

> ✨ **Vantaggio:** Con il rebase, la storia del tuo branch è chiara e focalizzata solo sui tuoi cambiamenti.

---

## 🏅 La regola d'oro: quando **NON** fare rebase

Il rebase è potente, ma può creare grossi problemi se usato nel momento sbagliato!

### ❓ Perché rebase invece di merge?

- La storia è più pulita e leggibile
- I tuoi commit sono raggruppati e facili da revisionare
- Nei progetti open source con tanti collaboratori, la cronologia è più chiara

### ⚠️ **La regola d'oro del rebase**

> **Non fare mai rebase su commit che hai già condiviso con altri!**

Se hai già pushato il tuo branch su GitHub e altri lo hanno scaricato, **non fare rebase**: riscrivere la storia di commit condivisi crea conflitti e problemi difficili da risolvere.

**Quando puoi fare rebase?**
- Su branch locali che nessuno ha ancora scaricato
- Su commit che sono solo tuoi

**Quando NON devi fare rebase?**
- Su branch già condivisi con il team
- Su commit che altri hanno già sul loro computer
- Sui branch principali (`main`/`master`) condivisi

> 🚨 **Attenzione:** Se riscrivi la storia di commit condivisi, il team avrà una cronologia diversa e sarà difficile sincronizzare il lavoro!

### 📝 In sintesi

- Il rebase riscrive la storia: usalo solo su commit che sono tuoi e non condivisi
- Prima di pushare, puoi rebaseare per pulire la storia
- Dopo il push, **non rebaseare** se altri hanno già scaricato il branch

> 💡 **Consiglio:** Se lavori in team, segui sempre le regole aziendali o del progetto. Chiedi prima di fare rebase su branch condivisi!

---

---

## 🧑‍💻 Gestire i conflitti durante il rebase

Quando usi `git rebase`, puoi incontrare conflitti proprio come con il merge. Ecco una demo pratica:

### 1️⃣ Simuliamo un conflitto

Supponiamo che tu abbia modificato `website.txt` sia su `master` che su `feat`:

**Su feature branch:**
```bash
echo "TOP NAVBAR ADDED" > website.txt
echo "LOG OUT FORM ADDED" >> website.txt
git commit -am "update website on feat"
```

**Su master:**
```bash
echo "MAIN NAVBAR ADDED" > website.txt
echo "SIGN UP FORM ADDED" >> website.txt
git commit -am "update copy on master"
```

### 2️⃣ Proviamo il rebase

```bash
git switch feat
git rebase master
# Si verifica un conflitto su website.txt
```

### 3️⃣ Risolvi il conflitto

Apri il file segnalato (`website.txt`), scegli quali righe mantenere (puoi combinare le modifiche di entrambi i branch), poi:
```bash
git add website.txt
git rebase --continue
```

Se vuoi annullare tutto:
```bash
git rebase --abort
```

### 4️⃣ Conclusione

Il rebase prosegue dopo la risoluzione del conflitto. Alla fine, la storia sarà lineare e i cambiamenti di entrambi i branch saranno integrati.

> ⚠️ **Nota:** I conflitti durante il rebase si risolvono come quelli del merge: scegli cosa tenere, aggiungi il file, continua il rebase.

---