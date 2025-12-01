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

