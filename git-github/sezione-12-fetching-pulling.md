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

