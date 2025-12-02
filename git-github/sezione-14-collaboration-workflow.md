# Sezione 14: Git Collaboration Workflows

## Il workflow centralizzato: tutti su un solo branch

Il workflow centralizzato è il più semplice (e il più rischioso) tra i flussi di lavoro collaborativi con Git:

- Tutti i collaboratori lavorano su un unico branch (di solito `main` o `master`)
- Non si creano branch separ ati per nuove funzionalità o esperimenti

### Come funziona
1. Tutti clonano lo stesso repository da GitHub
2. Lavorano localmente sul branch principale
3. Fanno commit e cercano di fare push su GitHub
4. Prima di ogni push, devono fare `git pull` per scaricare le modifiche degli altri e risolvere eventuali conflitti

### Problemi principali
- **Conflitti frequenti:** Ogni collaboratore deve continuamente risolvere conflitti e fare merge con il lavoro degli altri
- **Codice rotto:** Se qualcuno spinge codice incompleto o con errori, tutti gli altri si ritrovano con il repository rotto
- **Nessun spazio per esperimenti:** Non si può provare nuove idee senza rischiare di danneggiare il progetto principale
- **Collaborazione difficile:** Per condividere lavoro non finito, bisogna per forza "sporcare" il branch principale

### Quando (non) usarlo
Può funzionare solo in team molto piccoli e su progetti semplici, dove tutti sono molto coordinati. In generale, è sconsigliato per la collaborazione vera!

**Consiglio:** Usa branch separati per nuove funzionalità, bugfix o esperimenti: vedrai che la collaborazione sarà molto più semplice e sicura!

## Esempio pratico: i problemi del workflow centralizzato

Immagina due collaboratori, Colt e StevieChicks, che lavorano sullo stesso repository GitHub, entrambi sul branch principale (`main`).

### 1. Clonano il repository
Entrambi clonano il repo e iniziano a lavorare localmente.

### 2. Colt aggiunge e committa dei file
```bash
git add index.html
git commit -m "add index.html"
git push origin main
```

### 3. Stevie lavora su una Navbar
Stevie aggiunge una Navbar a `index.html`, committa e prova a fare push:
```bash
git add index.html
git commit -m "add navbar"
git push origin main
```
Ma riceve un errore:
```
Updates were rejected because the remote contains work that you do not have locally.
```

### 4. Stevie deve fare pull e merge
Stevie deve prima scaricare le modifiche di Colt:
```bash
git pull origin main
```
Se ci sono conflitti, deve risolverli e poi può fare push:
```bash
git push origin main
```

### 5. Codice incompleto sul branch principale
Se Stevie vuole chiedere aiuto a Colt, deve per forza pushare il suo codice incompleto su `main`, rischiando di "rompere" il progetto per tutti.

### 6. Colt deve fare pull, ma ha modifiche locali
Se Colt ha modifiche non ancora committate, Git non gli permette di fare pull:
```
Your local changes to the following files would be overwritten by merge.
Please commit your changes or stash them before you merge.
```
Colt deve committare o "stashare" le modifiche prima di poter aggiornare il repository.

### 7. Tutti i collaboratori sono costretti a lavorare sullo stesso branch
Questo porta a conflitti, merge continui e rischio di codice rotto.

**Morale:** Il workflow centralizzato è semplice, ma poco sicuro e poco flessibile. Meglio usare branch separati!

## Feature Branch Workflow: lavorare su branch dedicati

Il Feature Branch Workflow è il metodo più diffuso e sicuro per collaborare su progetti Git:

- Nessuno lavora direttamente su `main` o `master`
- Ogni nuova funzionalità, bugfix o esperimento viene sviluppato su un branch dedicato
- Il branch principale (`main`/`master`) rappresenta la "storia ufficiale" e stabile del progetto

### Come funziona
1. Tutti clonano lo stesso repository da GitHub
2. Per ogni nuova funzionalità, si crea un branch dedicato:
	```bash
	git switch -c nome-feature
	```
