# 🚀 **Sezione 14: Git Collaboration Workflows**

---

## 🏷️ Il workflow centralizzato: tutti su un solo branch
---

> ⚠️ **Attenzione:** Il workflow centralizzato è il più semplice (e il più rischioso) tra i flussi di lavoro collaborativi con Git!

- Tutti i collaboratori lavorano su un unico branch (di solito `main` o `master`)
- Non si creano branch separ ati per nuove funzionalità o esperimenti

### 🔎 Come funziona
1. Tutti clonano lo stesso repository da GitHub
2. Lavorano localmente sul branch principale
3. Fanno commit e cercano di fare push su GitHub
4. Prima di ogni push, devono fare `git pull` per scaricare le modifiche degli altri e risolvere eventuali conflitti

### ❌ Problemi principali
- **Conflitti frequenti:** Ogni collaboratore deve continuamente risolvere conflitti e fare merge con il lavoro degli altri
- **Codice rotto:** Se qualcuno spinge codice incompleto o con errori, tutti gli altri si ritrovano con il repository rotto
- **Nessun spazio per esperimenti:** Non si può provare nuove idee senza rischiare di danneggiare il progetto principale
- **Collaborazione difficile:** Per condividere lavoro non finito, bisogna per forza "sporcare" il branch principale

### ⏳ Quando (non) usarlo
Può funzionare solo in team molto piccoli e su progetti semplici, dove tutti sono molto coordinati. In generale, è sconsigliato per la collaborazione vera!

> 💡 **Consiglio:** Usa branch separati per nuove funzionalità, bugfix o esperimenti: vedrai che la collaborazione sarà molto più semplice e sicura!
---

## 🧑‍💻 Esempio pratico: i problemi del workflow centralizzato
---

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

> 📝 **Morale:** Il workflow centralizzato è semplice, ma poco sicuro e poco flessibile. Meglio usare branch separati!
---

## 🌿 Feature Branch Workflow: lavorare su branch dedicati
---

Il Feature Branch Workflow è il metodo più diffuso e sicuro per collaborare su progetti Git:

- Nessuno lavora direttamente su `main` o `master`
- Ogni nuova funzionalità, bugfix o esperimento viene sviluppato su un branch dedicato
- Il branch principale (`main`/`master`) rappresenta la "storia ufficiale" e stabile del progetto

### 🔎 Come funziona
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

### ✅ Vantaggi
- Il branch principale rimane sempre stabile e funzionante
- Si può collaborare su funzionalità anche non finite senza "rompere" il progetto
- Meno conflitti e merge, solo quando la feature è pronta
- Ogni collaboratore può lavorare su più branch contemporaneamente

### 🧑‍💻 Esempio pratico
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

> 💡 **Consiglio:** Tratta il branch principale come "sacro": lavora sempre su branch dedicati e fai merge solo di codice stabile!
---

## 🧑‍🤝‍🧑 Demo pratica: collaborazione con Feature Branch Workflow
---

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

> 📝 **Morale:** Con il Feature Branch Workflow puoi collaborare, sperimentare e chiedere aiuto senza "sporcare" il branch principale. Solo quando la feature è pronta si fa il merge su `main`!
---

## 🔀 Merging Feature Branches: integrare le modifiche su main
---

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

> 💡 **Consiglio:** Non fare merge "a caso"! Discuti sempre con il team e usa Pull Request per progetti più grandi o collaborativi.
---

## 📬 Introduzione alle Pull Request (PR)
---

Le **Pull Request** (PR) sono uno strumento fondamentale per collaborare su GitHub e altre piattaforme. Non fanno parte di Git "puro", ma sono una funzionalità aggiunta da servizi come GitHub, Bitbucket, GitLab.

### ❓ A cosa servono le Pull Request?
- Permettono di proporre modifiche da un branch (di solito una feature) verso il branch principale (`main`/`master`)
- Facilitano la revisione del codice: altri collaboratori possono commentare, chiedere modifiche, approvare o rifiutare
- Rendono il processo di integrazione trasparente e controllato
- Spesso sono obbligatorie nei progetti aziendali o open source: non si può fare merge diretto su `main`

### 🔎 Come funziona una Pull Request
1. Fai il push del tuo branch su GitHub
2. Apri una Pull Request dal branch di lavoro verso il branch principale
3. Scrivi una descrizione chiara: cosa hai fatto, perché, eventuali note
4. I collaboratori (o i responsabili) revisionano il codice, lasciano commenti, chiedono modifiche
5. Quando la PR è approvata, viene fatta la merge nel branch principale

### ✅ Vantaggi
- Discussione e revisione prima di integrare il codice
- Possibilità di richiedere modifiche o chiarimenti
- Maggiore sicurezza: il branch principale rimane stabile
- Tracciabilità: ogni modifica è documentata e discussa

