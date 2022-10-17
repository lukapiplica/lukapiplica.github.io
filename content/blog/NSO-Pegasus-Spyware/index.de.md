---
title: "NSO Pegasus Spyware"
date: 2021-07-21 
draft: false
description: "Informative Anleitung zu Pegasus und Methoden, um festzustellen, ob Sie sich infiziert haben"
categories:
  - Cybersecurity
  - Privacy
---


<p align="center">
  <img width="75%" src="nso.webp" />
</p>

<p align="center">
  <b>🔍 NSO Pegasus Spyware 🔍</b>
</p>

{{< alert >}}
**Hinweis**: Diese Seite wurde mit Hilfe von [DeepL](https://www.deepl.com/translator) und [Google Translate](https://translate.google.com/) ins Deutsche übersetzt.
{{< /alert >}}


## Was ist Pegasus-Spyware?


Am Wochenende sickerten Nachrichten durch, dass mehrere autoritäre Regierungen (darunter Mexiko, Marokko und die Vereinigten Arabischen Emirate) Spionagesoftware verwendeten, die von der israelischen Firma [NSO Group](https://en.wikipedia.org/wiki/NSO_Group) entwickelt wurde. Ihr Ziel war es, Politiker, Aktivisten und Journalisten auszuspionieren. Eine Liste mit 50.000 Telefonnummern, die möglicherweise für Spionagezwecke genutzt werden, ist in den Besitz der gemeinnützigen Pariser Organisation [Forbidden Stories](https://forbiddenstories.org/) und [Amnesty International](https://www.amnesty.org/en/), die sie mit der Öffentlichkeit [The Washington Post](https://www.washingtonpost.com/) und [The Guardian](https://www.theguardian.com/international) geteilt haben.

Nachdem Cybersicherheitsforscher mehrere Telefone von Opfern dieses Angriffs analysiert hatten, stellten sie fest, dass es sich um eine komplexe Malware handelt, die auf alle Daten auf dem Telefon zugreifen kann, von Nachrichten und Anrufen bis hin zu Ihren Fotos, und das Schlimmste ist, dass Pegasus es Ihnen ermöglicht nehmen Sie Gespräche auf und greifen Sie auf das Mikrofon und die Kamera zu. Dies bedeutet, dass diese Spyware Sie rund um die Uhr verfolgen und aufzeichnen kann, was Sie sagen, tun und wo Sie sich befinden.

Außerdem wurde diese Spyware sowohl für **iOS**- als auch für **Android**-Betriebssysteme entwickelt.

## Wie Pegasus funktioniert ?

Pegasus arbeitet mit dem sogenannten. "0-Day-Exploits". Dies sind Systemfehler, von denen fast niemand weiß, nicht einmal die Unternehmen hinter Betriebssystemen, Elektronik usw. Eine einfachere Erklärung ist, dass Apple nicht weiß, dass diese Fehler im Code vorhanden sind, weshalb es „Bug Bounty“ gibt "Programme, für die sich Cybersicherheitsforscher anmelden. Sie suchen nach Fehlern im System und werden je nach Auswirkung dieses Fehlers mit Geld belohnt. Nehmen wir natürlich an, Cybersicherheitsforscher erkennen Codefehler (Bugs) nicht vor Hackern mit bösen Absichten. In diesem Fall ist dies ein Problem und trägt zur Entwicklung verschiedener bösartiger Software wie Pegasus bei. Soweit wir wissen, reicht es aus, nur einen Anruf oder eine SMS zu erhalten (die Sie nicht anklicken oder beantworten müssen), um Ihr iOS- oder Android-Gerät zu infizieren.

## Wie lösche ich diese Spyware von Ihrem Mobilgerät?

Es gibt keine Möglichkeit, Pegasus von Ihrem mobilen Gerät zu entfernen, aber der beste Rat ist, Ihr mobiles Betriebssystem ständig auf die neueste Version zu aktualisieren. Die letzte bekannte Version von iOS, die für diese Hacking-Methode anfällig ist, ist **iOS 14.6**.

## Wie erkennt man Pegasus?

Pegasus ist schwer zu erkennen, nachdem es auf Ihrem Mobilgerät installiert wurde, und es ist so konzipiert, dass es von selbst gelöscht wird, falls es die falsche Telefonnummer erhält oder erkennt, dass das Gerät länger als 60 Tage nicht aktiv war. Derzeit wurden mehrere IOCs (Indicators of Compromise) gefunden, die Sie auf [AmnestyTech Github](https://github.com/AmnestyTech/investigations/tree/master/2021-07-18_nso) finden können.

## Wie führen Sie digitale Forensik auf Ihrem Gerät durch?

Jetzt zeige ich Ihnen, wie Sie digitale Forensik auf Ihrem Gerät durchführen, mit der Sie überprüfen können, ob Sie mit dieser Spyware infiziert sind.


Erforderlich:

>+ **Betriebssystem:** [Kali Linux](https://www.kali.org/)  
>+ **Programm:** [MVT (Mobile Verification Toolkit)](https://github.com/mvt-project/mvt)
>+ **IOCs:** [AmnestyTech IOCs](https://github.com/AmnestyTech/investigations/tree/master/2021-07-18_nso)


## Anweisungen

Nach der Installation oder dem Booten des Betriebssystems Kali Linux in der virtuellen Maschine müssen wir als erstes das Systemupdate durchführen.

*In diesem Beispiel verwende ich Kali Linux, aber jede auf Debian Linux basierende Distribution sollte mit geringfügigen Unterschieden in den Befehlen funktionieren.*

### Aktualisieren von Kali Linux

Wir öffnen das Terminal und geben die folgenden Befehle ein:

> ```shell
> sudo apt update
> sudo apt upgrade
> ```

### Installation von MVT

Wir müssen zuerst ein paar "Abhängigkeiten" installieren, damit das MVT richtig funktioniert.

+ Installation von Abhängigkeiten:

> ```shell 
> sudo apt install python3 python3-pip libusb-1.0-0 git 
> ```
     

+ Installation von MVT:

   Nach der Installation der Abhängigkeiten installieren wir das MVT. Zuerst betreten wir das Downloads-Verzeichnis.
    
> ```shell
> cd Downloads
> ```

+ Dann müssen wir MVT von GitHub herunterladen:

> ```shell
> git clone https://github.com/mvt-project/mvt.git 
> ```

+ Wir betreten nun das heruntergeladene MVT-Verzeichnis:

> ```shell
> cd mvt
> ```

+ Wir installieren MVT jetzt mit diesem Befehl:

> ```shell
> pip3 install . 
> ```
     
+ Hinzufügen einer PATH-Variablen:

> ```shell
> export PATH=$PATH:/home/*USERNAME*/.local/bin
> ```

{{< alert >}}
**Hinweis**: BENUTZERNAME müssen Sie abhängig vom Benutzernamen unter Linux ändern.
{{< /alert >}}

### Herunterladen von IOCs

+ Wir werden zuerst das Verzeichnis im Ordner Downloads ändern:

> ```shell
> cd ~/Downloads 
> ```
     
+ Dann klonen wir das Repository:

> ```shell
> git clone https://github.com/AmnestyTech/investigations.git
> ```


## Digitale Forensik auf iOS-Geräten.

Wenn Sie ein iOS-Gerät (Apple) haben, befolgen Sie die nachstehenden Anweisungen; Falls nicht, finden Sie Anleitungen für Android-Systeme unter **Digitale Forensik auf Android-Geräten**.


### Eine Kopie des Systems Ihres Geräts

Der erste Schritt in diesem Prozess besteht darin, die Betriebssystemdatei auf dem Mobiltelefon zu sichern, damit wir sie analysieren können. Es gibt zwei Methoden **Dateisystem-Dump** und **iTunes-Sicherung**.

**Dateisystem-Dump** ist eine Methode, die einen **Jailbreak** eines iOS-Systems erfordert, das Sie mit [checkra1n](https://checkra.in/) ausführen können. Die Vorteile dieser Methode bestehen darin, dass Sie das gesamte System "dumpen" und damit weitere Daten extrahieren können, aber leider verliert das Jailbreaking des iPhone die Garantie und einige iPhones mit bestimmten iOS-Versionen können nicht jailbreakt werden.

**iTunes Backup** ist eine alternative Option, obwohl dadurch weniger Daten erneut extrahiert werden und die Garantie Ihres Geräts erhalten bleibt.

{{< alert >}}
**HINWEIS:** Sie können mehr Daten mit der iTunes-Sicherungsmethode extrahieren, wenn Sie eine verschlüsselte Sicherung verwenden.
{{< /alert >}}   

### Backup von iOS mit iTunes

Sie können iTunes auf einem Windows-Gerät sichern. Anweisungen:

>+ Installieren Sie iTunes auf Ihrem Computer oder Laptop.
>+ Verbinden Sie das iPhone mit einem Kabel mit Ihrem Computer oder Laptop.
>+ Öffnen Sie Ihr iPhone in iTunes.
>+ Wenn Sie bessere Ergebnisse erzielen möchten, wählen Sie die verschlüsselte Backup-Option.
>+ Führen Sie eine Sicherung durch; es kann bis zu 30 Minuten dauern.
      
Sobald die Sicherung abgeschlossen ist, finden Sie ihren Speicherort auf Windows 10-Betriebssystemen in einem von zwei Ordnern:

>+ %USERPROFILE%\Apple\MobileSync\  
>+ %USERPROFILE%\AppData\Roaming\Apple Computer\MobileSync\ 
      
Der einfachste Weg, sie zu finden, besteht darin, %USERPROFILE% in die Suchleiste einzufügen und den Ordner manuell zu überprüfen. Der wichtige Ordner ist der Ordner mit **UDID** (ein Ordner namens 0000 [ZENSIERT]).

### Sicherungskopie entschlüsseln:

Wenn Sie Ihr Backup verschlüsselt haben, übertragen wir es auf einen Computer oder eine virtuelle Maschine mit Linux (in diesem Beispiel verschiebe ich die Datei von USB in den Ordner „Dokumente“). dann müssen wir einen Ordner zum Entschlüsseln erstellen:

> ```shell
> mkdir ~/Documents/decrypted
> ```

Jetzt entschlüsseln wir die Datei:

> ```shell
> mvt-ios decrypt-backup -p 'IHR_PASSWORT' -d ~/Documents/decrypted ~/Documents/0000[REDACTED]
> ```

Dieser Befehl dauert je nach Gewicht der Kopie sehr lange. Sobald die Entschlüsselung abgeschlossen ist, ist es an der Zeit, einen Ausgabeordner zu erstellen:

> ```shell
> mkdir ~/Downloads/output_forensics
> ```

Danach bleibt uns nur noch ein Befehl, der einen Scan mit einer strix2-Datei durchführt und prüft, ob das iPhone mit Pegasus infiziert ist oder nicht.

> ```shell
> mvt-ios check-backup -i ~/Downloads/investigations/2021-07-18_nso/pegasus.strix2 -o ~/Downloads/output_forensics ~/Documents/decrypted
> ```

   <p align="center">
      <img width="100%" src="1.webp" />
   </p>

## Digitale Forensik auf Android-Geräten

Die digitale Forensik auf Android-Geräten ist viel komplizierter; MVT bietet derzeit zwei Methoden an.

>+ Durch Herunterladen und Analysieren der installierten APK-Dateien.
>+ Durch Extrahieren von Android-Backups und Suchen nach verdächtigen SMS-Nachrichten.


### Überprüfung der APK-Datei

Um die MVT-Option **mvt-android** zu verwenden, muss Ihr Android-Gerät mit Linux verbunden sein. Sie müssen die USB-Debugging-Option auf Ihrem Telefon aktivieren.

Dann müssen Sie bei der ersten Verbindung die Verbindung des Geräts auf Android bestätigen, damit wir unter Linux einen Ausgabeordner erstellen können:

> ```shell
> mkdir ~/Downloads/output_forensics
> ```

Sie können dann den folgenden Befehl ausführen:

> ```shell 
> mvt-android download-apks -o ~/Downloads/output_forensics 
> ```

Sie können auswählen, wo Sie die auf [VirusTotal](https://www.virustotal.com/gui/) extrahierten SHA256-Hash-APKs anzeigen möchten. Dies kann dabei helfen, bösartige APK-Dateien (Anwendungen) auf Ihrem Android-Gerät zu identifizieren. Das machen wir mit dem Befehl:

> ```shell
> mvt-android download-apks -o ~/Downloads/output_forensics --virustotal
> ```

### Prüfung auf schädliche SMS-Nachrichten

Diese Methode verwendet das MVT, um zu überprüfen, ob Ihr Android-Gerät mit bösartigen SMS infiziert ist. Ich gehe davon aus, dass Sie Ihr Gerät bereits wie in den Anweisungen für APK-Dateien verbunden haben. Jetzt führen wir diesen Befehl aus:

> ```shell
> adb backup com.android.providers.telephony
> ```

Wir müssen das Backup auf Ihrem Telefon genehmigen und möglicherweise Ihr Backup-Passwort eingeben. Das Backup wird dann in einem Ordner namens **backup.ab** gespeichert.

Dann müssen wir [Android Backup Extractor](https://github.com/nelenkov/android-backup-extractor) verwenden, um die zuvor erhaltene Datei in ein lesbares Format zu konvertieren. Java muss auf dem System installiert sein!

Führen Sie dann die folgenden Befehle aus:

> ```shell
> java -jar ~/Downloads/abe.jar unpack backup.ab backup.tar
> tar xvf backup.tar
> ```

Android Backup Extractor fragt Sie nach dem Passwort, wenn das Backup verschlüsselt ist.

Dann prüft MVT, ob in SMS-Nachrichten bösartige Links enthalten sind; wir machen es mit dem Befehl:

> ```shell
> mvt-android check-backup -o sms .
> ```
  
Mit den Optionen **--iocs** oder **--i** können wir die IOCs-Datei spezifizieren. 

## Welche Dateien erstellt und prüft mvt-ios dann?

Nachdem das MVT die Analyse abgeschlossen hat, schreibt Ihnen das Terminal eine Warnung (verdächtige Datei), wenn Ihr Gerät mit Pegasus infiziert ist. Sie sehen nun alle Dateien, die MVT erstellt und während der Analyse überprüft hat.

+ 💵 `[cache_files.json]`

  Diese JSON-Datei erstellt das **CacheFiles**-Modul. Das Modul extrahiert Datensätze aus allen SQLite-Datenbankdateien, die auf einer Festplatte mit dem Namen **Cache.db** gespeichert sind. Diese Datenbanken enthalten normalerweise Daten aus dem internen iOS-URL-Caching.

    Sie können dieses Modul verwenden, um HTTP-Anforderungen und -Antworten anzuzeigen. Dies ist nützlich, da wir HTTP-Anforderungen sehen können, die Teil der „Ausbeutungskette“ sind und vom iOS-Dienst ausgeführt werden, der versucht, während der ersten Phase dieser Anforderung eine bösartige Datei herunterzuladen.


+ 📱 `[calls.json]`

   Diese JSON-Datei erstellt das **Calls**-Modul. Das Modul extrahiert Datensätze aus der SQLite-Datenbank, die sich unter `/private/var/mobile/Library/CallHistoryDB/CallHistory.store` befindet. Daten enthalten eine Liste aller eingehenden und ausgehenden Anrufe, einschließlich Anwendungen wie WhatsApp oder Skype.

+ 💻 `[chrome_favicon.json]`

  Diese JSON-Datei erstellt das **ChromeFavicon**-Modul. Das Modul extrahiert Datensätze aus der SQLite-Datenbank, die sich auf `/private/var/mobile/Containers/Data/Application/*/Library/Application Support/Google/Chrome/Default/Favicons` befindet, und dient dazu, Favicons (kleine Symbole in Ihrer Webbrowser-Tabs) für schnelleres Laden.

   Favicons können gehackt werden; Weitere Informationen zu diesem Thema finden Sie unter [LINK](https://www.youtube.com/watch?v=X7OW5hTt5hY).

+ 💻 `[chrome_history.json]`

   Diese JSON-Datei erstellt das **ChromeHistory**-Modul. Das Modul extrahiert Datensätze aus der SQLite-Datenbank unter `„/private/var/mobile/Containers/Data/Application/*/Library/Application Support/Google/Chrome/Default/History`, die den Verlauf Ihres Google Chrome-Webbrowsers enthält.


+ 🤓 `[contacts.json]` 

   Diese JSON-Datei erstellt das Modul ** Kontakte **. Das Modul extrahiert Datensätze aus der SQLite-Datenbank unter `/private/var/mobile/Library/AddressBook/AddressBook.sqlitedb`, die eine Liste Ihrer Kontakte enthält.

+ 🦊 `[firefox_favicon.json]` 

   Das Modul **FirefoxFavicon** hat diese JSON-Datei erstellt. Das Modul extrahiert Datensätze aus der SQLite-Datenbank, die sich auf `/private/var/mobile/profile.profile/browser.db` befindet, und dient dazu, Favicons (kleine Symbole in den Registerkarten Ihres Webbrowsers) zum schnelleren Laden zu speichern.


+ 🦊 `[firefox_history.json]` 

   Das Modul **FirefoxHistory** hat diese JSON-Datei erstellt. Das Modul extrahiert Datensätze aus der SQLite-Datenbank unter `/private/var/mobile/profile.profile/browser.db` und enthält den Verlauf Ihres Firefox-Webbrowsers.


+ 📋 `[id_status_cache.json]` 

  Diese JSON-Datei erstellt das **IDStatusCache**-Modul. Das Modul extrahiert Datensätze aus der Plist-Datei unter `/private/var/mobile/Library/Preferences/com.apple.identityservices.idstatuscache.plist`, die Ihre Apple-ID-Muster speichert (dies umfasst biometrische Daten wie Touch- und Face-ID).


+ 🤝 `[interaction_c.json]` 

   Diese JSON-Datei erstellt das **InteractionC**-Modul. Das Modul extrahiert Datensätze aus der SQLite-Datenbank unter `/private/var/mobile/Library/CoreDuet/People/interactionC.db` und enthält Details zu Benutzerinteraktionen mit installierten Anwendungen.

+ 📍 `[locationd_clients.json]` 

   Diese JSON-Datei erstellt das **LocationdClients**-Modul. Das Modul extrahiert Datensätze aus der Plist-Datei, die sich unter `/private/var/mobile/Library/Caches/location/clients.plist` befindet, und enthält zwischengespeicherten Speicher von Anwendungen, die Zugriff auf Ortungsdienste angefordert haben.

+ 🔷 `[manifest.json]` 

   Das Modul **Manifest** hat diese JSON-Datei erstellt. Das Modul extrahiert Datensätze aus der SQLite-Datenbank **Manifest.db**, die von iTunes während des Backups erstellt wurde, und dient dazu, dem lokalen Backup mitzuteilen, wo sich alle Dateien auf dem iOS-Gerät befinden.

+ 💽 `[datausage.json]` 

   Diese JSON-Datei erstellt das **Datausage**-Modul. Das Modul extrahiert Datensätze aus der SQLite-Datenbank, die sich in `/private/var/wireless/Library/Databases/DataUsage.sqlite` befindet. Es enthält den Verlauf der Datennutzung durch die auf dem System verwendeten Prozesse.

+ 💻 `[safari_browser_state.json]` 

   Diese JSON-Datei erstellt das **SafariBrowserState**-Modul. Das Modul extrahiert Datensätze aus SQLite-Datenbanken, die sich auf `/private/var/mobile/Library/Safari/BrowserState.db` oder `/private/var/mobile/Containers/Data/Application/*/Library/Safari/BrowserState.db` befinden , und enthalten eine Liste der geöffneten Registerkarten im Safari-Webbrowser.

+ 💻 `[safari_favicon.json]`

   Diese JSON-Datei erstellt das **SafariFavicon**-Modul. Das Modul extrahiert Datensätze aus SQLite-Datenbanken, die sich auf `/private/var/mobile/Library/Image Cache/Favicons/Favicons.db` oder `/private/var/mobile/Containers/Data/Application/*/Library/Image Cache/ befinden. Favicons/Favicons.db` und dient zum Speichern von Favicons (kleine Symbole in den Registerkarten Ihres Webbrowsers) zum schnelleren Laden.

+ 🔥 `[safari_history.json]`

   Diese JSON-Datei erstellt das **SafariHistory**-Modul. Das Modul extrahiert Datensätze aus SQLite-Datenbanken, die sich auf `/private/var/mobile/Library/Safari/History.db` oder `/private/var/mobile/Containers/Data/Application/*/Library/Safari/History.db` befinden , die den Suchverlauf enthalten.

+ 📝 `[sms.json]` 

   Diese JSON-Datei erstellt ein **SMS**-Modul. Das Modul extrahiert eine Liste von SMS-Nachrichten mit HTTP-Links aus der SQLite-Datenbank unter `/private/var/mobile/Library/SMS/sms.db`.

+ 📝 `[sms_attachments.json]` 

   Diese JSON-Datei erstellt das **SMSAttachments**-Modul. Das Modul extrahiert Details zu per SMS oder iMessage gesendeten Anhängen aus derselben Datenbank, die auch vom SMS-Modul verwendet wird.

+ 📜 `[version_history.json]`

   Diese JSON-Datei erstellt das **IOSVersionHistory**-Modul. Das Modul extrahiert iOS-Update-Datensätze aus den Analyselistendateien, die sich unter `/private/var/db/analyticsd/Analytics-Journal-*.Ips` befinden.

+ 🕸️ `[webkit_indexeddb.json]` 

   Diese JSON-Datei erstellt das **WebkitIndexedDB**-Modul. Das Modul extrahiert eine Liste von Dateien und Ordnern, die sich in `/private/var/mobile/Containers/Data/Application/*/Library/WebKit/WebsiteData/IndexedDB` befinden, und enthält IndexedDB-Dateien, die von einer beliebigen Anwendung erstellt wurden.

+ 🕸️ `[webkit_local_storage.json]` 

   Diese JSON-Datei erstellt das **WebkitLocalStorage**-Modul. Das Modul extrahiert eine Liste von Datei- und Ordnernamen, die in `/private/var/mobile/Containers/Data/Application/*/Library/WebKit/WebsiteData/LocalStorage/` gefunden werden, und enthält Dateien aus dem internen Speicher, die von einer beliebigen Anwendung erstellt wurden.

+ 🕸️ `[webkit_safari_view_service.json]` 

   Diese JSON-Datei erstellt das **WebkitSafariViewService**-Modul. Das Modul extrahiert eine Liste von Datei- und Ordnernamen, die in `/private/var/mobile/Containers/Data/Application/*/SystemData/com.apple.SafariViewService/Library/WebKit/WebsiteData/` gefunden werden, und enthält Dateien, die von SafariVewService zwischengespeichert werden .

+ 🕸️ `[webkit_session_resource_log.json]` 

   Diese JSON-Datei erstellt das **WebkitSessionResourceLog**-Modul. Das Modul extrahiert Datensätze aus Plist-Dateien mit dem Namen **full_browsing_session_resourceLog.plist** und enthält Ressourcendatensätze, die von verschiedenen besuchten Webseiten geladen wurden.

+ 📞 `[whatsapp.json]`

   Diese JSON-Datei wurde vom **WhatsApp**-Modul erstellt. Das Modul extrahiert eine Liste von WhatsApp-Nachrichten, die HTTP-Verbindungen enthalten, aus der SQLite-Datenbank, die sich unter `/private/var/mobile/Containers/Shared/AppGroup/*/ChatStorage.sqlite` befindet.




## Schlussfolgerung

Pegasus ist eines der gefährlichsten Werkzeuge für Spionage, ich bin mit den Aktionen des Unternehmens der NSO Group nicht einverstanden, und ich denke, jeder hat das Recht auf Privatsphäre. Derzeit könnte der einzige Schutz gegen Pegasus ein Telefon sein, das weder Android noch iOS ist. Eine gute Alternative ist das Nokia 8110 4G mit dem Betriebssystem [GerdaOS](https://gerda.tech/). Ich empfehle, sich das [Interview](https://www.theguardian.com/news/2021/jul/19/edward-snowden-calls-spyware-trade-ban-pegasus-revelations) von The Guardian mit Edward Snowden zum Thema anzusehen Pegasus.

## Danke für deine Zeit 💙

