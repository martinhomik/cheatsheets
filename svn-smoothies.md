## Find last 50 commits by mhomik

```sh
svn log --search mhomik -l 50
```

## Recursively delete .svn folders:

```sh
rm -rf `find . -type d -name .svn`
```

## Sort lines for 'svn status'
```sh
svn status | sort -k 2
```

## Checkout

smerf trunk

```sh
svn co <SVN-URL>/smerf/trunk smerf
```

smerf branch (Example)

```sh
svn co <SVN-URL>/smerf/branches/FEATURE_1 smerf_feature_1
```

heidi trunk

```sh
<SVN-URL>/heidi/trunk heidi
```

## Update

```sh
svn up
svn update
```

Status anzeigen

```sh
svn st
svn status
```

## Änderungen anzeigen

Änderung der Datei im Workspace im Vergleich zur neuesten Revision im SVN

```sh
svn diff Dateiname
```

Änderung der Datei im Workspace im Vergleich zur bestimmten Revision im SVN

```sh
svn diff -r12345 Dateiname
```

## Committen

alle Änderungen

```sh
svn ci
```

mit Text in einer Zeile

```sh
svn ci -m 'my committ comment' 
```

nur bestimmten Änderungen (Beispiel)

```sh
svn ci -m 'mein text' pfixschlundAS/trunk/projects/dslorder-de/conf/order.conf.xml
```

## Änderungen zurücknehmen

Änderung einer einzelnen Datei zurücknehmen:

```sh
svn revert pfixschlundAS/trunk/projects/dslorder-de/conf/order.conf.xml
```

Alle Änderung zurücknehmen (zum Beispiel nach einem Merge):

```sh
svn revert -R .
```

## Löschen von Dateien (Beispiel)

```sh
svn rm pfixschlundAS/trunk/projects/dslorder-de/conf/order.conf.xml
```

Wiederherstellen von Dateien, die gelöscht wurden und in einen neuen Pfad einfügen (Beispiel)

```sh
svn copy https://svn.1and1.org/svn/PFXNGH/nghwizard/branches/HOST.974/projects/ngh_us/img/testimonials@2636 https://svn.1and1.org/svn/PFXNGH/nghwizard/branches/HOST.974/projects/ngh_us/img/frontend-ngh
@2636 -> @[Revisionsnummer]
```

## Branchen

Übersicht anzeigen

```sh
svn ls <SVN-URL>/smerf/branches/
Branch erstellen (Beispiel)
```


```sh
svn cp <SVN-URL>/smerf/trunk <SVN-URL>/smerf/branches/CON.450 -m "<Kommentar>"
```

## Tag erstellen

Vom der aktuellen Revision

```sh
svn cp <SVN-URL>/smerf/trunk <SVN-URL>/smerf/tags/pre-CON.450
```

Von einer alten Revision

```sh
svn cp -r55966 <SVN-URL>/smerf/trunk <SVN-URL>/smerf/tags/pre-CON.518
```

Switchen (lokale Änderungen bleiben erhalten)

```sh
svn switch <SVN-URL>/smerf/trunk
```

Informationen anzeigen

```sh
svn info <SVN-URL>/smerf/trunk
```

Änderungen zeilenweise mit verantwortlichen Personen anzeigen

```sh
svn blame projects/dslorder-de/conf/order.conf.xml | less
```

Branch erstellen (Beispiel)

```sh
svn cp <SVN-URL>/smerf/trunk <SVN-URL>/smerf/branches/CON.450 -m "<Kommentar>"
```

## Mergen

### Merge Branch in Branch

Wir mergen Ausgangsbranch
```
https://svn.1and1.org/svn/PFX/application-name/branches/ausgangsbranch (erste Revisionsnummer 1234) 
```

in Zielbranch

```sh
https://svn.1and1.org/svn/PFX/application-name/branches/zielbranch (letzte Revisionsnummer 5678)
```

In den Zielbranch wechseln
erste Revisionsnummer aus dem Ausgangsbranch nehmen
letzte Revisionsnummer aus dem Zielbranch nehmen

```sh
svn merge -r1234:5678 https://svn.1and1.org/svn/PFX/application-name/branches/ausgangsbranch
```

Rausfinden von welchen Branch Release bis zum Merge Release gearbeitet wurde

Im Branch aufrufen

```sh
svn log --stop-on-copy
```

Merge Test OHNE Ausführung

```
svn merge --dry-run --ignore-ancestry -r
```

### Merge in den Trunk

- In den ausgecheckten Trunk wechseln
- erste Revisionsnummer aus dem Branch nehmen
- letzte Revisionsnummer aus dem Trunk nehmen

```sh
svn merge --ignore-ancestry -r54476:54913 <SVN-URL>/smerf/branches/CON.450 .
```

