su-03-gitdemo
=============

* mein bash prompt : https://github.com/git/git/blob/master/contrib/completion/git-prompt.sh
* mein git lg1 hab ich von [Stackoverflow](http://stackoverflow.com/questions/1057564/pretty-git-branch-graphs)
* das hier kam gerade über die Railsgirls vorbei: [Der einfache Einstieg in Git](http://rogerdudler.github.io/git-guide/index.de.html)


## Basic Git Commands - SU 23.10.2014

### Workspace als Verzeichnis anlegen

|Command|Explanation||
|:--|:--|:--|
|mkdir git-demo | bash | legt unterverzeichnis an|
|cd git-demo/  | bash | "change directory" - wechselt in verzeichnis|
|ls | list files in directory||
|subl einkaufsliste.md | neue Datei editieren (subl -> Sublime editor)||
 
### Lokales Git Repository anlegen

|Command|Explanation|
|:--|:--|
|    git init | legt git repository in unterverzeichnis .git an |
|    ls -lart | listet alle dateien im langformat auf - so sieht man .-dateien |
|    git status | zeigt an, welche Dateien nur im Workspace, oder Index / Staging area sind|
|    git add . | fügt aktuelles Verzeichnis (.) dem Index hinzu |
|    mkdir einunterverzeichnis | bash: legt unterverzeichnis an |
|    touch einunterverzeichnis/hallo.md | bash: legt datei an |
|    git status||
|    git add .||
|    git status||
|    git add -A .| fügt alle Änderungen, auch das löschen von Dateien, dem Index hinzu|
|    git status||
|    git commit -m "initial commit" | der erste commit mit message |
|    git status||
|    less .git/config| bash: less zeigt Inhalt der Config datei an| 

### Variante 1: mit vorhandenem Git-Repository verbinden

|Command|Explanation|
|:--|:--|
|    git remote add origin git@github.com:bkleinen/git-demo.git| remote repository, dass vorher auf github angelegt wurde, bekannt machen - die url von der github seite kopieren|
|    less .git/config| das steht dann in der config!|
|    git push origin master| Änderungen in das remote Rep. pushen|
|    cd ..| bash: eine Verzeichnisebene höher|

### Variante 2: GitHub Repository Klonen

- Zuerst auf Github neues repository anlegen, falls nicht mit einem schon vorhandenem gearbeitet werden soll 

|Command|Explanation|
|:--|:--|
|    git clone git@github.com:htw-imi-info3/su-03-gitdemo.git | s.o. |
|    ls | siehe da: su-03-gitdemo ist jetzt da|
|    cd su-03-gitdemo/ | bash: wechsle in das verzeichnis|
|    ls||
|    ls -a||
|    less .git/config| remote steht jetzt schon in der konfig|
 
### Demo mit zwei parallelen lokalen Repositories

|Command|Explanation|
|:--|:--|
|    mv su-03-gitdemo/ su-03-gitdemo-personA| bash: mv - move nennt dateien um|
|    cd su-03-gitdemo-personA/ ||
|    subl . | irgendwas editieren|
|    git status||
|    git add added-by-a.md| fügt einzelne datei dem index zu|
|    git commit -m "added cheese by a"||
|    git lg1||
|    git push origin master||

#### jetzt das selbe remote rep nochmal klonen, in ein anderes unterverzeichnis, dort änderung machen
 
|Command|Explanation|
|:--|:--|
|    cd ..||
|    git clone git@github.com:htw-imi-info3/su-03-gitdemo.git su-03-gitdemo-personB|| 
|    ls||
|    cd su-03-gitdemo-personB/||
|    ls||
|    subl added-by-a.md||
|    git status||
|    git add .||
|    git commit -m "added milk by B"||
|    git push origin master||
|    cd ..||

#### von A aus holen

|Command|Explanation|
|:--|:--|
|    cd su-03-gitdemo-personA||
|    ls||
|    less added-by-a.md| - änderung noch nicht da|
|    git pull --rebase origin master ||
|    git lg1| jetzt ja|

 
#### Arbeiten mit einem branch

|Command|Explanation|
|:--|:--|
|    git checkout -b freitagseinkauf| neuen branch anlegen und auschecken|
|    git branch| listet branches auf|
|    subl freitagseinkauf.md||
|    git status||
|    git add .||
|    git commit -m "freitag von A"||
|    git status||
|    git lg1||
|    git checkout master||
|    subl  added-by-a.md||
|    git commit -am "change in master by a"||
|    git lg1||
|    git push origin master||
|    pwd| "print working directory| 
|    git lg1||
|    git push origin freitagseinkauf| push the new branch as well| 

#### neuen Branch von local repository B aus holen

|Command|Explanation|
|:--|:--|
| cd /Users/kleinen/Dropbox/info3/code/git-demo/class/su-03-gitdemo-personB/ ||
| git pull --rebase origin master | master holen mit rebase|
| git lg1 ||
| git pull origin freitagseinkauf | mergt den branch in master!|
| git lg1 ||
| git push origin master | diesen merge pushen|
| git lg1 ||

#### neuen branch erst holen, dann auschecken -> master bleibt unverändert

|Command|Explanation|
|:--|:--|
| git fetch origin freitagseinkauf | holt den branch nur in das lokale repository, nicht in den workspace|
| git lg1 ||
| git checkout freitagseinkauf ||

#### und Nochmal von A aus...

|Command|Explanation|
|:--|:--|
|    git lg1||
|    git pull origin master||
|    git lg1||
|    git checkout freitagseinkauf||
|    ls||
|    subl freitagseinkauf.md||
|    git commit -am "change in Branch F."||
|    git push origin freitagseinkauf||
|    git checkout master||