3. Si lavora sul branch, si fanno commit e push:
	```bash
	git add .
	git commit -m "Implementa la feature X"
	git push origin nome-feature
	```
4. Si può collaborare sullo stesso branch con altri membri del team
5. Quando la feature è pronta e testata, si fa il merge su `main` (di solito tramite una Pull Request)

### Vantaggi
- Il branch principale rimane sempre stabile e funzionante
- Si può collaborare su funzionalità anche non finite senza "rompere" il progetto
- Meno conflitti e merge, solo quando la feature è pronta
- Ogni collaboratore può lavorare su più branch contemporaneamente

### Esempio pratico
David vuole aggiungere la "dark mode" al sito:
```bash
git switch -c add-dark-theme
# Lavora, committa e pusha
git push origin add-dark-theme
```
Pamela vuole collaborare sulla stessa feature:
```bash
git fetch
git switch add-dark-theme
# Lavora, committa e pusha
git push origin add-dark-theme
```
Quando la feature è pronta:
```bash
# Su GitHub, crea una Pull Request per unire add-dark-theme su main
# Dopo la revisione, si fa il merge
```

**Consiglio:** Tratta il branch principale come "sacro": lavora sempre su branch dedicati e fai merge solo di codice stabile!

## Demo pratica: collaborazione con Feature Branch Workflow

Immagina due collaboratori, Colt e Stevie, che lavorano su un sito Bootstrap.

### 1. Stevie crea un branch per la Navbar
```bash
git switch -c navbar
# Lavora sulla navbar, committa e pusha
git add index.html
git commit -m "add broken navbar"
git push origin navbar
```
Stevie può condividere il branch anche se la navbar non è finita o funzionante.

### 2. Colt crea un branch per la pricing table
```bash
git switch -c pricing-table
# Lavora, committa e pusha
git add index.html
git commit -m "add pricing table"
git push origin pricing-table
```
Entrambi lavorano su branch separati, senza toccare `main`.

### 3. Colt aiuta Stevie sul branch navbar
Colt riceve la richiesta di aiuto, fa fetch e passa al branch di Stevie:
```bash
git fetch origin
git switch navbar
# Risolve il bug (es: aggiunge il JS di Bootstrap), committa e pusha
git add index.html
git commit -m "fix navbar bug"
git push origin navbar
```

### 4. Stevie riceve la correzione
Stevie fa pull sul branch navbar:
```bash
git pull origin navbar
```
Ora la navbar funziona!

### 5. Entrambi continuano a lavorare su altri branch
Possono sperimentare, collaborare, fare commit e push senza rischiare di rompere il branch principale.

**Morale:** Con il Feature Branch Workflow puoi collaborare, sperimentare e chiedere aiuto senza "sporcare" il branch principale. Solo quando la feature è pronta si fa il merge su `main`!

## Merging Feature Branches: integrare le modifiche su main

Quando una feature è pronta, va integrata nel branch principale (`main` o `master`). Ecco come si fa:

### 1. Parla con il team
Prima di fare il merge, è buona pratica discutere con i collaboratori e assicurarsi che la feature sia pronta e testata.

### 2. Passa al branch principale
```bash
git switch main
git pull origin main # Assicurati di avere l’ultima versione
```

### 3. Fai il merge del feature branch
Supponiamo che il branch si chiami `pricing-table`:
```bash
git merge pricing-table
```
Se non ci sono conflitti, il merge sarà "fast-forward" e immediato.

### 4. Spingi le modifiche su GitHub
```bash
git push origin main
```

### 5. Gli altri collaboratori aggiornano il branch principale
Tutti devono fare pull su `main` per ricevere le nuove modifiche:
```bash
git switch main
git pull origin main
```

### 6. (Opzionale) Elimina il feature branch
Se la feature è stata integrata e non serve più:
```bash
git branch -d pricing-table
git push origin --delete pricing-table
```

**Consiglio:** Non fare merge "a caso"! Discuti sempre con il team e usa Pull Request per progetti più grandi o collaborativi.

