# Sezione 19: The Power of Reflogs - Retrieving Lost Commits

# 🚦 Introduzione ai Reflog in Git

I **reflog** (reference log) sono i registri interni che Git mantiene ogni volta che un riferimento (branch, HEAD, tag, ecc.) viene aggiornato o spostato.

## 🔎 Cosa sono i reflog?
- Sono una cronologia delle modifiche ai riferimenti (branch, HEAD, remoti...)
- Ogni volta che HEAD cambia (nuovo commit, cambio branch, reset, ecc.), Git registra l'evento
- Ogni branch ha il suo reflog, così come HEAD

## 📁 Dove si trovano?
- Nella cartella `.git/logs/` trovi:
  - `HEAD`: log di tutti i movimenti di HEAD
  - Un file per ogni branch locale e remoto

Questi file sono **leggibili** (testo), non compressi o binari

## 🧑‍💻 Esempio pratico
1. Cambia branch:
   ```bash
   git switch turtle
   # In .git/logs/HEAD viene aggiunta una riga: checkout: moving from master to turtle
   ```
2. Vai in detached HEAD:
   ```bash
   git checkout <commit>
   # In .git/logs/HEAD: checkout: moving from turtle to <commit>
   ```
3. Torna su un branch:
   ```bash
   git switch master
   # In .git/logs/HEAD: checkout: moving from <commit> to master
   ```

## 📝 Perché sono utili?
- Permettono di recuperare commit "persi" o non più visibili con git log
- Sono fondamentali per il recupero dopo errori (reset, rebase, branch cancellati)
- Puoi vedere la cronologia di ogni branch, HEAD, remoti

## ⚠️ Limiti dei Reflog

- I reflog sono **solo locali**: ogni sviluppatore vede solo la propria cronologia dei riferimenti, non quella degli altri.
- Non vengono sincronizzati tra collaboratori o repository remoti.
- I reflog **non sono permanenti**: le voci più vecchie vengono eliminate dopo circa 90 giorni (valore predefinito, modificabile).
- Non sono quindi un archivio storico eterno, ma uno strumento di recupero recente.

> 💡 **In sintesi:** I reflog sono utilissimi per recuperare errori recenti, ma non sostituiscono la storia ufficiale del repository (i commit).

> ⚠️ **Attenzione:** Non modificare mai manualmente questi file! Sono gestiti da Git.

Nel prossimo paragrafo vedrai come usare il comando `git reflog` per consultare facilmente questi log.

---

## 🛠️ Il comando git reflog show

Il comando principale per consultare i reflog è:

```bash
git reflog show <riferimento>
```
- `<riferimento>` può essere HEAD, un branch locale, un branch remoto, ecc.
- Mostra la cronologia delle modifiche a quel riferimento (spostamenti, commit, reset, checkout...)

### 🔍 Differenza tra git log e git reflog
- `git log` mostra solo la storia dei commit visibili (la "storia ufficiale")
- `git reflog show` mostra **tutti** i cambiamenti, anche quelli "nascosti" (reset, rebase, branch cancellati, checkout, ecc.)
- Puoi recuperare commit persi o non più visibili con git log

### 🧑‍💻 Esempi pratici
```bash
git reflog show HEAD
# Mostra la cronologia di HEAD (tutti i movimenti)

git reflog show master
# Mostra la cronologia del branch master

git reflog show donkey
# Mostra la cronologia del branch donkey
```

### 📌 Sintassi dei riferimenti numerici
- Ogni riga del reflog ha un identificatore relativo: `HEAD@{0}` è l'evento più recente, `HEAD@{1}` il penultimo, ecc.
- Questi numeri cambiano ogni volta che si aggiorna il reflog
- Puoi usare questa sintassi per riferirti a uno stato passato:

```bash
git checkout HEAD@{3}
# Torna allo stato di HEAD di 3 eventi fa
```

> ℹ️ **Nota:** Puoi usare la stessa sintassi con altri riferimenti, es: `master@{2}`

---

## 🔗 Usare e passare riferimenti dei reflog

La sintassi `<riferimento>@{N}` permette di riferirsi a una specifica voce del reflog (es: `HEAD@{2}` = HEAD due mosse fa).

### 🛠️ Come si usano?
- Puoi passare questi riferimenti a molti comandi git:
  - `git checkout HEAD@{2}` → Torna allo stato di HEAD di due eventi fa
  - `git diff HEAD@{0} HEAD@{5}` → Mostra le differenze tra ora e 5 mosse fa
  - `git reflog show master@{3}` → Mostra la cronologia del branch master a 3 eventi fa

### 📌 Differenza con la sintassi tilde (~)
- `HEAD~2` → Due commit genitori fa (nella storia dei commit)
- `HEAD@{2}` → Due eventi fa nel reflog (potrebbero essere cambi branch, reset, checkout, ecc.)

### 🧑‍💻 Esempio pratico
```bash
git reflog show HEAD
# Vedi la lista degli eventi

git checkout HEAD@{3}
# Torna allo stato di HEAD di 3 eventi fa (potrebbe non essere un commit diverso)

git diff HEAD@{0} HEAD@{5}
# Differenze tra lo stato attuale e quello di 5 eventi fa
```

> ℹ️ **Nota:** Puoi usare questa sintassi con qualsiasi riferimento: branch, HEAD, remoti...

---

## ⏳ Qualificatori temporali nei reflog

