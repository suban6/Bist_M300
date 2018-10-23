Toolumgebung aufsetzen
======

Dieses Repository behandelt die Installation von GitHub, VirtualBox, SSH, Vagrant und Visual Studio Code.

#### Einleitung
Diese Dokumentation wurde von mir mit der Unterstützung des Klassenkameraden und des Google erstellt.

#### Voraussetzungen
***
1. macOS High Sierra
2. GitHub Account
3. Git-OSX-Installer
4. VirtualBox
5. Vagrant
6. Visual Studio Code

### Git-Konto erstellen
***

Auf www.github.com ein Benutzerkonto erstellen (Angabe von Username, E-Mail und Passwort)

### Repository erstellen
***
1. Anmelden unter www.github.com 
2. Innerhalb der Willkommens-Seite auf Start a project klicken
3. Unter Repository name einen Name definieren (z.B. Bist_M300)
4. Haken bei Initialize this repository with a README.md setzen
5. Auf repository klicken

### SSH-Key erstellen (lokal)
***
1.  Terminal öffnen
2.  Folgenden Befehl mit der Account-E-Mail von GitHub einfügen:
    ```Shell
      $  ssh-keygen -t rsa -b 4096 -C "beispiel@beispiel.com"
    ```
3. Neuer SSH-Key wird erstellt:
    ```Shell
      Generating public/private rsa key pair.
    ```
4. Bei der Abfrage, unter welchem Namen der Schlüssel gespeichert werden soll, die Enter-Taste drücken (für Standard):
    ```Shell
      Enter a file in which to save the key (~/.ssh/id_rsa): [Press enter]
    ```
5. Nun kann ein Passwort für den Key festgelegt werden. Ich empfehle dieses zu setzen und anschliessend dem SSH-Agent zu hinterlegen, sodass keine erneute Eingabe (z.B. beim Pushen) notwendig ist:
    ```Shell
      Enter passphrase (empty for no passphrase): [Passwort]
      Enter same passphrase again: [Passwort wiederholen]
    ```

### SSH-Key dem SSH-Agent hinzufügen
***
1.  Terminal öffnen
2.  SSH-Agent starten:
    ```Shell
      $ eval "$(ssh-agent -s)"
      Agent pid 931
    ```
3.  Ab Version macOS High Sierra 10.12.2 muss das `~/.ssh/config` File angepasst werden, damit SSH-Keys automatisch dem SSH-Agent hinzugefügt werden:
    ```Shell
      $ sudo nano ~/.ssh/config
      
      Host *
      AddKeysToAgent yes
      UseKeychain yes
      IdentityFile ~/.ssh/id_rsa
    ```
4.  Nun muss der Schlüssel dem Agent nur noch hinzugefügt werden:
    ```Shell
      $ ssh-add -K ~/.ssh/id_rsa
    ```
5.  Der SSH-Key muss nun nur noch kopiert und anschliessend dem GitHub-Account hinzugefüg werden (siehe "SSH-Key hinzufügen"):
    ```Shell
      $ pbcopy < ~/.ssh/id_rsa.pub
      # Kopiert den Inhalt der id_rsa.pub Datei in die Zwischenablage
    ``` 

