## 1. Linux: Die Shell – Dein Tor zur Kommandozeile


 ### Grundlagen der Shell
 *   **was ist eine Shell ?** Für mich ist die Shell eine Umgebung, in der ich mit Befehlen direkt mit dem System arbeite. Im Gegensatz zur grafischen Oberfläche, wo ich mit Maus und Fenstern arbeite, kann ich in der Shell schneller und genauer Aufgaben erledigen.
 Der Vorteil der Shell ist für mich Geschwindigkeit, mehr Kontrolle und die Möglichkeit, Dinge zu automatisieren. Eine GUI ist für einfache Aufgaben bequemer, aber für komplexe Arbeiten oft langsamer.
 *   **Gängige Shells:** Häufig benutzte Shells sind Bash, Zsh und Fish. Auf den meisten Linux-Systemen, die ich genutzt habe, war Bash die Standardshell.


 ### Das Dateisystem navigieren
 *   **Orientierungspunkte:** Um zu sehen, wo ich mich gerade befinde, benutze ich pwd.
 Um Dateien und Ordner aufzulisten, nutze ich ls, und für versteckte Dateien oder mehr Details ls -a und ls -l.
 Mit cd wechsle ich zwischen Ordnern.
 *   **Pfadangaben:** Beim Üben von Pfaden habe ich den Unterschied zwischen absoluten Pfaden wie /home/user/Documents und relativen Pfaden wie ../Downloads gut verstanden.


 ### Dateien und Verzeichnisse bearbeiten
 *   **Erstellen und Verwalten:** Mit touch erstelle ich neue, leere Dateien.Mit mkdir und mkdir -p lege ich Ordner und komplette Ordnerstrukturen an.
 *   **Verschieben und Kopieren:** Dateien verschiebe ich mit mv und kopiere sie mit cp. Für Ordner benutze ich dafür meistens die Option -r.
 *   **Entfernen:** Zum Löschen benutze ich rm oder für Ordner rm -r. Ich mache das nur in einem Testordner, damit nichts Wichtiges verloren geht.
 ### Befehle kombinieren – die Macht der Pipelines
 *   **Kombinierte Aktionen:** Mit dem Pipe-Symbol | leite ich die Ausgabe eines Befehls an einen anderen weiter.


## 2. Linux: Benutzerverwaltung – Wer darf was?




 ### Überblick: root vs. normale Benutzer
 *   **Rollenverständnis:** Ich habe verstanden, dass der Benutzer root alle Rechte im System hat. Er kann Programme installieren oder löschen und sogar wichtige Systemdateien ändern. Normale Benutzer haben viel weniger Rechte und können nur in ihrem eigenen Bereich arbeiten.
 Darum sollte ich im Alltag nicht als root arbeiten, weil ein kleiner Fehler das ganze System kaputtmachen kann.
 ### Benutzer anlegen und löschen
 *   **Neue Identitäten:** Zum Anlegen neuer Benutzer habe ich Befehle wie useradd oder adduser verwendet. Dabei habe ich gesehen, dass automatisch ein Home-Ordner und einige Standardeinstellungen angelegt werden.
 *   **Benutzer entfernen:** Beim Löschen eines Benutzers nutze ich userdel und kann entscheiden, ob sein Home-Ordner bleiben oder gelöscht werden soll.
 ### Passwortverwaltung
 *   **Sicherheitsschlüssel:** Mit dem Befehl passwd habe ich für Benutzer Passwörter gesetzt. Dabei habe ich gemerkt, dass ein sicheres Passwort lang genug sein und aus verschiedenen Zeichen bestehen sollte.
 ### Die Benutzer- und Gruppenkonfiguration
 *   **Blick hinter die Kulissen:** In der Datei /etc/passwd habe ich die wichtigsten Infos über jeden Benutzer gefunden, zum Beispiel Benutzername, UID, Home-Ordner und Shell.
 In /etc/group stehen die Informationen über die Gruppen.
 *   **Zusammenhänge:** Dadurch habe ich verstanden, dass jeder Benutzer in einer oder mehreren Gruppen ist und dass Gruppen wichtig für die Zugriffsrechte sind.




## 3. Linux: Berechtigungen – Kontrolle über deine Daten


 ### Grundlagen der Dateiberechtigungen
 *   **Die magischen drei:** Ich habe gelernt, dass es drei wichtige Rechte gibt: lesen (r), schreiben (w) und ausführen (x).
 Bei Dateien bedeuten diese Rechte:


 r = Datei lesen
 w = Datei ändern
 x = Datei ausführen


 Bei Ordnern funktionieren sie etwas anders:


 r = den Inhalt des Ordners sehen
 w = Dateien im Ordner anlegen oder löschen
 x = in den Ordner hineingehen können
 *   **Gruppen von Rechten:** Diese Rechte gelten immer für drei Gruppen: Benutzer (Owner), Gruppe und Andere.
 ### Berechtigungen ansehen und interpretieren
 *   **Detaillierte Ansicht:** Mit ls -l habe ich die genauen Rechte angezeigt. Die Zeichenkette wie -rw-r--r-- zeigt die Rechte in drei Blöcken:
 die ersten drei für den Besitzer
 die nächsten drei für die Gruppe
 die letzten drei für alle anderen
 Mit etwas Übung konnte ich die Ausgabe gut lesen.
 ### Berechtigungen ändern
 *   **Kontrolle übernehmen:** Zum Ändern der Rechte habe ich chmod benutzt.
 Ich habe die symbolische Schreibweise ausprobiert, zum Beispiel:
 chmod u+r file.txt
 chmod g+w file.txt
 *   **Eigentümer und Gruppen:** Den Besitzer oder die Gruppe habe ich mit chown und chgrp geändert.
 ### Praktische Beispiele
 *   **Szenarien:** Ich habe mehrere kleine Aufgaben ausprobiert:


 1. Datei nur für den Besitzer lesbar machen:
   chmod 400 secret.txt
 
 2. Gruppe darf schreiben, andere nur lesen:
   chmod 640 report.txt


 3. Ordner, in dem nur der Besitzer Dateien anlegen oder löschen darf, aber andere hineingehen können:
   mkdir shared_dir
   chmod 711 shared_dir




Hier kann nur der Besitzer etwas verändern. Andere Benutzer können den Ordner nur betreten.


