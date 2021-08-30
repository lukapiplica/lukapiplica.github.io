---
title: "Digitalna privatnost"
date: 2021-08-30 12:32:00 +0800
categories:
  - Privatnost
tags:
  - privatnost
  - digitalna privatnost
  - FSF
  - FOSS
---



<p align="center">
  <img width="100%" src="/assets/images/digitalnapriv/google.gif" />
</p>

<p align="center">
  <b>👋 Digitalna privatnost 👋</b>
</p>


## Uvod u digitalnu privatnost !


Već duže vrijeme znamo da velike kompanije kao Google i Facebook špiuniraju nad njihovim korisnicima. Svaku sliko što uslikate i spremite na Google Drive ili Google Fotografije, kao i objavite na društvene mreže ostaju zauvijek iako vi mislite da ste izbrisali te slike.

 Da li bi vama bilo neugodno da znate da vam netko ima pristup vašoj galeriji na telefonu i svim vašim podatcima uključujući poruke, geolokaciju itd. ? 


## Zašto je bitna digitalna privatnost ?

Digitalna privatnost je bitna jer time vi imate kontrolu nad **vašim** podatcima, a naravno tako i dobijate pravo na vaše mišljenje. Ovaj primjer možemo vidjeti sa Facebook-om koji je 2016. godine imao utjecaj na izborima, tako što je od određenog kandidata forsirao korisnicima reklame, samim time to je utjecalo na mišljenje mnogih korisnika. 

Relevantnost informacija, ako želite da saznate nešto novo ili da pročitate, vjerovtno će te potražiti informaciju na Google-u, a zatim ući u neku web stranicu. Nažalost mnogo stranica danas je prepuno informacija koje uopšte nisu potrebne (reklama). Najbolji primjer je ako želim da potražim recept na internetu, trebat će nekoliko sekundi da se ta stranica učita. Ako izmjerimo potrošimo otprilike 100 Mb na stranicu od kojih je 20 Mb relevantno (ono što sam pretražio). 

Sve ovo je povezano jer ove velike kompanije prodaju vaše podatke drugim-a i pomoću toga vi ste žrtva ciljanih reklama u smislu da ako nešto napišete vašem prijatelju preko Messenger-a, Viber-a, WhatsApp-a itd. dobivat ćete reklame o tome što ste napisali. 


## Kako poboljšati digitalnu privatnost ? 

Prvo se moramo zapitati na kojem nivou vi želite vašu privatnost ? Zatim nakon što to odlučimo, možemo započeti sa svim ostalim stvarima. Krenut ćemo od **računara i laptopa**.

## Digitalna privatnost na računarima i laptopima.

