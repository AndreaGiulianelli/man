# Manuale Git
## Descrizione Git
Git è un sistema peer-to-peer di database chiave/valore su file system

Non c'è un server: il repository è locale ---> + veloce

Per git il progetto è l'unità indivisibile di lavoro, perciò quando faccio un commit
git mi risalva tutto il progetto e NON LE MODIFICHE SUI SINGOLI FILE

* il file system è la directory con i tuoi file.
* il repository è il database locale su file che conserva i vari commit
* l’index è lo spazio che git ti mette a disposizione per creare il tuo prossimo commit prima di registrarlo definitivamente nel repository

Quando git salva i file nel database CHIAVE/VALORE:
* CHIAVE: calcola lo SHA1 del contenuto
* VALORE: contenuto stesso del file

---
## Comandi Git

### Configurare git:
``` bash
git config --global user.name "Nome"
git config --global user.email "email"
```

### Inziare a gestire il progetto con git
``` bash
git init
```

### Aggiungere un file all'index
``` bash
git add NOMEFILE
```

### Per fare un commit
``` bash
git commit -m "TESTO DI DESCRIZIONE DEL COMMIT"
```

### GUI che permette di vedere la storia del progetto
```
gitk --all &
```

### Oppure direttamente dalla shell(Visualizza tutto lo storico)
``` bash
git log --graph --all --oneline
```

### Visualizzare i vari HASH dei commit fatti
``` bash
git log --oneline
```

### Tornare ad un commit
``` bash
git checkout HASH/BRANCH
```

### Creare un branch
```bash
git branch NOMEBRANCH HASH
```

### Se voglio creare il branch sul COMMIT DOVE MI TROVO
``` bash
git branch NOMEBRANCH
```

### Eliminare un branch
```bash
git branch -d NOMEBRANCH
```

### Creare un branch e spostarsi sopra (-b)
```bash 
git checkout -b NUOVOBRANCH
```

### Per vedere le differenze tra due branch --> quali modifiche devo effettuare a FROM per farlo uguale a TO?
```bash
git diff FROMBRANCH1 TOBRANCH2
```

### Conoscere gli HASH dei commit tra due branch senza visualizzarli tutti
```bash
git log BRANCH1..BRANCH2 --oneline
```

### Spostare un branch nella posizione in cui mi trovo (Dopo ovviamente bisogna spostarsi sopra)
```bash
git branch --force feature
```

### Aggiungere tutti i file modificati e poi fare un commit (-a --> aggiunge i file)
```bash
git commit -am "DESCRIZIONE DEL COMMIT"
```

## **Cherry-pick**

### Applica i cambiamenti introdotti da un commit in un altro punto del repository (Dove ti trovi in quel momento) 
### Cherry-pick “coglie” il commit che gli indichi e lo applica sul commit dove ti trovi.
```bash
git cherry-pick BRANCH/HASH
```

### Spostare il RAMO CORRENTE sulla nuova BASE: ed è equivalente a spostare tutti i commit e il branch tramite cherry-pick
```bash
git rebase BASE
```

## **Merge**
### Fonde tra loro due commit/branch
### Mi sposto sul branch che voglio aggiornare e faccio un merge con quello nuovo
```bash 
git merge NOMEBRANCH
``` 
### Hai chiesto a git: “procurami un _commit_ che contenga tutto quello che c’è nel mio _branch_ corrente e aggiungici tutte le modifiche introdotte dal ramo _NOMEBRANCH_”

## **Fast-foward merge**
### Esegue un merge in linea: l'etichetta si sposta in avanti
### Il merge di due branch è eseguito in fast-forward quando è possibile spostare il primo ramo sul secondo semplicemente spingengolo in avanti
### Il merge non può essere fast-forward quando i due branch si trovano su linee di sviluppo divergenti


## **Octopus merge**
### Su git il numero di genitori di un commit non è limitato a due. In altre parole, puoi mergiare tra loro quanti branch vuoi, in un colpo solo
```bash
git checkout BRANCHVECCHIO
git merge uno due tre quattro ...........
```

## **Risolvere i conflitti nel merge**
### Git mette a disposizione diversi tool:
### Tra cui:
```bash
git mergetool --tool=emerge
```

### Ci sono diversi comandi:
* *__n__*  -->  Ti mostra con dei caratteri le righe in cui il codice è diverso e dopo con 'a' e 'b' scelgo quali delle due voglio
* *__q__* ---> Chiudo

### Dopo faccio un commit e digito :wq per uscire dall'editor di testo per il commit
### Oppure apro il file con il notepad e mi farà notare le stesse cose (Cancello qullo di cui non ho bisogno)



## **Connessione Remota GitHub**
### Aggiungere un repository REMOTO
```bash
git remote add NOMEREPO INDIRIZZO/PATH
```

### Spedire un set di commit al repository remoto
```bash
git push NOMEREPO NOMEBRANCH
```

### Ricevere dati dal repo-remoto
```bash
git fetch NOMEREPO 
```

### Ricevere dati ed effettuare i merge eseguiti da remoto
```bash
git pull NOMEREPO NOMEBRANCHDAMERGE
```