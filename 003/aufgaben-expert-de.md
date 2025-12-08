## Aufgabe 1: Log-Forensik – Systemanomalien aufdecken
### 1.1 Untersuchung fehlgeschlagener Anmeldeversuche
Identifiziere alle fehlgeschlagenen SSH-Login-Versuche der letzten 24 Stunden.

\````
sudo grep "Failed password" /var/log/auth.log
\````

\````
 sudo journalctl -u ssh --since "24 hours ago" | grep "Failed password"
\````

- Welche IP-Adressen sind dafür verantwortlich?

\````
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}'
\````

- Wie viele Versuche gab es pro IP-Adresse?

\````
sudo gerp “Failed password” /var/log/auth.log | awk '{print $(NF-3)}' | sort -nr | uniq -c
\````

- Zu welchen Uhrzeiten traten diese Versuche auf?

\````
sudo grep "Failed password" /var/log/auth.log | awk '{print $1, $2, $3}' 
\````

- Welche Benutzerkonten wurden dabei ins Visier genommen?

\````
 sudo grep "Failed password" /var/log/auth.log  | awk '{print $(NF-5)}' 
\````

### 1.2 Analyse eines Dienst-Wiederherstellungsereignisses

- Rekonstruiere mithilfe von `journalctl` und relevanten Logdateien, wann dieser Dienst zuletzt gestartet, neu gestartet oder seinen Status geändert hat.

\````
 sudo journalctl -u sshd --reverse “
“ systemctl status sshd
\````


- Finde Einträge, die auf einen unerwarteten Fehler oder eine Warnung unmittelbar vor einem Neustart hinweisen könnten (falls vorhanden).

\````
sudo journalctl -u sshd -p warning --since "1 hour ago" 
\````

- Analysiere, welche Informationen `journalctl` spezifisch für diesen Dienst bietet, die in den regulären Logdateien vielleicht weniger detailliert sind.

\````
sudo journalctl -u sshd --since "2024-01-01 10:00" --until "2024-01-01 12:00"
\````

## Aufgabe 2: Tiefenanalyse der Boot-Sequenz

### 2.1 Boot-Vorgang rekonstruieren

- Identifiziere den genauen Startzeitpunkt des Kernels und das Ende der Boot-Phase

\````
 sudo journalctl -b 
 sudo journalctl -b | head
 systemd-analyze
\````
- Welche kritischen Systemd-Einheiten (Units) wurden während des Boot-Vorgangs gestartet und beendet?


- Gab es während des Boot-Vorgangs Fehlermeldungen oder Warnungen, die auf potenzielle Probleme hinweisen könnten?

\````
 sudo journalctl -b -p warning
\````


### 2.2 Dienststartzeiten und Abhängigkeiten

- Finde heraus, welche Dienste die längste Zeit zum Starten benötigten.

\````
 systemd-analyze blame
\````

- Untersuche die Abhängigkeiten von mindestens zwei wichtigen Systemdiensten, die früh im Boot-Prozess gestartet werden. Wie beeinflusst die Startreihenfolge die Gesamtzeit des Boot-Vorgangs?

\````
 systemctl list-dependencies sshd 
\````

## Aufgabe 3: Dienst-Architektur und Abhängigkeiten

### 3.1 Analyse einer Dienst-Unit

- Zeige den vollständigen Inhalt der systemd-Unit-Datei für diesen Dienst an.

\````
 systemctl cat systemd-logind.service “
\````

- Erläutere die Bedeutung der Abschnitte `[Unit]`, `[Service]` und `[Install]`.

[Unit]
Beschreibungen und Abhängigkeiten des Dienstes.
 Enthält unter anderem: Requires=, Wants=, After=, Before=.

[Service]
Definiert, wie der Dienst ausgeführt wird: simple, forking, notify, usw.
 Pfad zur ausführbaren Datei des Dienstes: ExecStart=
 Verhalten beim Neustart: Restart=

[Install]
Legt fest, ob der Dienst beim Systemstart aktiviert wird.
 Enthält typischerweise: WantedBy=multi-user.target

- Identifiziere in der Unit-Datei alle direkten und indirekten Abhängigkeiten (z.B. `Requires`, `Wants`, `After`, `Before`). Welche anderen Dienste oder Targets müssen vorhanden oder gestartet sein, damit dein gewählter Dienst korrekt funktionieren kann?

\````
Requires=systemd-user-sessions.service
After=basic.target nss-user-lookup.target
\````

### 3.2 Auswirkungen von Dienst-Manipulationen

- Wähle einen Dienst, der von deinem zuvor analysierten Dienst abhängt (eine seiner `Requires=` oder `Wants=` Abhängigkeiten).

\````
 systemctl status systemd-logind
 systemctl status systemd-user-sessions
\````

- Untersuche den Status beider Dienste.
 Wenn Requires= gesetzt ist:
  Das Anhalten der abhängigen Unit führt zum Anhalten des Hauptdienstes.

 Wenn Wants= gesetzt ist:
  Der Hauptdienst läuft weiter, auch wenn die abhängige Unit gestoppt wird.

- **Ohne den Hauptdienst zu stoppen**, überlege, welche Auswirkungen das Stoppen oder Deaktivieren des abhängigen Dienstes auf den Hauptdienst hätte. Begründe deine Annahme basierend auf den Abhängigkeitsdefinitionen in den Unit-Dateien. Bestätige deine Annahme, indem du die Log-Ausgaben beider Dienste nach dem manipulierten Start oder Stopp des abhängigen Dienstes überprüfst.

\````
 sudo journalctl -u systemd-logind -n 50
sudo journalctl -u systemd-user-sessions -n 50
\````