1. **Operativni sistem**:

   Kao što već znamo Windows sistemi su puni špiunaže i ne potrebnih aplikacija koje dođu nakon instalacije. MacOS sistemi su bili sasvim ok dok Apple nije uveo skeniranje vaše galerije na iCloud-u.

   **Trenutno najbolji operativni sistem za privatnost je GNU/Linux.**

   + [Ubuntu](https://ubuntu.com/) distribucija je veoma lagana za početnike, ali imajte u podsvjesti da su imali skandal prije nekoliko godina gdje su slali neke informacije Amazonu, ali trenutno možete tu opciju izgasiti u postavkama.

   + Ako prelazite sa Windows operativnog sistema, jako dobra distribucija je [Linux Mint](https://linuxmint.com/)

   + Ako želite privatnost na maximalnom nivou, onda imate opciju između [Artix GNU/Linux-a](https://artixlinux.org/) i [Debian GNU/Linux-a](https://www.debian.org/). Ova dva sistema su odlična, ali nisu preporučljiva novim korisnicima ! 

   + Ako želite maksimalnu privatnost i sigurnost, trenutno najbolji operativni sistem je [QubesOS](https://www.qubes-os.org/), ali problem Qubes-a je što ovaj sistem zahtjeva minimalno 32 GB RAM memorije kao i jači procesor, jer ovaj sistem je napravljen da sve što pokrenete, pokreće se u novoj virtualnoj mašini koja je izolovana od svega ostalog. Što se tiče privatnosti i sigurnosti sistem je bolji čak od gore navedenih, ali zahtjeva jak računar.  

   + [Whonix](https://www.whonix.org/) distribucija orijentisana ka privatnosti, a koristi TOR protokol.

   + [TailsOS](https://tails.boum.org/) sličan način rada kao Whonix samo što Tails je namijenjen da se koristi preko Live USB-a, što znači da se ne instalira. 

2. **Web preglednik**:

   + [Firefox](https://www.mozilla.org/en-US/firefox/new/?redirect_source=firefox-com) je jedan od najboljih web pretraživača za privatnost, potrebno je podesiti nekoliko postavkih za maksimalnu privatnost, možete kliknuti na [link](https://www.privacytools.io/browsers/#about_config) da vidite postavke.
   
   + [Tor Browser](https://www.torproject.org/) iako se Tor najviše koristi za ulazak u Deep Web, veoma je siguran što se tiče privatnosti. 

3. **Dodatci web preglednik**:

   + [uBlock Origin](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/) ovaj dodatak je "adblocker" i služi za blokiranje reklama. 

   + [HTTPS Everywhere](https://www.eff.org/https-everywhere) ovaj dodatak forsira sve web stranice da koriste HTTPS protokol. 

   + [ClearURLs](https://gitlab.com/KevinRoebert/ClearUrls) veoma koristan dodatak koji izvlači originalni link od skraćenih linkova (adfly, bitly itd.).

   + [Firefox Multi-Account Containers](https://support.mozilla.org/en-US/kb/containers) napravljen od firefox-a, a radi tako što svaku novu karticu otvori u posebnom izolovanom kontejneru.

4. **Pretraživači**:

   + [DuckDuckGo](https://duckduckgo.com) trenutno najbolji pretraživač orijentisan ka privatnosti.


## Digitalna privatnost na mobitelima.

Digitalnu privatnost na mobitelu je veoma teško postići jer su ovi uređaji napravljeni za špiuniranje korisnika. Postoje nekoliko Android ROM-ova koji su odlični za privatnost ali većina ih zahtjeva Google Pixel mobitel. **NAPOMENA**: Obratite pažnju na koji sistem birate i koje uređaje on podržava, kao i trebaju li vam Google aplikacije !

   1. **Android ROM-ovi**:

      + [CalyxOS](https://calyxos.org/) jako dobra zamjena za GrapheneOS, korisnicima kojima su potrebne Google Aplikacije jer ovaj sistem podržava microG servis koji je zamjena za Google Play servise, a microG šalje veoma malo podataka Google-u. **Podržava samo Google Pixel telefone.** 

      + [GrapheneOS](https://grapheneos.org/) najbolji sistem za privatnost i ne podržava microG servis što znači da ako vam je potrebna aplikcija sa Play Store-a ne možete je instalirati. **Podržava samo Google Pixel telefone.** 

      + [LineageOS](https://www.lineageos.org/) odličan sistem za privatnost, no pošto nakon otključavanja bootloader-a, ne može se zaključati što znači da ako vam netko ukrade telefon onda se sve informacije mogu izvući jer otključanim bootloader-om telefon gubi enkripciju. Prednost je što ovaj sistem podržava microG servis koji vi možete birati hoćete li ili ne, također **podržava mnogo više uređaja od Xiaomi-a do Samsung-a.**

   2. **Zamjena za Google Play Store**

      + [F-Droid](https://www.f-droid.org/) najbolja trgovina za skidanje aplikacija, a podržava samo FOSS (Free Open Source Software) aplikacije.

      + [Aurora Store](https://auroraoss.com/) također jedna od boljih trgovina za skidanje aplikacija. 

## Aplikacije orijetisane ka digitalnoj privatnosti.

Postoji mnogo aplikacija za privatnost, ja ću nabrojati nekoliko, a ostale možete provjeriti na [PrivacyToolsIO](https://www.privacytools.io/).

+ [Joplin](https://joplinapp.org/) aplikacija za note, i to-do liste

+ [KeePass](https://keepassxc.org/) password manager, aplikacija koja čuva vaše šifre, ne podržava Cloud Backup tako da manuelno morate praviti kopije nakon svake dodane šifre.

+ [Bitwarden](https://bitwarden.com/) password manager, koji podržava Cloud Backup.

+ [Signal](https://www.signal.org/) aplikacija za chat i pozive, **NAPOMENA** signal će uskoro promjeniti model zarade tako da postoji mogućnost da će krenuti prikupljati podatke, **XMPP i MATRIX(Element)** su zamjene za Signal ali ne podržavaju pozive.

+ [Nextcloud](https://nextcloud.com/) jako dobra alternativa za Google Photos i Google Drive, ali zahtjeva self hosting, što znači da morate imati računar sa većim hard diskom da sebi hostate NextCloud.

+ [Protonmail](https://protonmail.com/) alternativa za Gmail.

## Korisni linkovi

+ [r/privacy](https://www.reddit.com/r/privacy/)

+ [r/privacytoolsio](https://www.reddit.com/r/privacytoolsIO/)

+ [r/degoogle](https://www.reddit.com/r/degoogle/)

## Zaključak

Dosta aplikacija možete naći na F-droid marketu. Siguran je i za skoro sve postoji alternativa na njemu. Što se tiče mobitela mislim da je Google Pixel najbolje uzeti i instalirati GrapheneOS na njemu. Od računarskih sistema bilo koja Linux distribucija je dobra za početak ! 


### Hvala puno na vašem vremenu !

