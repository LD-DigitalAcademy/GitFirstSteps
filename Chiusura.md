
# Git + VSCODE

  

## Prerequisiti

  
### 1 - Installare git

  

controllare se e' gia installato:

  

`git --version`

  

altrimenti installare -> https://git-scm.com/downloads

  

e configurare l'identita':

  

`git config --global user.name "nome"`

`git config --global user.email "e@mail"`

  

controllate con

  

`git config --global --list`

  
  

installare vscode -> https://code.visualstudio.com/download

  

## Creare repo locale


Aprire un terminale in vs code **nella working folder** e fare

`git init`

oppure seezionare **source control** tra le icone a sinistra

![enter image description here](https://code.visualstudio.com/assets/docs/editor/versioncontrol/initialize-repository.png)

quindi inizializza repository

vi creera' cosi' il branch **master** e lo potete vedere in basso a sinistra (vi dice in che branch siete)

![enter image description here](https://assets.digitalocean.com/articles/git-integration-in-visual-studio-code/9.png)

cliccando qui sopra e' possibile muoversi tra i branch e crearne nuovi.

![enter image description here](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSyqO205GWgsU5xZmYAdpsjIkxpIRm8sT1s2Q&usqp=CAU)



## Committare

creare un file e salvarlo e se torniamo sul menu source control vediamo

![enter image description here](https://assets.digitalocean.com/articles/git-integration-in-visual-studio-code/4.png)

Una lettera che rappresenta lo stato del file:

 - U -> Untracked
 - A -> Added to repo
 - M -> Modified

e dei bottoni che facendo mouse over vi dicono cosa fanno , in questo caso il **+** aggiungera' il file per il tracciamento,

In ultimo il tasto con la spunta permette di fare commit (ricordate i messaggi fatti bene)

Esiste la possibilita' di fare commit in maniera diversa, per esempio provate "amend"

### Git Diff

e' possibile vedere le differenze nei file modificati cliccandoci 2 volte sopra. 

Vicino ai numeri delle righe trovate anche delle linee colorate, sperimentate!


## 4 - Connettere in remoto

Create una vuota su github (tastino + in alto a destra)

copiatevi il link, aprite un terminale in vs code (controllate di essere nella cartella corretta) e incollate il comando che vi danno sulla homepage

`git remote add origin https://github.com/NomeUtente/NomeRepo.git`

### git pull vs git  fetch

Cosa fa **git fetch**?  preleva i cambiamenti dal branch remoto e li aggiunge al nostro branch locale

e' molto safe perche' non cambia la versione di codice su cui stiamo lavorando (domanda quindi, possiamo finire in detached head? provate!)

#### detached head 

> per semplificare -> HEAD puntatore della vostra posizione, alcune operazioni possono spostarlo senza dirvi nulla e creare situazioni spiacevoli...
> detached head -> per semplificare -> non punto ad un branch ma ad un commit
> e' utile a volte, ma dovete stare attenti perche' i cabiamenti che state facendo potrebbero andare persi (git tende ad eliminare i detached changes)!
> recuperare files cancellati ad esempio 
![enter image description here](https://blog.git-init.com/content/images/2021/08/HEAD.004.png)
> 
> 
> non e' un solitamente un problema ma va usata con cognizione
> 
> condivido un paio di link per capire meglio:
> https://stackoverflow.com/questions/10228760/how-do-i-fix-a-git-detached-head/58142219
> https://www.baeldung.com/git-detached-head

cosa fa **git pull**? fa un **git fetch** e un **git merge**, scarica il branch remoto e cerca di unirlo con il locale dando precedenza ai cambi in remoto! (potrebbe fallire in che fase? perche'? leggete il terminale sempre =) )  
quindi cambia il codice su cui stiamo lavorando ed e' piu' "pericoloso"!

### git reset & git revert & git checkout

- git checkout, lo conoscete vi permette di muovermi tra branch/commit
- git revert, vi permette di eliminare un commit particolare (undo/indietro per un singolo commit)
	- crea un nuovo commit che "cancella" le modifiche committate
	
- git reset /!\ ATTENZIONE /!\ rimuove definitivamente i commit
	- vi permette di fare in modo che tutti i commit fino a quello a cui avete fatto il reset non siano mai avvenuti...
	- Riporta lo stato della repo ad un commit precedente
	- cosa succede alle modifiche fatte nel frattempo? provate a fare status/log
	- se facciamo `git reset --hard nomeBranch/nomeCommit` non si torna indietro mai piu'
	- Puo' servire ad annullare un merge mal riuscito/non finito

### git clone vs git fork

serve a scaricare la repository la prima volta, poi useremo pull e push in corretta cobinazione

![enter image description here](https://miro.medium.com/max/1400/1*lWez3rFZacK-tbmYvDBR1w.png)

git fork invece permette di poter "clonare" la repository separatamente rispetto alla repo orginale

di solito serve per scenari del genere: 

- vedete un errore in un progetto open/ dovete sviluppare una nuova feature di un progetto gia' avviato
- forkate la repo (create una copia vostra sconnessa)
- implementate
- mandte una richiesta di pull al proprietario/mantenitore della repo per far incorporare le vostre modfiche

![enter image description here](https://cdn.ttgtmedia.com/rms/onlineimages/cdo-git_clone_vs_fork-f_mobile.png)


### git push

permette di portare i cambiamenti su un branch locale ad uno remoto. Di seguito la documentazione che vi consiglio di guardare perche' puo' facilitarvi la vita
https://git-scm.com/docs/git-push

sottolineo il fla `-n / --dry-run`  che vi fa cosa succederebbe senza fare realmente tutto.

### git merge vs git rebase

Entrambi i comandi permottono di portare cambiamenti da un branch specificato a quello in cui siamo, cerchiamo di capirne il funzionamento

il comando git merge, aggiunge i cambiamenti del branch che specifichiamo al branch in cui ci troviamo

`git merge nomeBranchDiCuiVogliamoAggiungereDeiCambiamenti`

Quando abbiamo dei conflitti? per esempio quando abbiamo modificato la stessa riga nello stesso file.

se non ve la sentite piu'

`git merge --abort` 

invece se siete convinti, guardate l'interfacccia che nei file incriminati vi presentera' 4 opzioni: 

 - accept current: i cambiamenti del branch attuale sono quelli definitivi post merge
 - accept incoming: i cambiamenti del branch che stiamo unendo verranno resi definitivi
 - accept both: prima gli attuali poi gli altri, ma va bene tutto!
 - compare changes: due finestre affiancate che vi mostrano le differenze

potete anche eseguire un edit manuale del file per renderlo permanente.

a questo punto se avete letto il terminale dovete fare un add seguito da commit.
Questa e' una delle differenze principali tra i due comandi, come potete vedere sotto.

![enter image description here](https://miro.medium.com/max/1400/1*Y77kjfj3xgPz_YRYa8Zmsg.png)

#### git rebase

Funziona in maniera opposta, prende i cambiamenti dal branch specificato, mettendo da parte i miei cambiamenti, che tentera' di ricommittare uno alla volta (cioe' di aggiungerli dopo).

Purtroppo questa operazione e' pericolosa in quanto riscrive la storia (cambiano gli ID dei commit), quindi bisogna stare molto attenti quando si fanno perche' si rischia di creare stati della repo diversi da persona a persona.  

I conflitti si gestiscono nello stesso identico modo che nei merge.

per provare, usate il comando `git rebase -i altroBranch` il flag meno i vi permette di avere interattivita' con il terminale e vi fa vedere le cose passo per passo.






## Git Blame

quando le cose andranno male servira' fare troubleshooting, e se volete sapere quali, da chi e dove sono state fatte le modifiche:

`git blame nome.file` 

vi dira' autore, ora e modifiche apportate

`git blame -L 1,+12 nome.file`

vi permette di limitare la ricerca ad un intervallo di righe (che va da 1 in questo caso a 12)

`git blame --since=1.week nome.file`

## Estensioni interessanti

 - git history
 - git lens
 - git graph
 - git blame
