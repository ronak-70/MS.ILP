##  Linux: Paketverwaltung – Dein Werkzeugkasten für Software

 **Verständnis der Paketmanager:** Bedeutung von Paketmanagern

 Paketmanager sind das zentrale Werkzeug zur Installation, Aktualisierung und Entfernung von Software unter Linux.
 Vorteile:
 Automatische Installation von Programmen inkl. Abhängigkeiten
 Sichere Updates aus offiziellen Repositories
 Saubere Deinstallation
 Keine manuelle Suche oder Installation von Binärdateien

 Unterschiede der Paketmanager-Familien

 apt (Debian/Ubuntu)
 Einfach, stabil, große Paketquellen, weit verbreitet auf Desktop und Server.

 yum/dnf (RedHat/CentOS/Fedora)
 dnf ist moderner, bessere Abhängigkeitsverwaltung, schnelleres Caching, fortgeschrittene Funktionen.
 **Praktische Übungen mit deinem Paketmanager:**
 *   **Paketinformationen abrufen:**
      *   **cat /etc/os-release**
      *    **apt search nano**
      *   **apt show nano**

 *   **Pakete installieren:** 
      *   **sudo apt install htop**
 *   **System aktualisieren:**
      *   **sudo apt update**
      *   **sudo apt upgrade**
 *   **Pakete entfernen:**  
      *   **sudo apt remove htop**
      *   **sudo apt purge htop**


##  Linux: SSH – Sicherer Zugang zur Ferne

 **Was ist SSH?**SSH ist ein verschlüsseltes Protokoll für den sicheren Zugriff auf entfernte Systeme.
 Kernfunktionen:
 Sicheres Einloggen
 Dateiübertragung (scp, sftp)
 Verschlüsselte Tunnel

 Sicherheitsaspekte:
 Ende-zu-Ende-Verschlüsselung
 Schutz vor Man-in-the-Middle und Sniffing
 Unterstützung von Schlüsselbasierter Authentifizierung

 **Verbindung zu einem entfernten System:**
 *   **SSH-Schlüsselpaar erstellen:**
 ```bash
 ssh-keygen
 ```
  Typische Dateien:
  ```bash
  ~/.ssh/id_rsa        ← Privater Schlüssel  
  ~/.ssh/id_rsa.pub    ← Öffentlicher Schlüssel

  ```
  Öffentlichen Schlüssel auf den Server kopieren

  Einfachste Methode:

  ```bash
  ssh-copy-id user@host
  ```
  
 