Beim Mergen in den Trunk ist merge-rechts immer der Branch.

### Merge vom Trunk in den Branch

- in den ausgecheckten Branch wechseln

Jetzt gibt es zwei Möglichkeiten:

#### Der Trunk wurde noch nie in den branch gemerged:
- mit svn log --stop-on-copy -v die Version herausfinden, wann der branch erstellt wurde. Hier ist es z.B. 66468 und nicht die Version, bei der der neue Branch committed wurde.

```sh

r66470 | fehrenbach | 2008-11-07 16:55:32 +0100 (Fr, 07. Nov 2008) | 2 lines
Geänderte Pfade:
A /pfixorder/branches/HOST.479 (von /pfixorder/trunk:66468)

new branch for HOST.479
```

```sh
svn merge -r 66468:66571 https://svn.1and1.org/svn/PFX/pfixorder/trunk .
```
        
- eventuelle Konflikte auflösen
- Änderungen comitten (wichtig: als Kommentar das merge-Kommando angeben):

```        
svn ci -m "MERGED: svn merge -r 66468:66571 https://svn.1and1.org/svn/PFX/pfixorder/trunk ."
```

####Der Trunk wurde bereits schon einmal in den branch gemerged:

- mit svn log --stop-on-copy die Version herausfinden, die beim letzten Merge die höchste Version war (wenn man obiges Beispiel nimmt ist das 66571).
- die Revisionsnummer bis zu der gemerged wird ist die aktuelle Revisionsnummer (z.B. mit svn up).

```sh
svn merge -r 66571:66666 https://svn.1and1.org/svn/PFX/pfixorder/trunk .
```

- eventuelle Konflikte auflösen
- Änderungen comitten (wichtig: als Kommentar das merge-Kommando angeben):
        
```sh
svn ci -m "MERGED: svn merge -r 66468:66571 https://svn.1and1.org/svn/PFX/pfixorder/trunk ."
```

Wer bei einem Merge Meldungen in der Form

```sh
Skipped missing target: 'projects/oneandone_us/htdocs/style/general'
```

bekommt, sollte den Merge wiederholen und den Output in eine Datei umleiten, zum Beispiel

```sv
svn merge -r119495:121026 https://svn.1and1.org/svn/PFX/pfixorder/trunk
> merge.txt
```

Hier hat man mit großer Wahrscheinlichkeit im Branch eine Datei gelöscht(verschoben), die im Trunk geändert wurde. Anschließend kann man sich den diff besorgen, der 'verloren' gehen würde. Zum Beispiel:

```sh
cat merge.txt | grep ^Skip | cut -d ':' -f2 | cut -d "'" -f2 | xargs -i svn diff -r119495:121025 https://svn.1and1.org/svn/PFX/pfixorder/trunk/{} > changes.txt
```

Die Änderungen wurden hier in die Datei changes.txt geschrieben. Diese kann man sich anschauen und die Änderungen, falls nötig, in die neuen Dateien nachziehen.

### Merge zurück in den Trunk (nachdem man den Trunk in den Branch gemerged hat)

- nochmals den Trunk in den Branch mergen (siehe oben)
- in den auscheckten Trunk wechseln
- mit svn up updaten (die aktuelle Versionsnummer ist die, die beim svn up angezeigt wird)

```sh
svn merge trunk-url@revision-des-letzten-commits branch-url@revision-des-letzten-commits (revisionen müssen gleich sein)
```

- Änderungen comitten

## Konflikte

Konflikte anzeigen

```sh
svn st | grep "C "
```

Konflikte lösen (Beispiel)

```sh
svn resolved pfixschlundAS/trunk/projects/dslorder-de/conf/order.conf.xml
```

Für alle Konflikte die Branch Version verwenden

(aktuelle Versionsnummer verwenden!)

```sh
for i in `svn st | grep "C " | cut -c8-100`; do rm $i; mv $i.merge-rechts.r99999 $i; svn resolved $i; done;
```

Alte Versionen aus dem Repository wieder herstellen

```sh
svn up -r 12345 "datei"
mv "datei" "datei"_old
svn up "datei"
mv "datei"_old "datei"
```

## Ignorieren von Dateien:

Im aktuellen Verzeichnis:

```sh
svn propedit svn:ignore .
```

- Alles eintragen, was nicht ins SVN soll
- Status zeigt M . an
- Committen (evtl. ist vorher ein Update notwendig)

## SVN konfigurieren

Passwort speichern deaktivieren

In der Datei $HOME/.subversion/config muss folgender Eintrag stehen:

```sh
store-auth-creds = no
```

Alle neuen Dateien hinzufügen

```sh
svn st | grep "? " | sed 's|\?||' | xargs svn add
```
