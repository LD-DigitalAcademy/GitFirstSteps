# ![enter image description here](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e0/Git-logo.svg/1280px-Git-logo.svg.png)Fenomenali poteri cosmici sul codice...

Dunque siete qui per imparare a viaggiare nel tempo e tra i possibili universi (limitatamente parlando al codice, ma immagino fosse chiaro...) 

Bene, siete nel posto giusto, ma da grandi poteri derivano un sacco di menate, ma anche un sacco di poteri, ma anche un sacco di menate, ma anche un sacco di poteri... (potrebbe andare avanti per un po'...)


# 1 - Git: che cos'e'

E' uno strumento che vi permette di versionare dei file contenuti in una cartella (cioe' di tracciare i cambiamenti che li interessano).
Potete scattare una fotografia a quei file e metterla da parte, perche' non si sa mai...
Inoltre vi offre la possibilita' di creare dei binari paralleli nello sviluppo, se volete fare prove o state collaborando.

![enter image description here](https://uploads.sitepoint.com/wp-content/uploads/2019/06/155993572204-gitflow.png)

## 1.1 - Installazione

Per scaricare git, andate qui:

> https://git-scm.com/downloads

Se siete su windows, andranno benissimo le impostazioni di default che vi vengono proposte dal wizard di installazione.

Su mac consiglio di installare il packet manager Homebrew, e poi di fare il comando 

`brew install git`

Alla fine dell'installazione, per controllare che sia andato tutto bene provate a dare da un terminale, il comando:

    git --version

Se vi ritorna un numero di versione siete apposto, provate a ripetere il processo di installazione, oppure no, non posso dirvi cosa fare sono solamente un file.

A questo punto fate rimane l'ultimo passo: presentarvi a git.

    git config --global user.name "inserite il vostro nome qui"
    
    git config --global user.email "e@qui.la.vostra.mail"

Controllate a questo punto di aver configurato correttamente con il comando:

> git config -l

Che vi stampera' a terminale il file di configurazione in cui dovrebbero essere contenute anche le proprieta' che avete appena aggiunto.

**Nota**: abbiamo usato il flag *- -global*, ma potete anche toglierlo e specificarlo per ogni repository, se avete delle identita' segrete o state lavorando/facendo progetti personali.

Cioe' ogni volta che create una repository potete specificare la vostra identita':

    git config  user.name "inserite il vostro nome qui"
    
    git config  user.email "e@qui.la.vostra.mail"

Dire a git chi siete e' fondamentale per poterlo usare, presentatevi senza tante storie e passiamo alla parte in cui impariamo ad usarlo

# 2 - Utilizzo di git

## 2.1 - Qualche concetto e ciclo di vita

 - **Workspace:** e' la cartella che avete scelto come contenitore nel vostro sistema per il lavoro.
 - **Repository:** e' l'insieme dei file che avete fatto tracciare a git, sono le cose che vi interessa tenere sotto controllo.
 - **Stage:** e' la fase del processo ci di permette di aggiungere i file alla repository. Nell'immagine sotto ci dice che la aggiungiamo ad un indice (index = stage per semplificare)
 - **Commit**: fotografia scattata alla **repository**. Abbiamo deciso di fare un salvataggio in quel momento e possiamo riusarlo come punto di ritorno. Ha bisogno di un messaggio che brevemente esplichi cosa si e' fatto in questo salvataggio di stato.
 - **Branch:** si tratta di un ramo parallelo nella storia della **repository**: da un certo punto in poi abbiamo deciso che da un certo **commit** in avanti abbiamo creato due strade possibili.

![enter image description here](http://interactionprototyping.github.io/exercises/images/github/git-stages.svg)


## 2.2 - Fase 0: Ini(t)zializzazione della repository

Per creare una nuova repository, andate nella working directory e da terminale:

    git init
    
che creera' una cartella nascosta .git, dove avviene tutta la magia. Potete controllare da file explorer oppure se siete su sistemi linux-based (come mac ad esempio) con il comando:

    ls -a

Invece controllate lo stato della repository (o repo da qui) con il comando:

    git status
    
Usate git status dopo ogni comando per vedere cosa cambia... 

## 2,3 - Fase 1: Add, aggiungere un file alla repository e quindi al tracciamento

E' giunto il momento di dire git di chi si deve preoccupare...

    git add nome.del.file.con.estensione

per aggiungere un file

    git add .

per aggiungere tutti quelli nella cartella
    
    git add tutti.i file.che volete.aggiungere
    
per specificare una lista di file da aggiungere ( separati da spazio)

ricordo di usare

    git status
    
per vedere cosa cambia... fatelo eh, non fate i pigri...

## 2.4 - Fase 2: Commit dei cambiamenti

Se con ***git add*** stiamo dicendo a git "oh fre tieni d'occhio i cambiamenti di sta roba qui" con ***git comit*** gli stiamo dicendo "fre sti cambiamenti che ho fatto mi piacciono un sacco, ricordateli".

L'unico dettaglio che ci manca e dire cosa abbiamo fatto in quei cambiamenti, in maniera tale che siano poi riconoscibili. I commenti dei commit devono essere fatti **BENE** se no mi arrabbio: fidatevi non volete vedere un file di testo che perde le staffe. 

Na roba del tipo "*fixed issue #548832 on subimit button*" o "*added the change avatar functionality for users*" vanno bene, roba tipo '*prova 12345678 e 12345678 stacco*" oppure "4 commit" non si possono vedere... 

Se non vi fidate fate:

    git log

che vi fa vedere lo storico dei commit: se non vi sforzate di essere un po' ordinati, non ci capite piu' nulla e tutti sti poteri non vi serviranno ad una ceppa di niente...

Vi lascio sto link per approfondire...

https://chris.beams.io/posts/git-commit/

Promettemi che li fate bene, per favore!

Ricapitoliamo: 

    git commit -m "messaggio sintetico che riassuma i cambiamenti"

e con git log guardate tutti i salvataggi/ fotografie che avete fatto. 

### 2.4.1 - Altre raccomandazioni e linee guida per i commit

Ora che vi ho detto come fare un commit bene vediamo di capire come e' fatto un buon commit, ovvero cosa ci va in un commit.

Per semplificare proverei a fare un parallelismo con un videogioco (salvare = commit):

 - Salvare prima di un Boss / Provare qualcosa di nuovo 

	 - in questo senso facciamo un commit e potremmo fare un nuovo branch per ogni funzionalita'...
 - Salvare spesso, per non perdere progresso 
 
	 - facciamo commit "spesso": non una volta a settimana, ma quando si e' fatto qualcosa di "significativo"
 - Non quando si ha fatto del progresso in piu' missioni, ma salvare il progresso per ogni missione separatamente
	 - se modifichiamo due funzionalita', fai 2 commit, uno per ogni funzionalita' 

## 2.5 - Checkout o muoversi tra i salvataggi

Dopo aver "*salvato*" (**commit**) le modifiche che ci interessavano, come facciamo a "*caricarli*"?

Per prima cosa dobbiamo:

    git log

> commit c0dic3h4shUniv0c0ch3rappr3sent4ilC0mmitB3ll0lung0 (HEAD -> master)
Author: autore <autore@email.com>
Date:   Tue Dic 25 26:58:46 2077 +0200
repository created and added files

Che come vedete ci ritorna il codice hash del commit (quindi univoco) che dobbiamo usare nel comando

    git checkout c0dic3h4shUniv0c0ch3rappr3sent4ilC0mmitB3ll0lung0

Questo comando ci riporta allo stato del commit del codice.

per tornare all'ultimo commit di un branch, ci basta fare:

    git checkout nomeBranch

oppure inserire un altro codice per muoversi a quel commit.


## 2.6 Branches
![enter image description here](https://coderefinery.github.io/git-intro/img/octopus.jpeg)


Rappresentano timeline parallale di commit. 

Ci permetto di aggiungere feature sperimentali/nuove senza toccare la versione stabile che abbiamo.

Il branch principale di solito viene chiamato master (praticamente il tronco del nostro albero di rami) 

Se vogliamo creare un nuovo branch: 
   
    git branch nomeNuovoBranch

Per spostarsi su quel ramo

    git checkout nomeBranch

per vedere tutti i branch esistenti per la repo:

    git branch

In ultimo per spostarsi su un branch mentre lo si crea, possiamo fare:

    git checkout -b nomeNuovoBranch

### 2.61 - Linee guida per i branches

 1. Fare subito un branch **Development/Sviluppo** e tenere pulito il branch principale. Fare le modifiche a partire da questo branch
 2. Fare un branch per ogni funzionalita' maggiore: 
	 2.1. (login e autenticazione, carrello, registrazione, gestione account) e lavorare su quella feature e spostarsi quando si cambia
 3. Non fare branch personali per ogni sviluppatore, perche' poi rimettere tutto insieme e' complesso...

## 2.7 - Merge, ricostruire il puzzle

L'ultima cosa da fare e' mettere insieme i vari pezzi del codice sviluppato in diversi binari paralleli, che e' l'operazione piu' delicata.
Quando sono su un branch, per far si che le modifiche di un altro branch si applicano al branch attuale 

    git merge nomeBranchDaUnire
    
Se sono sul branch **dev** e voglio recepire le modifiche fatte sul branch **interfaceLoadingAnimation** faro'

    git merge interfaceLoadingAnimation 
e cosi' il branch dev adesso avra' tutte le modifiche fatte nel branch **interfaceLoadingAnimation**

Come funziona per i conflitti? cioe' righe modificate in entrambi? bisogna scegliere, ma vi lascio fare delle prove =)

## 2.8 Eliminare un branch

Nel casi sopra, il branch **interfaceLoadingAnimation** e' stato assorbito da **dev**: possiamo eliminarlo!

    git branch -d nomeBranchDaEliminare

# 3 Github, cos'e'?

L'unica cosa che ci manca e' la condivisione online, e github fa quello: trasporta le nostre repository sulla rete.

## 3.1 - Aggiungiamo il riferimento

 Creiamo una nuova repo su Gitub aggiungiamo il riferimento che ci danno:

    git remote add origin https://github.com/nomeUtente/nomeRepo.git

spostiamoci di branch per sincronizzarci:

    git branch -M main


## 3. - Push, mandiamo il nostro codice sul cloud
    
    git push -u origin main