Ogni voce del reflog ha un timestamp: puoi usare riferimenti temporali per navigare la cronologia!

### 🛠️ Sintassi
- `<riferimento>@{yesterday}`
- `<riferimento>@{2.days.ago}`
- `<riferimento>@{1.hour.ago}`
- `<riferimento>@{2023-11-01 10:00:00}` (data e ora specifica)

### 🧑‍💻 Esempi pratici
```bash
git diff master master@{yesterday}
# Differenze tra lo stato attuale di master e quello di ieri

git checkout master@{1.week.ago}
# Vai allo stato di master di una settimana fa (detached HEAD)

git reflog show HEAD@{2.days.ago}
# Mostra il reflog di HEAD fino a due giorni fa
```

### ℹ️ Note
- Puoi usare "yesterday", "2.days.ago", "1.hour.ago", "1.week.ago", ecc.
- Funziona con HEAD, branch, remoti...
- I riferimenti temporali sono utili per trovare rapidamente uno stato passato senza contare le mosse
- Ricorda: i reflog sono solo locali e di solito non vanno oltre 90 giorni

> 💡 **Consiglio:** Usa i qualificatori temporali per recuperare rapidamente uno stato "funzionante" dopo errori o modifiche complesse.

Nel prossimo paragrafo vedrai come usare i reflog per recuperare commit persi o annullare operazioni rischiose.

---

## 🆘 Recuperare commit persi con il reflog

Il reflog è uno strumento potentissimo per recuperare commit "persi" dopo reset, rebase o errori.

### 🧑‍💻 Esempio pratico: recuperare un commit dopo un reset --hard
1. Crea una serie di commit:
   ```bash
   git init
   echo "broccoli\nrainbow chard\nkale" > veggies.txt
   git add veggies.txt
   git commit -m "Plant winter veggies"
   echo "cabbage\nlettuce\narugula" >> veggies.txt
   git commit -am "Add more greens"
   echo "watermelon\npumpkins\nsquash" >> veggies.txt
   git commit -am "Add summer seeds"
   ```
2. Fai un reset hard per "perdere" l'ultimo commit:
   ```bash
   git log --oneline
   # Prendi l'hash del penultimo commit
   git reset --hard <hash-penultimo-commit>
   # L'ultimo commit sparisce da git log
   ```
3. Recupera il commit perso con il reflog:
   ```bash
   git reflog show master
   # Trova l'hash del commit perso (es: fb5072a)
   git checkout fb5072a
   # Oppure:
   git checkout master@{1}
   # Ora sei in detached HEAD, ma puoi vedere il commit
   ```
4. Ripristina il commit come nuovo tip del branch:
   ```bash
   git reset --hard master@{1}
   # Oppure:
   git reset --hard fb5072a
   # Il commit "perso" torna visibile in git log
   ```

### ℹ️ Note
- Il reflog tiene traccia di tutti i movimenti recenti, anche quelli che "cancellano" commit
- Puoi recuperare commit persi finché sono ancora presenti nel reflog (di solito 90 giorni)
- Funziona anche per branch cancellati, rebase, merge, ecc.

> 💡 **Consiglio:** Se perdi un commit, non disperare! Controlla sempre il reflog prima di pensare che sia tutto perso.

Nel prossimo paragrafo vedrai come annullare un rebase usando il reflog.

---

## 🔄 Annullare un rebase con il reflog

Il reflog permette di recuperare anche i commit che sembrano persi dopo un rebase (specialmente interattivo), dove la storia viene riscritta e i vecchi commit non sono più visibili nel log.

### 🧑‍💻 Esempio pratico: recuperare commit dopo un rebase interattivo
1. Crea un branch di feature e una serie di commit:
   ```bash
   git switch -c flowers
   echo "salmon zinnia\nqueen lime zinnia" > flowers.txt
   git add flowers.txt
   git commit -m "Add flowers file"
   echo "old rose dahlia\ndinnerplate dahlia" >> flowers.txt
   git commit -am "Add dahlias"
   echo "coral fountain amaranth\nhot biscuits amaranth" >> flowers.txt
   git commit -am "Add amaranth"
   echo "coral reef celosia" >> flowers.txt
   git commit -am "Add celosia"
   ```
2. Esegui un rebase interattivo per "squashare" i commit:
   ```bash
   git rebase -i HEAD~4
   # Scegli 'fixup' o 'squash' per unire i commit
   # Modifica il messaggio se vuoi
   ```
   Dopo il rebase, avrai un solo commit nel log:
   ```bash
   git log --oneline
   # Solo 1 commit visibile
   ```
3. Recupera i commit "persi" tramite reflog:
   ```bash
   git reflog show flowers
   # Trova l'hash di uno dei commit precedenti al rebase
   git reset --hard <hash-commit-perso>
   # Ora il branch punta di nuovo a quel commit e ai suoi genitori
   git log --oneline
   # Tutti i commit "persi" sono tornati!
   ```

### ℹ️ Note
- Dopo un rebase, i vecchi commit non sono più visibili nel log, ma sono ancora referenziati dal reflog finché non vengono eliminati dal garbage collector.
- Puoi recuperare l'intera sequenza di commit semplicemente resettando il branch al commit desiderato trovato nel reflog.
- Questo trucco funziona anche per merge, cherry-pick e altre operazioni che riscrivono la storia.

> 💡 **Consiglio:** Prima di disperare dopo un rebase "sbagliato", consulta sempre il reflog: spesso puoi ripristinare tutto!

