---
title: "So schützen Sie einen Linux-Server"
draft: false
date: 2022-10-09
description: "Eine Anleitung zum Schutz eines Linux-Servers" 
categories:
  - Linux
---



<p align="center">
  <img width="40%" src="1.webp" />
</p>

<p align="center">
  <b>🐧 So schützen Sie einen Linux-Server ! 🐧</b>
</p>

{{< alert >}}
**Hinweis**: Diese Seite wurde mit Hilfe von [DeepL](https://www.deepl.com/translator) und [Google Translate](https://translate.google.com/) ins Deutsche übersetzt.
{{< /alert >}}

Jeder weiß bereits, dass Sie einen Server schützen und sicherer machen sollten. Nun, hier sind einige grundlegende Schritte zum Schutz Ihrer Server. Fangen wir gleich an: 

Erstens würde ich dringend empfehlen, das **HTTPS**-Protokoll für Ihre Spiegel zu verwenden!

Ich gehe davon aus, dass Sie einen frisch installierten Linux-Server haben. Denken Sie daran, dass diese Befehle auf den **apt**-Paketmanager ausgerichtet sind, aber sie sollten auch mit anderen Paketmanagern mit kleinen Änderungen funktionieren. 

## Aktualisierung Ihres Servers

Nach einer Neuinstallation aktualisiere ich als erstes den Server manuell: 

 ```shell
 sudo apt update
 sudo apt upgrade
 ```

## Automatische Updates aktivieren

Nachdem ich meinen Server manuell aktualisiert habe, aktiviere ich normalerweise automatische Updates.

Denken Sie daran, je nachdem, wie kritisch der Server ist, möchten Sie möglicherweise nicht, dass Updates ihn beschädigen.

Um automatische Updates zu aktivieren, benötigen Sie ein Paket namens **unattended-upgrades** !

> ```shell
> sudo apt install unattended-upgrades
> ```

Dann müssen Sie es aktivieren: 

> ```shell
> sudo dpkg-reconfigure --priority=low unattended-upgrades
> ```

## Secure Shell (SSH)

### Vorbereitung

Normalerweise erfolgt die Verbindung zu Servern remote über das SSH-Protokoll auf dem **Standardport 22**.

Zuerst erstelle ich einen neuen Ordner mit dem Namen **.ssh**, falls er nicht im **/home**-Verzeichnis existiert. 

>    ```shell
>    mkdir ~/.ssh
>    ```

Dann vergeben wir die Ordnerberechtigungen von **700**, was eine Datei vor dem Zugriff anderer Benutzer schützt, während der ausstellende Benutzer noch vollen Zugriff hat.

>    ```shell
>    chmod 700 ~/.ssh
>    ```

Nun wollen wir uns von unserem Server abmelden, wenn wir per ssh verbunden sind.

>    ```shell    
>    logout
>    ```
    
### Generieren eines soliden Secure Shell-Schlüsselpaars

Lassen Sie uns nun ein öffentliches und ein privates Schlüsselpaar generieren, damit wir uns sicher mit dem Server verbinden können. Ich verwende den ed25519-Algorithmus, da er schnell ist und die Sicherheit nicht beeinträchtigt.

Ich würde auch empfehlen, eine Passphrase zu verwenden.

>- Windows Powershell: 
> ```shell
> ssh-keygen -t ed25519
> ```
>- Linux Terminal: 
> ```shell
> ssh-keygen -t ed25519
> ```
>- MacOS Terminal:
> ```shell
> ssh-keygen -t ed25519
> ```
  
Dadurch werden die privaten und öffentlichen Schlüssel in Ihrem home/.ssh-Ordner gespeichert, abhängig von Ihrem Betriebssystem, es könnte versteckt sein.

### Kopieren des öffentlichen Schlüssels auf den Server aus der Ferne

Nachdem die öffentlichen und privaten Schlüssel generiert wurden, müssen wir sie auf den Server übertragen. Ich werde **SCP** verwenden, um den Schlüssel auf den Server zu verschieben.

>- Windows Powershell:
> ```shell
> scp $env:USERPROFILE/.ssh/id_ed25519.pub SERVER_USER@SERVER_IP:~/.ssh/authorized_keys
> ``` 
>- Linux Terminal: 
> ```shell
> ssh-copy-id SERVER_USER@SERVER_IP
> ```
>- MacOS Terminal: 
> ```shell
> scp ~/.ssh/id_ed25519.pub SERVER_USER@SERVER_IP:~/.ssh/authorized_keys
> ```

### Passwortloser Fernzugriff und Ändern des Standardports

Jetzt müssen wir unser ssh sperren und Passwörter deaktivieren, damit Sie sich nur mit den generierten Schlüsselpaaren anmelden können. Wir melden uns bei unserem Server an und bearbeiten die ssh-Konfigurationsdatei.

Öffnen der Konfigurationsdatei:
        
> ```shell
> sudo nano /etc/ssh/sshd_config
> ```

Lassen Sie uns den standardmäßigen **Port** von **22** ändern. Kommentieren Sie die Zeile **Port** aus, löschen Sie die Nummer 22 und fügen Sie etwas nach Ihrem Geschmack hinzu.
    
**Verwenden Sie zum Beispiel höhere Zahlen wie 4723**. 

Jetzt können Sie in der Zeile **AddressFamily** angeben, ob Sie IPv4, IPv6 oder beides verwenden möchten. Ich deaktiviere IPv6, aber das musst du nicht. Wenn Sie nur IPv4 verwenden möchten, ersetzen Sie **any** durch **inet**

**Root-Anmeldung deaktivieren**, indem **PermitRootLogin yes** durch **PermitRootLogin no** ersetzt wird.

Deaktivieren Sie dann die Passwortauthentifizierung, indem Sie **PasswordAuthentication yes** durch **PasswordAuthentication no** ersetzen

Speichern Sie nun die Änderungen!

### Neustart von SSH, um Änderungen zu übernehmen

Nachdem wir Änderungen an der Konfigurationsdatei vorgenommen haben, müssen wir nun den ssh-Dienst neu starten. 

> ```shell
> sudo systemctl restart sshd
> ```

{{< alert >}}
**HINWEIS**: Stellen Sie sicher, dass Sie eine Verbindung haben, indem Sie versuchen, eine Verbindung von einem anderen Terminal/einer anderen Powershell herzustellen. Wenn Sie einen Fehler machen, können Sie sich aussperren!
{{< /alert >}}

## Firewall aktivieren

Überprüfen Sie zunächst Ihre verwendeten Ports, indem Sie:

> ```shell
> sudo ss -tupln
> ```

Möglicherweise haben Sie andere Ports verwendet, recherchieren Sie, aber ich werde ssh nur aktivieren, damit ich eine Verbindung zum Server herstellen kann.

Zuerst installieren wir ufw.

> ```shell
> sudo apt install ufw
> ```

Als Firewall verwende ich **ufw**. Denken Sie an den letzten Port, den wir in die Konfigurationsdatei von ssh eingefügt haben. Wir müssen es zulassen. Außerdem wird immer empfohlen, anzugeben, welches Protokoll der Port verwendet, entweder TCP oder UDP! 

> ```shell
> sudo ufw allow SSH_PORT/tcp
> ```

Dann müssen wir die Firewall aktivieren.

> ```shell
> sudo ufw enable
> ```

Um zu überprüfen, welche Regeln erlaubt sind, können wir Folgendes verwenden:

> ```shell
> sudo ufw status
> ```

## ICMP deaktivieren (ping)

Normalerweise ist der Befehl **ping** hilfreich für Netzwerkadministratoren und Hacker. Am besten deaktivieren Sie Ping!

Um Ping zu deaktivieren, müssen wir die ufw-Konfiguration bearbeiten.

> ```shell
> sudo nano /etc/ufw/before.rules 
> ```

Fügen Sie unter dem Abschnitt **ok icmp codes for INPUT** diese Zeile so ein, dass sie an erster Stelle steht (direkt unter ok icmp codes for INPUT).

> ```shell
> -A ufw-before-input -p icmp --icmp-type echo-request -j DROP
> ```

Starten Sie den Server neu:

> ```shell
> sudo reboot now
> ```

Ping wurde jetzt deaktiviert!

## Schlussfolgerung

Der nicht hackbare Server existiert nicht! Denken Sie daran, dass jeder Server hackbar ist, aber dies ist eine bewährte Methode, die Sie in Betracht ziehen sollten, um Ihren Server zu härten.

## Vielen Dank für Ihre Zeit 💙