**Esempio:**
Pamela ha finito la feature "dark mode" su un branch dedicato. Fa push su GitHub, apre una Pull Request verso `main`, descrive il lavoro, riceve feedback, apporta modifiche se richiesto, e solo quando tutto è approvato la PR viene "mergiata" su `main`.

> 💡 **Consiglio:** Usa sempre le Pull Request per integrare nuove funzionalità, bugfix o refactor su progetti condivisi!
---

## 🧑‍💻 Demo pratica: creare e gestire una Pull Request
---

Immagina che Stevie abbia finito la sua feature "navbar" su un branch dedicato e voglia integrarla su `main` tramite una Pull Request.

### 1. Push del branch su GitHub
```bash
git push origin navbar
```

### 2. Apertura della Pull Request
- Vai su GitHub, seleziona il repository
- Clicca su "Compare & pull request" accanto al branch appena pushato
- Compila titolo e descrizione, menziona collaboratori se necessario (es: @Colt)
- Clicca su "Create pull request"

### 3. Revisione e discussione
- I collaboratori possono commentare, chiedere modifiche, approvare o rifiutare
- Stevie può aggiungere nuovi commit al branch "navbar" per rispondere ai feedback

### 4. Merge della Pull Request
- Quando la PR è approvata, un responsabile (es: Colt) clicca su "Merge pull request"
- Si può scegliere di eliminare il branch dopo il merge

### 5. Aggiornamento dei branch locali
Tutti i collaboratori devono aggiornare il branch principale:
```bash
git switch main
git pull origin main
```
E possono eliminare il branch locale:
```bash
git branch -D navbar
```

> 📝 **Morale:** La Pull Request permette di integrare nuove funzionalità in modo controllato, con revisione e discussione, mantenendo il branch principale stabile!
---

## 🧩 Demo: risolvere conflitti durante il merge di una Pull Request
---

Quando si cerca di fare il merge di una Pull Request, può capitare che ci siano conflitti tra il branch della PR e il branch principale (`main`). Ecco come risolverli:

### 1. Crea una PR che genera conflitto
Supponiamo che Stevie abbia cambiato l’intestazione (`<h1>`) su un branch chiamato `new-heading`, mentre Colt ha modificato la stessa riga su `main`.

Stevie fa push e apre una Pull Request verso `main`. GitHub segnala che ci sono conflitti.

### 2. Risolvi i conflitti in locale
Colt (o chi deve gestire la PR) segue questi passaggi:
```bash
# Assicurati di avere l’ultima versione di main
git switch main
git pull origin main

# Passa al branch della PR
git switch new-heading

# Unisci main nel branch della PR
git merge main
# Git segnala i conflitti: apri il file, risolvi manualmente
# Modifica il file per mantenere le parti corrette

# Aggiungi e committa la risoluzione
git add index.html
git commit -m "risolvi conflitto tra main e new-heading"

# Torna su main e unisci il branch risolto
git switch main
git merge --no-ff new-heading

# Spingi su GitHub
git push origin main
```

### 3. Chiudi la PR e aggiorna i branch locali
La PR viene chiusa automaticamente su GitHub dopo il merge. Puoi eliminare il branch:
```bash
git branch -D new-heading
git push origin --delete new-heading
```
Tutti i collaboratori devono aggiornare il branch principale:
```bash
git switch main
git pull origin main
```

> 💡 **Consiglio:** Risolvi i conflitti localmente se sono complessi o coinvolgono molti file. Su GitHub puoi risolvere conflitti semplici direttamente dal browser!
---

## 🛡️ Branch Protection Rules: proteggere il branch principale
---

Su GitHub puoi configurare regole di protezione per i branch (branch protection rules) per aumentare la sicurezza e la qualità del codice.

### ❓ A cosa servono?
- Impediscono modifiche dirette al branch principale (`main`/`master`)
- Richiedono che tutte le modifiche passino tramite Pull Request
- Puoi obbligare la revisione di almeno un collaboratore prima del merge
- Puoi impedire la cancellazione o il force push sul branch

### ⚙️ Come si configurano
1. Vai su GitHub → Settings del repository → Branches
2. Scegli il branch da proteggere (es: `main`)
3. Aggiungi una regola di protezione:
	- Richiedi revisione PR prima del merge
	- Impedisci il force push
	- Impedisci la cancellazione del branch
	- (Opzionale) Richiedi che i test passino prima del merge
4. Salva la regola

### 🧑‍💻 Esempio pratico
- Stevie prova a modificare direttamente `main`, ma GitHub lo blocca: deve creare una feature branch e aprire una Pull Request
- La PR non può essere "mergiata" finché almeno un revisore (es: Colt) non la approva
- Si può discutere, lasciare commenti, richiedere modifiche
- Solo dopo l’approvazione la PR può essere integrata su `main`

### ✅ Vantaggi
- Maggiore controllo e qualità del codice
- Riduce il rischio di errori o modifiche non volute
- Favorisce la collaborazione e la revisione