### Client installieren
***
1. Für die Client-Installation muss der Installer unter [dieser Webseite](http://sourceforge.net/projects/git-osx-installer/ "sourceforge.net/projects/git-osx-installer") heruntergeladen werden (Version 2.15.0)

2. Die Installation erfolgt GUI-basiert, jedoch standard (ohne speziellen Anpassungen). Daher wird an dieser Stelle auf eine Erklärung verzichtet.

3. Sobald der Vorgang abgeschlossen wurde, kann mit der Konfiguration fortgefahren werden.


### Client konfigurieren
***
1. Terminal öffnen
2. Git konfigurieren mit Informationen des GitHub-Accounts:
    ```Shell
      $ git config --global user.name "<username>"
      $ git config --global user.email "<e-mail>"
    ``` 
3. Konfiguration abgeschlossen


### Repository klonen
***
1. Zu Testzwecken soll ein Repository geklont werden. Dazu sind folgende Befehle notwendig:
2. Terminal öffnen
3. Repository klonen: 
    ```Shell
      $ git clone https://github.com/mc-b/devops
    ``` 
4. In das devops-Verzeichnis wechseln:
    ```Shell
      $ cd devops
    ``` 
5. Repository aktualisieren und Status anzeigen:
    ```Shell
      $ git pull

      Already up to date.

      $ git status

      Your branch is up to date with 'origin/master'.
    ``` 
6. Die Statusmeldung soll dabei mitteilen, dass das lokale Repository mit dem Originalen übereinstimmt.

### Repository herunterladen & aktualisieren (clone/pull)
***
1. Terminal öffnen
2. Ordner für Repository im gewünschten Verzeichnis erstellen:
    ```Shell
      $ cd Wohin\auch\immer
      $ mkdir MeinLokalesRepository
    ``` 
3. Repository mit SSH klonen (siehe Webseite des Repositorys unter "Clone or download"):
    ```Shell
      $ git clone git@github.com:suban6/Bist_M300.git

      Cloning into 'M300'...
    ``` 
4. Repository aktualisieren und Status anzeigen:
    ```Shell
      $ git pull

      Already up to date.
    ```

### Repository hochladen (Push)
***
1.  Terminal öffnen (nachdem Teile bzw. Dateien des lokalen Repositorys geändert wurden)
2.  In das entsprechende Verzeichnis des Repository gehen: 
    ```Shell
      $ cd Pfad\zu\meinem\Repository  
    ```  
3.  Dateien dem Upload hinzufügen:
    ```Shell
      $ git add -a.
    ``` 
4.  Den Upload commiten:
    ```Shell
      $ git commit -m "Mein Kommentar"
    ``` 
5.  Schliesslich den Upload pushen:
    ```Shell
      $ git push
    ```
6.  Nun sollte der Master-Branch des Repositorys ebenfalls aktualisiert sein


VirtualBox
======

### Software herunterladen & installieren
***
1. Zuerst muss die VirtualBox-Anwendung installiert werden. Der Installer lässt sich [hier](https://www.virtualbox.org"virtualbox.org") herunterladen.
2. Auf "Download VirtualBox 5.2" klicken und bei Abschnitt "VirtualBox 5.2.19 platform packages" dem OS X hosts Link folgen (Datei wird heruntergeladen)
3. Die Installation erfolgt GUI-basiert, jedoch standard (ohne speziellen Anpassungen). Daher wird an dieser Stelle auf eine Erklärung verzichtet.
4. Sobald der Vorgang abgeschlossen wurde, kann mit dem Herunterladen der ISO-Datei und der VM-Erstellung fortgefahren werden.

### ISO-Datei herunterladen
***
Für das weitere Vorgehen wird eine System-Abbild-Datei benötigt. Dazu laden wir in unserem Fall das Image von Ubuntu Desktop 16.04.05 herunter. Wie das genau funktioniert, wird nachfolgend beschrieben:

1. Das Systemabbild (ISO-Image) über [diesen Link](http://releases.ubuntu.com/16.04/ubuntu-16.04.5-desktop-amd64.iso.torrent"ubuntu.com") herunterladen
2. Datei im gewünschten Verzeichnis ablegen (damit das Image wiederverwendet werden kann)
3. Allen Anweisung in Abschnitt "VM erstellen" folgen

### VM erstellen
***
1. VirtualBox starten
2. Links oben, innerhalb der Anwendung, auf `Neu` klicken
3. Im neuen Fenster folgende Informationen eintragen:
   *  Name:           `Ilamaran_M300_Ubuntu_16.04_Desktop`
   *  Typ:            `Linux`
   *  Version:        `Ubuntu (64-bit)`
   *  Speichergrösse: `8182 MB`
   *  Platte:         `[X] Festplatte erzeugen`
4. Auf `Erzeugen` klicken
5. Weiteres Fenster öffnet sich, folgende Informationen eintragen:
   *  Dateipfad:                       standard
   *  Dateigrösse:                     `40.00 GB`
   *  Dateityp der Festplatte:         `VMDK (Virtual Maschine Disk)`
   *  Storage on physical hard disk:   `dynamisch alloziert`
6. Ebenefalls auf `Erzeugen` klicken, dann im Hauptmenü die VM anwählen (blau markiert) und den Punkt `Ändern` aufrufen
7. Im Abschnitt `Massenspeicher` den SATA-Controller anwählen und auf das CD+Symbol klicken
8. Unter `Medium auswählen` das zuvor heruntergeladene Systemabbild (ISO-Datei) anwählen
9. Alle Änderungen speichern und die VM starten
10. Den Installationsanweisungen der OS-Installation folgen und anschliessend zu Abschnitt "VM einrichten" gehen

### VM einrichten
***
Die virtuelle Maschine (VM) sollte nun soweit betriebsbereit sein, sprich der Zugriff auf den Home-Desktop ist möglich. 

1. Ubuntu-VM starten
2. Anmelden und Terminal öffnen
3. Paketliste neu einlesen und Pakete aktualisieren:
   ```Shell 
   $  sudo apt-get update   #Paketlisten des Paketmanagement-Systems "APT" neu einlesem
   
   $  sudo apt-get update   #Installierte Pakete wenn möglich auf verbesserte Versionen aktualisieren

   $  sudo reboot           #System-Neustart durchführen
   ```
4. Software Controlcenter "Synaptic" installieren:
   ```Shell 
   $  sudo apt-get install synaptic
   ```
5. Nach erfolgreicher Installation in der Suche nach "Synaptic Package Manager" suchen und diesen starten
6. Innerhalb des Managers nach "apache" (Webserver-Programm) suchen und dieses (inkl. aller Abhängigkeiten) installieren
7. System-Neustart durchführen:
   ```Shell 
   $  sudo reboot
   ```
8. Gängiger Web-Browser (z.B. Firefox) starten und prüfen, ob der Standard-Content des Webservers unter "http://127.0.0.01:80" (localhost) erreichbar ist
9. Browser-Fenster schliessen und VM wieder herunterfahren/stoppen
10. Mit dem Kapitel 4 (Vagrant) fortfahren

04 - Vagrant
======

### Software herunteladen & installieren
***
1. Die Anwendung in der Vagrant kann auf der [offiziellen Webseite](https://www.vagrantup.com/ "vagrantup.com") heruntergeladen werden.
2. Die Installation erfolgt, wie alle anderen Anwendungen, GUI-basiert, jedoch standard (ohne speziellen Anpassungen). Daher wird an dieser Stelle ebenfalls auf eine Erklärung verzichtet.
3. Sobald der Vorgang abgeschlossen wurde, kann mit dem Erstellen einer VM fortgefahren werden. 


05 - Visual Studio Code
======

### Software herunteladen & installieren
***
1. Unter [dieser Webseite](https://code.visualstudio.com/"visualstudio.com") lässt sich der Installer herunterladen.
2. Auf "Download for Mac" klicken und warten, bis das Fenster zum Herunterladen erscheint. Anschliesend den Download des Installers starten.
3. Die Installation erfolgt auch hier GUI-basiert. Wiederum aber standard (ohne speziellen Anpassungen), sodass an dieser Stelle auf eine Erklärung ebenfalls verzichtet wird .
4. Sobald der Vorgang abgeschlossen wurde, kann mit dem Herunterladen der ISO-Datei und der VM-Erstellung fortgefahren werden.

### Extensions installieren
***

Wir fügen dem Editor drei wichtige Extensions hinzu:

* Markdown All in One (Version 1.6.0 / von Yu Zhang)
* Vagrant Extension (Version 0.5.0 / von Marco Stanzi)
* vscode-pdf Extension (Version 0.3.0 / von tomiko1207)

Dazu müssen folgende Anweisungen befolgt werden: 

1. Visual Studio Code öffnen
2. Die Tastenkombination `CTRL` + `SHIFT` + `X` drücken und in der Sucheleiste die erwähnten Extensions suchen
3. Auf `Install` klicken und anschliessend auf `Reload`, um die Extension in den Arbeitsbereich zu laden.
4. Nun können die Extensions angewendet werden. Für Markdown ist [diese Liste](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet/"github.com") sehr hilfreich.


### Einstellungen anpassen
***
Damit keine Dateien der virtuellen Maschinen dem Cloud-Repository hinzugefügt werden (da Dateien zu gross), müssen diese in den Einstellungen "exkludiert" werden:

1. Visual Studio Code öffnen
2. Unter `Code` > `Preferences` > `Settings` bei den 3 Punkten (...) auf `Open setting.json` klicken
3. Zu diesem Abschnitt gehen:
     ```
      // Configure glob patterns for excluding files and folders. For example, the files 
      explorer decides which files and folders to show or hide based on this setting. 
      Read more about glob patterns here. (...)
    ``` 
4. Nachstehenden Code einfügen:
     ```
      // Konfiguriert die Globmuster zum Ausschließen von Dateien und Ordnern.
      "files.exclude": {
        "**/.git": true,
        "**/.svn": true,
        "**/.hg": true,
        "**/.vagrant": true,
        "**/.DS_Store": true
      },
    ```
5. Änderungen speichern und die Einstellungen schliessen
   
