Toolumgebung (10)
======

Dieses Repository behandelt die Installation von GitHub, VirtualBox, Vagrant und Visual Studio Code.

#### Einleitung

Die nachstehende Dokumentation wurde von Ilamaran Palanivetpillai im Rahmen des Moduls M300 (Plattformübergreifende Dienste in ein Netzwerk integrieren) erarbeitet.

#### Voraussetzungen
***
1. macOS High Sierra
2. GitHub Account
3. Git-OSX-Installer
4. VirtualBox
5. Vagrant
6. Visual Studio Code

### Konto erstellen
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
