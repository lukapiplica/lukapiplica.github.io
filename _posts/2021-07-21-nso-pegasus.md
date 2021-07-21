---
title: "NSO Pegasus Spyware"
date: 2021-07-21 18:46:00 +0800
categories:
  - Reaserch
tags:
  - Pegasus
  - NSO
  - Spyware
---


<p align="center">
  <img width="75%" src="/assets/images/pegasus/nso.png" />
</p>

<p align="center">
  <b>👋 NSO Pegasus Spyware 👋</b>
</p>


## Šta je to Pegasus Spyware ?


Tokom vikenda, procurila je vijest da su nekoliko autoritarnih vlada (uključujući Meksiko, Maroko i UAE) koristili softver za špijuniranje kojeg je razvila izraelska kompanija [NSO Group](https://en.wikipedia.org/wiki/NSO_Group). Njihov cilj je bila špijunaža nad političarima, aktivistima i novinarima. Popis od 50 000 telefonskih brojeva potencialno korištenih za špijunažu je dospio u vlasništvo pariške neprofitne organizacije [Forbidden Stories](https://forbiddenstories.org/) i [Amnesty International](https://www.amnesty.org/en/), koji su podijelili u javnost sa [The Washington Post](https://www.washingtonpost.com/) i [The Guardian](https://www.theguardian.com/international). 

Nakon što su cyber sigurnosni istraživači analizirali nekoliko telefona žrtava ovog napada, otkrili su da se radi o kompleksnom malware-u, koji može pristupiti svim podatcima na telefonu od poruka, telefonskih poziva do vaših fotografija, a najstrašnije od svega Pegasus omogućava snimanje razgovora, kao i pristup mikrofonu i kameri. Što znači da vas ovaj spyware može pratiti 24/7 h i snimati šta god govorite, radite, na kojoj ste lokaciji itd. 

Također ovaj spyware je napravljen i za **iOS** i **Android** operativne sisteme.

## Kako Pegasus radi ?

Pegasus radi pomoću tzv. "0-day exploits". To su vam greške u sistemu za koje skoro nitko ne zna, čak ni kompanije iza operativnih sistema, elektronike itd. Lakše objašnjenjo ni Apple ne zna da ove greške u kodu postoje, upravo zbog toga postoje "bug bounty" programi na koje se cyber sigurnosni istraživači prijave i traže ove greške u sistemu za koje budu novčano nagrađeni zavisno od utjecaja te greške na privatnost korisnika ili štete koju može donijeti kompaniji. Naravno ako cyber sigurnosni istraživači ne uspiju otkriti greške u kodu (bug-ove) prije hakera sa lošom namjerom to predstavlja problem i doprinosi razvoju raznih malicioznih softvera kao naprimjer Pegasus. Koliko je poznato dovoljno je da primite samo jedan poziv ili tekstualnu poruku (na koju ne morate ni kliknuti ni javiti se) da vaš iOS ili Android uređaj bude inficiran. 

## Kako izbrisati ovaj spyware sa vašeg mobilnog uređaja ? 

Trenutno ne postoji ni jedan način da bi se Pegasus uklonio sa vašeg mobilnog uređaja, ali najbolji savjet je da uvijek updejtate vaš operativni sistem mobilnog uređaja na najnoviju verziju. Zadnja poznata verzija iOS-a koja je ranjiva ovom metodom hakovanja je **iOS 14.6**.

## Kako detektovati Pegasus ?

Pegasus je teško detektovati nakon što je instaliran na vaš mobilni uređaj, a i napravljen je da se sam briše u slučaju da pogriješi broj telefona ili prepozna da uređaj nije aktivan više od 60 dana. Trenutno postoje nekoliko IOCs (Indicators of Compromise) koji su pronađeni, a možete ih pronaći na [AmnestyTech Github-u](https://github.com/AmnestyTech/investigations/tree/master/2021-07-18_nso).

## Kako uraditi digitalnu forenziku na vašem uređaju o Pegasus-u ?

Sada ću vam pokazati kako uraditi digitalnu forenziku na vašem uređaju, pomoću koje možete provjeriti da li ste vi inficirani ovim špijunskim softverom. 


Potrebno:

+ **Operativni sistem:** [Kali Linux](https://www.kali.org/)  
+ **Program:** [MVT (Mobile Verification Toolkit)](https://github.com/mvt-project/mvt)
+ **IOCs:** [AmnestyTech IOCs](https://github.com/AmnestyTech/investigations/tree/master/2021-07-18_nso)


## Uputstva

Prva stvar koju moramo uraditi nakon što instaliramo ili pokrenemo u virtualnoj mašini Kali Linux operativni sistem jeste updejt sistema. 

*U ovom primjeru ja koristim Kali Linux, ali bilo koja distirbucija bazirana na Debian Linux-u bi trebala raditi sa malim razlikama u komandama.*

1. Updejtovanje **Kali Linux-a**:

   Otvaramo terminal i kucamo sljedeće komande: 

   ```shell
   sudo apt update
   sudo apt upgrade
   ```

2. Instalacija **MVT-a**:

   Prvo moramo instalirati nekoliko "dependencies-a" koji su nam potrebni da bi MVT radio kako treba. 

   + Instalacija dependencies-a:

     ```shell 
     sudo apt install python3 python3-pip libusb-1.0-0 git 
     ```
     

   + Instalacija MVT-a:

     Nakon instalacije dependencies-a instaliramo MVT. Prvo ulazimo u Downloads direktoriju. 
    
     ```shell
     cd Downloads
     ```

     Zatim moramo skinuti MVT sa github-a, to radimo kucanjem ove komande u terminal:

     ```shell
     git clone https://github.com/mvt-project/mvt.git 
     ```
     Ulazimo u MVT direktoriju koju smo skinuli.

     ```shell
     cd mvt
     ```

     Instaliramo MVT pomoću ove komande:

     ```shell
     pip3 install . 
     ```
     
     Dodavanje PATH varijable: 

     ```shell
     export PATH=$PATH:/home/*USERNAME*/.local/bin
     ```
     Obratite pažnju na **USERNAME** to vi morate promijeniti u zavisnosti od korisničkog imena na Linux-u.


   + Skidanje **IOCs-a**: 

     Prvo ćemo promijeniti direktoriju u Downloads folder: 

     ```shell
     cd ~/Downloads 
     ```
     Zatim kloniramo repozitoriju:

     ```shell
     git clone https://github.com/AmnestyTech/investigations.git
     ```


## Digitalna forenzika na iOS uređajima.

Ako imate iOS (Apple) uređaj onda pratite sljedeće instrukcije, ako ne onda možete pronaći instrukcije za Android sisteme ispod **Digitalne forenzike na iOS uređajima**.


   + Kopija sistema vašeg uređaja:

     Prvi korak ovog procesa je da napravimo backup fajl operativnog sistema na mobitelu tako da ga možemo analizirati. Postoje dvije metode **Filesystem dump** i **iTunes Backup**. 

     **Filesystem dump** je metoda koja zahtjeva **jailbreak** iOS sistema koji možete uraditi pomoću [checkra1n-a](https://checkra.in/). Prednosti ove metode su te da možete uraditi "dump" čitavog sistema i pomoću toga možete izvući više podataka, ali nažalost jailbreak-ovanjem iPhone-a gubite garanciju, a neki iPhone uređaji na određenim iOS verzijama se ne mogu jailbrek-ovati. 

     **iTunes Backup** je alternativna opcija iako će izvući manje podataka opet zadržava garanciju vašeg uređaja. 

     **NAPOMENA:** iTunes Backup metodom možete izvući više podataka ako koristite enkriptovani backup. 
   

   + Backup (sigurnosna kopija) iOS-a pomoću **iTunes-a**:

      iTunes backup možete uraditi na uređaju sa Windows operativnim sistemom. Instrukcije: 

      + Instalirajte iTunes na vaš računar ili laptop.
      + Spojite iPhone pomoću kabla na vaš računar ili laptop.
      + Otvorite vaš iPhone u iTunes-u.
      + Ako želite bolje rezultate onda izaberite opciju za enkriptovanje sigurnosne kopije. 
      + Pokrenite sigurnosnu kopiju, ona može potrajati i do 30 minuta. 
      
      Nakon što sigurnosna kopija završi, njenu lokaciju na Windows 10 operativnim sistemima možete pronaći u jednom od dva foldera:

      + %USERPROFILE%\Apple\MobileSync\  
      + %USERPROFILE%\AppData\Roaming\Apple Computer\MobileSync\ 
      
      Najlakši način da ih pronađete je da u "Search" traku zalijepite %USERPROFILE% pa provjerite folder manuelno. Folder koji je bitan jeste folder sa **UDID-om** (folder imenovan 0000[REDACTED]).


   + Dekriptovanje sigurnosne kopije:

     Ako ste enkriptovali vašu sigurnosnu kopiju, prebacimo je na računar ili virtualnu mašinu sa Linux-om (u ovom primjeru ja ću fajl sa USB-a prebaciti u Documents folder), zatim moramo napraviti folder u koji ćemo dekriptovati:

     ```shell
     mkdir ~/Documents/dekriptovano
     ```
     Zatim dekriptujemo fajl:

      ```shell
      mvt-ios decrypt-backup -p 'VAŠA_ŠIFRA' -d ~/Documents/dekriptovano ~/Documents/0000[REDACTED]
      ```

     Ova komanda će potrajati dugo zavisno od težine kopije, nakon što se dekripcija završi, vrijeme je da napravimo output folder:

     ```shell
     mkdir ~/Downloads/output_forenzike
     ```

     Nakon toga ostaje nam samo jedna komanda koja će nam pomoću strix2 fajla skenirati i provjeriti da li je iPhone zaražen Pegasus-om ili ne. 

     ```shell
     mvt-ios check-backup -i ~/Downloads/investigations/2021-07-18_nso/pegasus.strix2 -o ~/Downloads/output_forenzike ~/Documents/dekriptovano
     ```


   <p align="center">
      <img width="100%" src="/assets/images/pegasus/screenshot.png" />
   </p>

## Digitalna forenzika na Android uređajima:

   Digitalna forenzika na Android uređajima je mnogo komplikovanija, MVT trenutno pruža dvije metode. 

   + Skidanjem APK fajlova koji su instalirani po redoslijedu i analiziranjem istih. 
   + Ekstraktovanje Android sigurnosne kopije i provjeravanje o sumnjivim SMS porukama.


   1. Provjera **APK** fajlova:

      Da bismo koristili MVT opciju **mvt-android** potrebno je da vaš Android uređaj bude spojen sa Linux-om. Morat će te uključiti USB debugging opciju na vašem telefonu.

      Zatim na prvoj konekciji morat će te potvrditi spajanje uređaja na Android-u, pa na Linux-u možemo napraviti output folder:

      ```shell
      mkdir ~/Downloads/output_forenzike
      ```

      Nakon toga možete pokrenuti sljedeću komandu:

      ```shell 
      mvt-android download-apks -o ~/Downloads/output_forenzike 
      ```

      Po vašoj želji možete izabrati gdje želite da pregledate SHA256 Hash-ove APK-ova koji su ekstraktovani na [VirusTotal](https://www.virustotal.com/gui/). Ovo može pomoći u identifikovanju malicioznih APK fajlova (aplikacija) na Android uređaju. To radimo komandom:

      ```shell
      mvt-android download-apks -o ~/Downloads/output_forenzike --virustotal
      ```

   2. Provjera malicioznih **SMS poruka**:

      Ova metoda koristi MVT da provjeri da li je vaš Android uređaj inficiran malicioznim SMS porukama. Pretpostavljam da ste već spojili vaš uređaj kao na instrukcijama za APK fajlove, sada pokrećemo ovu komandu:

      ```shell
      adb backup com.android.providers.telephony
      ```
      Moramo odobriti sigurnosnu kopiju na telefonu i potencijalno unijeti vašu lozinku sigurnosne kopije. Sigurnosna kopija tada će se pohraniti u folder nazvan **backup.ab**.

      Zatim moramo koristiti [Android Backup Extractor](https://github.com/nelenkov/android-backup-extractor) da prethodno dobiveni fajl pretvorimo u format koji se može čitati. Java mora biti instalirana na sistemu!

      Zatim pokrećemo sljedeće komande:

      ```shell
      java -jar ~/Downloads/abe.jar unpack backup.ab backup.tar
      tar xvf backup.tar
      ```
      Ako je sigurnosna kopija enkriptovana, Android Backup Extractor će vam tražiti šifru.

      Zatim MVT provjerava da li se maliciozni linkovi nalaze u SMS porukama, to radimo komandom: 

      ```shell
      mvt-android check-backup -o sms .
      ```
      Pomoću **--iocs** ili **-i** opcije možemo specificirati IOCs fajl. 


## Koje sve fajlove mvt-ios kreira, a zatim provjerava ?

Nakon što je MVT odradio svoju analizu, u terminalu će vam pisati Warning (suspicious file) ako je vaš uređaj zaražen sa Pegasus-om. Sada će te moći vidjeti koje sve fajlove je MVT kreirao i provjerio tokom analize. 

+ 💵 `[cache_files.json]`

  Ovaj JSON fajl kreira modul **CacheFiles**. Modul izdvaja zapise iz svih datoteka SQLite baze podataka spašenim na disku s imenom **Cache.db**. Te baze podataka obično sadrže podatke iz iOS Internal URL caching-a.

  Pomoću ovog modula možete vidjeti HTTP zahtjeve i odgovore. To je korisno jer ovim načinom možemo vidjeti HTTP zahtjeve koji su dio "exploitation chain-a", a rade tako što iOS servis pokušava da skine maliciozni fajl tokom prve faze ovog zahtjeva. 


+ 📱 `[calls.json]`

   Ovaj JSON fajl kreira modul **Calls**. Modul izdvaja zapise iz baze podataka SQLite koja se nalazi na `/private/var/mobile/Library/CallHistoryDB/CallHistory.storedata`, koja sadrži spisak svih dolaznih i odlaznih poziva, uključujući i aplikacije kao naprimjer WhatsApp ili Skype.

+ 💻 `[chrome_favicon.json]`

   Ovaj JSON fajl kreira **ChromeFavicon** modul. Modul izdvaja zapise iz baze podataka SQLite koja se nalazi na `/private/var/mobile/Containers/Data/Application/*/Library/Application Support/Google/Chrome/Default/Favicons`, a služi da spasi favikonice (male ikonice u tab-ovima vašeg web pretraživača) za brže učitavanje.

   Favikonice mogu biti hakovane, više o ovoj temi možete pogledati na [LINK](https://www.youtube.com/watch?v=X7OW5hTt5hY).  

+ 💻 `[chrome_history.json]`

   Ovaj JSON fajl kreira **ChromeHistory** modul. Modul izdvaja zapise iz baze podataka SQLite koja se nalazi na `/private/var/mobile/Containers/Data/Application/*/Library/Application Support/Google/Chrome/Default/History`, koja sadrži vašu historiju Google Chrome web pretraživača.


+ 🤓 `[contacts.json]` 

   Ovaj JSON fajl kreira **Contacts** modul. Modul izdvaja zapise iz SQLite baze podataka koja se nalazi na `/private/var/mobile/Library/AddressBook/AddressBook.sqlitedb`, koja sadrži spisak vaših kontakata.

+ 🦊 `[firefox_favicon.json]` 

   Ovaj JSON fajl  kreirao je **FirefoxFavicon** modul. Modul izdvaja zapise iz baze podataka SQLite koja se nalazi na `/private/var/mobile/profile.profile/browser.db`, a služi da spasi favikonice (male ikonice u tab-ovima vašeg web pretraživača) za brže učitavanje.


+ 🦊 `[firefox_history.json]` 

   Ovaj JSON fajl kreirao je **FirefoxHistory** modul. Modul izdvaja zapise iz baze podataka SQLite koja se nalazi na `/private/var/mobile/profile.profile/browser.db`, koja sadrži vašu historiju Firefox web pretraživača.


+ 📋 `[id_status_cache.json]` 

  Ovaj JSON fajl kreira **IDStatusCache** modul. Modul izvlači zapise iz datoteke plist koja se nalazi na `/private/var/mobile/Library/Preferences/com.apple.identityservices.idstatuscache.plist` koja spašava vaše uzorke Apple ID-a (to uključuje i biometrijske podatke kao Touch i Face ID).


+ 🤝 `[interaction_c.json]` 

   Ovaj JSON fajl kreira **InteractionC** modul. Modul izvlači zapise iz baze podataka SQLite koja se nalazi na `/private/var/mobile/Library/CoreDuet/People/interactionC.db`, a sadrži detalje o interakcijama korisnika s instaliranim aplikacijama.

+ 📍 `[locationd_clients.json]` 

   Ovaj JSON fajl kreira **LocationdClients** modul. Modul izdvaja zapise iz datoteke plist koja se nalazi na `/private/var/mobile/Library/Caches/locationd/clients.plist`, a ona sadrži keširanu memoriju aplikacija koje su zatražile pristup uslugama lokacije.

+ 🔷 `[manifest.json]` 

   Ovaj JSON fajl kreirao je **Manifest** modul. Modul izvlači zapise iz baze podataka SQLite **Manifest.db** koje pravi iTunes tokom sigurnosne kopije, a služi da govori lokalnoj sigurnosnoj kopiji gdje svi fajlovi se nalaze na iOS uređaju.

+ 💽 `[datausage.json]` 

   Ovaj JSON fajl kreira **Datausage** modul. Modul izdvaja zapise iz SQLite baze podataka koja se nalazi `/private/var/wireless/Library/Databases/DataUsage.sqlite`, a sadrži historiju upotrebe podataka od strane procesa koji se koriste na sistemu. 

+ 💻 `[safari_browser_state.json]` 

   Ovaj JSON fajl kreira **SafariBrowserState** modul. Modul izdvaja zapise iz SQLite baza podataka smještenih na `/private/var/mobile/Library/Safari/BrowserState.db` ili `/private/var/mobile/Containers/Data/Application/*/Library/Safari/BrowserState.db`, a sadrže spisak otvorenih kartica u Safari web pretraživaču.

+ 💻 `[safari_favicon.json]`

   Ovaj JSON fajl kreira **SafariFavicon** modul. Modul izdvaja zapise iz SQLite baza podataka smještenih na `/private/var/mobile/Library/Image Cache/Favicons/Favicons.db` ili `/private/var/mobile/Containers/Data/Application/*/Library/Image Cache/Favicons/Favicons.db`,  a služi da spasi favikonice (male ikonice u tab-ovima vašeg web pretraživača) za brže učitavanje.

+ 🔥 `[safari_history.json]`

   Ovaj JSON fajl kreira **SafariHistory** modul. Modul izdvaja zapise iz SQLite baza podataka smještenih na `/private/var/mobile/Library/Safari/History.db` ili `/private/var/mobile/Containers/Data/Application/*/Library/Safari/History.db`, koje sadrže historiju pretraživanja.

+ 📝 `[sms.json]` 

   Ovaj JSON fajl kreira **SMS** modul. Modul izdvaja popis SMS poruka koje sadrže HTTP linkove iz baze podataka SQLite koja se nalazi na `/private/var/mobile/Library/SMS/sms.db`.

+ 📝 `[sms_attachments.json]` 

   Ovaj JSON fajl kreira **SMSAttachments** modul. Modul izvlači detalje o privitcima koji se šalju SMS-om ili iMessage-om iz iste baze podataka koju koristi SMS modul.

+ 📜 `[version_history.json]`

   Ovaj JSON fajl kreira **IOSVersionHistory** modul. Modul izdvaja zapise o ažuriranjima iOS-a iz datoteka s popisom analitike koje se nalaze na `/private/var/db/analyticsd/Analytics-Journal-*.ips`.

+ 🕸️ `[webkit_indexeddb.json]` 

   Ovaj JSON fajl kreira **WebkitIndexedDB** modul. Modul izdvaja popis datoteka i mapa koji se nalaze u `/private/var/mobile/Containers/Data/Application/*/Library/WebKit/WebsiteData/IndexedDB`, a sadrži IndexedDB datoteke koje su stvorene od bilo koje aplikacije.


+ 🕸️ `[webkit_local_storage.json]` 

   Ovaj JSON fajl kreira **WebkitLocalStorage** modul. Modul ekstraktuje listu imena datoteka i mapa pronađenih u `/private/var/mobile/Containers/Data/Application/*/Library/WebKit/WebsiteData/LocalStorage/`, a sadrži datoteke sa interne pohrane stvorene bilo kojom aplikacijom.

+ 🕸️ `[webkit_safari_view_service.json]` 

   Ovaj JSON fajl kreira **WebkitSafariViewService** modul. Modul izdvaja popis imena datoteka i mapa pronađenih u `/private/var/mobile/Containers/Data/Application/*/SystemData/com.apple.SafariViewService/Library/WebKit/WebsiteData/`, a sadrži fajlove koji su keširani od strane SafariVewService.

+ 🕸️ `[webkit_session_resource_log.json]` 

   Ovaj JSON fajl kreira **WebkitSessionResourceLog** modul. Modul izvlači zapise iz plist datoteka s imenom **full_browsing_session_resourceLog.plist**, a sadrže zapise resursa učitanih od različitih posjećivanih web stranica.

+ 📞 `[whatsapp.json]`

   Ovaj JSON fajl kreirao je **WhatsApp** modul. Modul izdvaja popis WhatsApp poruka koje sadrže HTTP veze iz SQLite baze podataka koja se nalazi na `/private/var/mobile/Containers/Shared/AppGroup/*/ChatStorage.sqlite`.




## Zaključak

Pegasus je jedan od najopasnijih alata za špijunažu, ne slažem se sa postupcima NSO Group kompanije i mislim da svi imaju pravo na privatnost. Trenutno jedina zaštita protiv Pegasus-a bi bila možda telefon koji nije ni Android ni iOS. Dobra alternativa je Nokia 8110 4G sa [GerdaOS](https://gerda.tech/) operativnim sistemom. Personalno preporučujem da pogledate The Guardian-ov [interview](https://www.theguardian.com/news/2021/jul/19/edward-snowden-calls-spyware-trade-ban-pegasus-revelations) sa Edward Snowden-om o temi Pegasus-a.     


### Hvala puno na izdvojenom vremenu !