> 💡 **Consiglio:** Attiva sempre branch protection rules su progetti condivisi o importanti!
---

## 🍴 Introduzione al Forking su GitHub
---

Il workflow "Fork & Clone" è fondamentale nei progetti open source con molti collaboratori. Invece di lavorare tutti su un unico repository centrale, ogni sviluppatore crea una copia personale (fork) del repository principale.

### ❓ Cos’è il fork?
- Forking è una funzione di GitHub (non di Git!) che permette di creare una copia di un repository su il proprio account GitHub.
- Il fork mantiene tutta la storia e i file del progetto originale, ma diventa indipendente: puoi modificarlo, sperimentare, rompere il codice senza influenzare il progetto principale.

### ⏳ Quando si usa il fork?
- Quando vuoi contribuire a un progetto open source ma non sei un collaboratore diretto
- Quando vuoi sperimentare o proporre modifiche senza toccare il repository originale

### 🔎 Come funziona
1. Vai sul repository pubblico che ti interessa
2. Clicca su "Fork" in alto a destra
3. GitHub crea una copia del repository sul tuo account
4. Puoi ora clonare il tuo fork, lavorare localmente, creare branch, fare commit e push
5. Quando hai finito, puoi proporre le tue modifiche tramite una Pull Request verso il repository originale

### ✅ Vantaggi
- Chiunque può proporre modifiche, anche senza permessi diretti
- I maintainer del progetto possono revisionare e accettare/rifiutare le proposte
- Il progetto principale rimane protetto da modifiche non controllate

> 💡 **Consiglio:** Se vuoi contribuire a un progetto open source, inizia sempre facendo il fork e lavorando sulla tua copia!
---

## 🍴🔗 Il Fork & Clone Workflow: collaborare senza permessi diretti
---

Il workflow "Fork & Clone" è il metodo più usato per collaborare su progetti open source dove non si ha accesso diretto al repository principale.

### 🔎 Come funziona, passo per passo
1. **Fork del repository:** Vai su GitHub e clicca su "Fork" per creare una copia del repository sul tuo account.
2. **Clona il fork:** Clona il tuo fork sul computer:
	```bash
	git clone https://github.com/tuo-username/nome-repo.git
	```
3. **Imposta il remote "upstream":** Aggiungi il repository originale come secondo remote, chiamato di solito `upstream`:
	```bash
	git remote add upstream https://github.com/original-owner/nome-repo.git
	```
4. **Lavora sul tuo fork:** Crea branch, fai commit e push sul tuo fork (`origin`). Puoi lavorare liberamente, sperimentare e modificare senza influenzare il progetto principale.
5. **Sincronizza con l’originale:** Se il repository originale riceve nuove modifiche, puoi scaricarle:
	```bash
	git fetch upstream
	git merge upstream/main
	```
6. **Proponi le tue modifiche:** Quando hai finito, apri una Pull Request dal tuo fork verso il repository originale (`upstream`). I maintainer possono revisionare, accettare o rifiutare la tua proposta.

### 🗺️ Diagramma concettuale
Immagina tre collaboratori (es: Colt, Taylor, Lupe) che vogliono contribuire a un grande progetto open source:
- Ognuno fa il fork del repository principale sul proprio account GitHub.
- Ognuno clona il proprio fork sul computer.
- Ognuno imposta il remote `upstream` per tenere traccia delle modifiche del progetto originale.
- Tutti lavorano sui propri fork e propongono modifiche tramite Pull Request.

Questo sistema permette a migliaia di persone di collaborare senza dover essere aggiunti come collaboratori diretti!

### ✅ Vantaggi del Fork & Clone Workflow
- Puoi lavorare liberamente senza rischiare di rompere il progetto principale.
- Puoi proporre modifiche anche se non hai permessi di scrittura.
- I maintainer mantengono il controllo sulle modifiche che vengono integrate.
- Ideale per progetti open source con molti collaboratori.

### 🛠️ Comandi fondamentali
- Fork su GitHub (interfaccia web)
- Clona il fork: `git clone ...`
- Aggiungi il remote upstream: `git remote add upstream ...`
- Sincronizza con l’originale: `git fetch upstream` e `git merge upstream/main`
- Push sul tuo fork: `git push origin nome-branch`
- Apri una Pull Request dal fork verso l’originale (interfaccia web)

### 📋 Riassunto pratico
1. Fai il fork del progetto su GitHub
2. Clona il tuo fork
3. Aggiungi il remote `upstream` per il repository originale
4. Lavora e fai commit/push sul tuo fork
5. Sincronizza periodicamente con l’originale
6. Apri una Pull Request per proporre le tue modifiche

> 📝 **Morale:** Il workflow Fork & Clone permette a chiunque di contribuire a progetti open source, anche senza permessi diretti, mantenendo il controllo e la qualità del codice!
---

