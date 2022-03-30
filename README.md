# 🏗️ Comandi Git di uso comune

- Per controllare se abbiamo già installato Git sul nostro sistema si usa &rarr; `git --version`

- Per inizializzare una repository all'interno di una cartella &rarr; `git init`

- Creare un nuovo file all'interno di una repo &rarr; `touch [filename.extension]`

- Vedere il contenuto di un file &rarr; `cat [filename.extension]`

- Vedere lo status della nostra repository &rarr; `git status`

- Aggiunge all'index di git (Staging area) tutti o alcuni files &rarr; `git add .` o `git add [nomefile.estensione]` o `git add [*.estensione]`

- Per fare una commit &rarr; `git commit -m "[messaggio di commit]" -m "[descrizione del commit]"`

- Per evitare di usare `git add` prima di ogni commit, possiamo optare per &rarr; `git commit -am "[messaggio di commit]"` dove il parametro `-a` sta per 'all'.

- Togliere dei file dall'index di git (Staging area) &rarr; `git restore --staged [filename.extension]`

- Per vedere lo storico delle varie commits &rarr;`git log`

- Vedere il contenuto del file HEAD e quindi sapere dove punta &rarr; `cat .git/HEAD`

- Vedere lo storico delle commits in maniera più minimale &rarr; `git log --oneline`

- Recupera i cambiamenti emessi dall'ultima commit facendone una nuova &rarr; `git revert`

- Per cambiare il messaggio dell'ultima commit &rarr; `git commit --amend -m "message"`

- Per annullare una commit:
  
  - `git reset` che di default è _--mixed_ &rarr; annulla la commit e rimuove i file dalla Staging Area &rarr; ***TL:DR: Remove the commit and the stage area***
  
  - `git reset --soft` &rarr; rimuove la commit e recupera lo status successivo alla Staging Area &rarr; ***TL:DR: Remove the commit***
  
  - `git reset --hard` &rarr; rimuove l'ultima commit e tutti i file aggiunti alla Staging Area, rimuove anche fisicamente i files! &rarr; ***TL:DR: Remove the commit, the stage area and delete the files!***

>***DA NOTARE:*** possiamo usare `git reset --[parametro]` con l'ID della commit o `HEAD` e la posizione temporale della commit al quale vogliamo fare riferimento, così: `git reset --[parametro] HEAD~1` in caso ci riferissimo alla penultima commit `HEAD` o `git reset --[parametro] HEAD~2` in caso volessimo fare riferimento a 2 commit prima della `HEAD`.

Per evitare che con il comando `git add .` si inseriscano nella Staging Area tutti i file, dobbiamo settare un file `.gitignore` che conterrà tutti i file, le cartelle e le estensioni che vogliamo evitare di committare. Possiamo anche creare delle regole per permettere singoli file di estensioni che vogliamo escludere totalmente.
```
*.txt
!file.txt
```
<br/>
<br/>

## 🦺 Branch
Il modo comune di utilizzare un branch è mantenere la versione stabile del software come branch principale, e tutte le altre funzionalità sperimentali o che possono comportare correzioni di bug o addirittura rendere instabile il software, sono destinate ad essere archiviate in qualche branch laterale.

Il branch `master` ha questo nome che gli viene attribuito dalla prima inizializzazione della nostra repo.

All'inizio il branch è solamente _"un' etichetta"_ che identifica l'ultimo commit di quello specifico branch.

Per vedere una rappresentazione grafica dei nostri branches possiamo usare il comando &rarr; `git log --all --decorate --oneline --graph`

Possiamo anche usare degli Alias con questi comandi per evitare di doverli scrivere tutte le volte.
Ho creato due Alias che permettono di fare la stessa cosa ma con un briciolo di chiarezza in più per quello che è il mio gusto personale.

```PowerShell
hist = log --pretty=format:\"%Cgreen%h %Creset%cd %Cblue[%cn] %Creset%s%C(yellow)%d%C(reset)\" --graph --date=relative --decorate --all
llog = log --graph --name-status --pretty=format:\"%C(red)%h %C(reset)(%cd) %C(green)%an %Creset%s %C(yellow)%d%Creset\" --date=relative
```

- Per creare un branch usiamo &rarr; `git branch [nome]`

Per vedere tutti i branches usiamo `git branch` senza nessun parametro.
Ogni nuovo branch che viene creato punterà all'ultimo commit, quindi dove punta l'`HEAD`.

