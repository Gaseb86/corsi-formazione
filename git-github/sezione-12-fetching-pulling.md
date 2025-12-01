# Sezione 12: Fetching & Pulling

## Remote tracking Branches: What are they?

Questa sezione è dedicata a come ottenere il codice da GitHub sul proprio computer, fondamentale per collaborare con altri. Prima di parlare dei comandi git fetch e git pull, è importante capire come funziona la clonazione di un repository e il concetto di remote tracking branch.

Quando cloni un repository da GitHub, ottieni tutti i file e la cronologia dei commit, ma anche due riferimenti di branch:
- Il branch locale (es. main o master)
- Il branch di tracking remoto (es. origin/main o origin/master)

Il branch di tracking remoto è un "segnalibro" che indica l’ultimo stato conosciuto del branch remoto su GitHub. Puoi visualizzarlo con:
```
git branch -r
```

Questi riferimenti partono dallo stesso punto, ma possono divergere se fai nuovi commit localmente. Il branch di tracking remoto ti aiuta a sapere dove si trova il branch remoto rispetto al tuo branch locale.

Nei prossimi paragrafi vedrai come questi concetti sono utili per sincronizzare il tuo lavoro con quello degli altri.

## Controllare e lavorare con i remote tracking branches

Quando fai nuovi commit sul branch locale (es. main), il riferimento locale si aggiorna, mentre il remote tracking branch (es. origin/main) resta fermo all’ultimo stato noto su GitHub.

Puoi vedere la differenza con:
```
git status
```
Se sei "head" di origin/main, significa che hai commit locali non ancora pushati.

Puoi anche controllare lo stato del remote tracking branch con:
```
git branch -r
```

Se vuoi vedere com’era il progetto all’ultimo aggiornamento da GitHub, puoi fare:
```
git checkout origin/main
```
Questo ti porta in modalità detached HEAD: puoi esplorare, creare un nuovo branch, oppure tornare al branch principale con:
```
git switch main
```

Quando vuoi sincronizzare i tuoi commit locali con GitHub, usa:
```
git push origin main
```
Dopo il push, il remote tracking branch si aggiorna e il tuo branch locale sarà "up to date" con origin/main.

Ripetendo il processo, puoi vedere come i riferimenti divergono e si riallineano dopo ogni push.

## Lavorare con i remote branches

Quando cloni un repository che ha più branch su GitHub, localmente ottieni solo il branch di default (main o master). Gli altri branch esistono come remote tracking branches (es. origin/movies, origin/fantasy).

Per vedere tutti i branch remoti:
```
git branch -r
```

Per lavorare su un branch remoto che non hai ancora localmente, usa:
```
git switch nome-branch
```
Se il branch esiste su origin, Git crea il branch locale e lo collega automaticamente al branch remoto corrispondente.

Esempio:
```
git switch movies
```
Ora hai un branch locale movies collegato a origin/movies. Puoi lavorarci, fare commit e push come su qualsiasi branch.

Se fai modifiche:
```
git add file.txt

git commit -m "aggiunta file"

git push origin movies
```

Questo workflow semplifica la collaborazione su branch multipli e ti permette di lavorare facilmente su nuove funzionalità o bugfix creati da altri membri del team.

## Git Fetch: il comando base

Il comando `git fetch` permette di scaricare le modifiche dal repository remoto (es. GitHub) senza integrarle direttamente nel tuo branch locale o nella tua working directory.

- Scarica i nuovi commit e aggiorna i remote tracking branches (es. origin/main), ma non modifica i tuoi file locali.
- Utile per vedere cosa è cambiato su GitHub prima di unire le modifiche al tuo lavoro.

### Sintassi
```
git fetch
```
Scarica tutte le modifiche da tutti i branch del remote origin.

```
git fetch origin nome-branch
```
Scarica solo le modifiche di uno specifico branch.

Dopo aver fatto fetch, puoi vedere le modifiche con:
```
git log origin/main
```
Oppure puoi esplorare i file con:
```
git checkout origin/main
```

Il tuo branch locale rimane invariato finché non esegui un merge o un pull.

In sintesi: `git fetch` aggiorna i riferimenti remoti sul tuo computer, ma non tocca i tuoi file locali. È il modo più sicuro per vedere le novità prima di integrarle.

