### Einleitung
Im folgenden Bericht geht es um ein Backupskript, in welchem ein bestimmtes Verzeichnis mit tar und gzip archiviert und komprimiert wird. Das dadurch erstellte, in einem eigenen Backup-Ordner liegende tar-Archiv wird anschließend noch remote auf einen anderen Computer übertragen.

### Verwendete Technologien

- VirtualBox, Version 6.1.14 r140239 (Qt5.6.2)
- Ubuntu 20.04.1 LTS

### Durchführung

1. Mit dem Befehl **nano backupscript.bash** wird der Nano-Editor geöffnet und eine Datei "backupscript.bash" erstellt, wenn das im Editor Veränderte anschließend auch gespeichert wird.
2. Das Skript beginnt mit **!/bin/bash** - dies ist der Pfad, wo die im Skript verwendeten Befehle liegen.
3. Es werden Variablen deklariert, welchen das zu sichernde Verzeichnis und das Backup-Verzeichnis zugewiesen wird. $1-$n können hierbei mit bei der Ausführung übergebenen Argumenten belegt werden. So wird es möglich, gleich bei der Skriptausführung das gewünschte zu sichernde Verzeichnis bzw. Backup-Verzeichnis als Argumente mitzugeben.
4. Mit if-Verzweigungen wird abgefragt, ob Verzeichnisse existieren oder nicht. Dies kann mit dem Ausdruck **[ -d Verzeichnisname ]** getestet werden. Falls das Backup-Verzeichnis nicht existiert, wird ein neues Verzeichnis angelegt. Bei nicht bestehendem Sicherungsverzeichnis, wird die Ausführung abgebrochen (**exit 1**).
5. Mit **tar -czf Zielordner/NameDesTarArchivs ZuSicherndesVerzeichnis** wird im gewünschten Ordner ein tar-Archiv des angegebenen Ordners, welcher dadurch auch komprimiert wird, erstellt.
6. Anschließend wird mit **[ -s Archivname ]** getestet, ob die Datei existiert und eine Größe größer 0 hat.
7. Wenn dies der Fall ist, wird mit **rsync /Verzeichnisname/NamederArchivDatei Benutzername@Ziel-IP-Adresse** die Archivdatei auf den anderen Computer übertragen.

### Verwendung

Bei der Ausführung des Backupskripts können, wie oben schon erwähnt, das Backupverzeichnis und das zu sichernde Verzeichnis als Argumente mitgegeben werden: **bash backupscript.bash \<ZusSicherndesVerzeichnis> \<Backupverzeichnis>**

Das Skript kann also dazu verwendet werden, ein Verzeichnis, z. B. Dokumente, zu sichern, indem es nach der Archivierung und Komprimierung als tar-Archiv auf einen anderen Computer übertragen wird.

### Literatur
**Ubuntuusers:** https://wiki.ubuntuusers.de/Bash