- Per spostarci tra i branches dobbiamo muovere la nostra `HEAD`, per farlo usiamo &rarr; `git checkout [nome branch]`

- Dopo che abbiamo modificato i files in ogni branch, potremmo volerli riunire sotto il main branch.
Per farlo possiamo usare &rarr; `git merge`

- Prima di unire i branch possiamo andare a visualizzarne le differenze con il comando &rarr; `git diff [primo branch]..[secondo branch]`

- Per unire i branch dobbiamo usare prima &rarr; `git checkout [primo branch]`
  poi &rarr; `git merge [secondo branch]`

- I merge possono essere di diverso tipo:
  - **_FastForward_** spostando avanti il branch `master` portandolo ad agganciarsi all'ultimo commit del `secondo` branch.
  - ***Three Way Merge*** in caso si sposti la `HEAD` in un branch che non sia direttamente a contatto con il branch che vogliamo unire, git, verificherà l'ultimo commit condiviso tra i due banches e lo comparerà alla commit per verificare che non ci siano incompatibilità.

- Per vedere i branches che sono stati uniti &rarr; `git branch --merged`

- Se non ci serve più uno specifico branch possiamo rimuoverlo con &rarr; `git branch -d [nome branch]`

>***DA NOTARE:*** che se i branches non sono ancora stati uniti, possiamo forzarne la rimozione ugualmente, (perdendo il contenuto) con il paramentro in maiuscolo `-D`.

- Se vogliamo annullare un merge usiamo &rarr; `git merge --abort`

- Se vogliamo muovere la `HEAD` e allo stesso tempo creare il banch di destinazione usiamo &rarr; `git checkout -b [nome nuovo branch]`
<br>
<br>

## 🏊🏻‍♂️ Usare un server Remoto come GitHub

- Dopo aver creato un account GitHub possiamo settare l'URL dell'`origin` con &rarr; `git remote add origin [URL]`

- Per caricare la nostra repo Locale sul nostro server usiamo &rarr; `git push -u origin master`

- Per vedere la lista delle nostre `origin` &rarr; `g remote` se aggiungiamo il parametro `-v` vedremo anche gli URL.

- Per ispezionare l'`origin` Remota e controllare se la nostra repo Locale è *aggiornata* rispetto a quella Remota ed altre info, usiamo &rarr; `git remote show origin`

- Se vogliamo rinominare l'`origin` del nostro Remote server &rarr; `git remote rename origin [nuovo nome]`

- Rimuovere l'`origin` del nostro Remote server &rarr; `git remote remove origin`

- Per ottenere i files dalla repo Remota direttamente sulla repo Locale usiamo &rarr; `git fetch or git pull`

Con il comando `git fetch` otteniamo la lista di tutti i cambiamenti, ma solo la lista non i files fisici, per avere i files dobbiamo unire il nostro branch Locale con l'`origin` Remota usando `git merge origin/master`. 

- Altrimenti, possiamo fare tutto in un comando solo, ottenere direttamente i files aggiornati usando &rarr; `git pull`
  
- Se vogliamo clonare, in Locale, una repo esistente online &rarr; `git clone [URL]`.
<br>
<br>

## 👨🏼‍🏭 Fare il 'Fork' di una repo di terze parti

Una volta effettuato il Fork direttamente sul sito (GitHub) possiamo clonare in Locale la repo in maniera classica con `git clone [URL del Fork]`.

Dopo aver fatto qualche modifica alla repo 'Forkata', possiamo contribuire con le nostre modifiche alla repo originale chiedendo il permesso al proprietario.
Questo può essere fatto direttamente da GitHub.

- Se vogliamo (e se il proprietario ce lo permette) possiamo aggiungere l'URL della repo originale nell'`origin` alla nostra repo 'forkata' &rarr; `git remote add [alias] [URL della repo originale]`

- Ogni volta che il proprietario aggiunge o modifica qualcosa nella repo originale, possiamo sincronizzare la nostra 'Forked' repo per tenerla aggiornata &rarr; `git fetch [alias]` e `git merge [alias]/[nome branch]` o possiamo usare direttamente &rarr; `git pull [alias] [nome branch]`

quanto il nostro repo in Locale è aggiornato possiamo usare `git push` per caricare i cambiamenti alla repo in Remoto (la repo 'Forkata').
<br>
<br>

## 🛀🏼 Bonus

Comando che consente di usare VSCode come editor predefinito per i messaggi delle commit &rarr; `git config --global core.editor "code --wait"`
