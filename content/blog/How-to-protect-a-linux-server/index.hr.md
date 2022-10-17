---
title: "Kako zaštititi Linux poslužitelja"
draft: false
date: 2022-10-09
description: "Vodič o tome kako zaštititi Linux poslužitelja" 
categories:
  - Linux
---



<p align="center">
  <img width="40%" src="1.webp" />
</p>

<p align="center">
  <b>🐧 Kako zaštititi Linux poslužitelja ! 🐧</b>
</p>


Svi već znaju da biste trebali zaštititi poslužitelja i učiniti ga sigurnijim. Pa, evo nekih osnovnih koraka koje treba poduzeti kako biste zaštitili svoje poslužitelje. Prijeđimo odmah na to:

Kao prvo, toplo bih preporučio korištenje **HTTPS** protokola za vaš mirror!

Pretpostavit ću da imate svježu instalaciju Linux poslužitelja, imajte na umu da su ove naredbe usmjerene na **apt** upravitelja paketa, ali bi trebale raditi s drugim upraviteljima paketa uz manje izmjene.

## Ažuriranje vašeg poslužitelja 

Nakon nove instalacije, prvo što radim je ručno ažurirati poslužitelj:

 ```shell
 sudo apt update
 sudo apt upgrade
 ```

## Omogućivanje automatskog ažuriranja

Nakon ručnog ažuriranja poslužitelja, obično omogućim automatska ažuriranja.

Imajte na umu da, ovisno o tome koliko je poslužitelj kritičan, možda nećete htjeti da ga ažuriranja pokvare.

Da biste omogućili automatsko ažuriranje, potreban vam je paket koji se zove **unattended-upgrades**!

> ```shell
> sudo apt install unattended-upgrades
> ```

Zatim ga morate omogućiti:

> ```shell
> sudo dpkg-reconfigure --priority=low unattended-upgrades
> ```

## Secure Shell (SSH)

### Priprema

Obično se povezivanje s poslužiteljima obavlja daljinski putem preko SSH protokola na **zadanom portu 22**.

Prvo ću napraviti novu mapu ako ne postoji u **/home** direktoriju pod nazivom **.ssh**.

>    ```shell
>    mkdir ~/.ssh
>    ```

Zatim ćemo mapi dati dopuštenja od **700**, što štiti datoteku od pristupa drugih korisnika dok korisnik koji izdaje i dalje ima puni pristup.

>    ```shell
>    chmod 700 ~/.ssh
>    ```

Sada se želimo odjaviti s našeg poslužitelja ako smo povezani putem ssh-a.

>    ```shell    
>    logout
>    ```
    
### Generiranje čvrstog para ključeva Secure Shell-a

Generirajmo sada par javnih i privatnih ključeva kako bismo se mogli sigurno spojiti na poslužitelj. Koristim algoritam ed25519 jer je brz i ne ugrožava sigurnost.

Također bih preporučio korištenje zaporke.

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
  
Ovo će pohraniti privatne i javne ključeve u vašu home/.ssh mapu, ovisno o vašem OS-u, možda će biti skriveni.

### Kopiranje javnog ključa na poslužitelja preko remote-a

Nakon što su javni i privatni ključ generirani, potrebno ih je prenijeti na poslužitelja. Koristit ću **SCP** za premještanje ključa na poslužitelja.

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

### Daljinski pristup bez lozinke i promjena zadanog porta

Sada moramo zaključati naš ssh i onemogućiti lozinke tako da se možete prijaviti samo s generiranim parovima ključeva. Prijavit ćemo se na našeg poslužitelja i urediti ssh konfiguracijsku datoteku.

Otvaranje konfiguracijske datoteke:
        
> ```shell
> sudo nano /etc/ssh/sshd_config
> ```

Promijenimo zadani **port** od **22**. Odkomentirajte liniju **Port**, obrišite broj 22 i stavite nešto po svom ukusu.
    
**Koristite veće brojeve kao što je 4723, na primjer**. 

Sada u retku **AddressFamily** možete odrediti želite li koristiti IPv4, IPv6 ili oboje. Onemogućio sam IPv6, ali vi ne morate. Ako odlučite koristiti samo IPv4, zamijenite **any** s **inet**

**Onemogućite root prijavu** zamjenom **PermitRootLogin yes** u **PermitRootLogin no**.

Zatim onemogućite provjeru autentičnosti lozinke zamjenom **PasswordAuthentication yes** s **PasswordAuthentication no**

Sada spremite promjene!

### Ponovno pokretanje SSH-a za primjenu promjena

Nakon što smo unijeli promjene u konfiguracijsku datoteku, sada moramo ponovno pokrenuti ssh uslugu.

> ```shell
> sudo systemctl restart sshd
> ```

{{< alert >}}
**NAPOMENA**: Provjerite imate li vezu tako da se pokušate spojiti s drugog terminala/powershell-a. Ako pogriješite, možete se zaključati!
{{< /alert >}}

## Omogućavanje vatrozida

Najprije provjerite svoje korištene portove tako što ćete:

> ```shell
> sudo ss -tupln
> ```

Možda koristite druge portove, istražite, ali ja ću omogućiti samo ssh da se mogu spojiti na poslužitelja.

Prvo, instalirajmo ufw.

> ```shell
> sudo apt install ufw
> ```

Koristit ću **ufw** kao svoj firewall. Zapamtite posljednji port koji smo stavili u konfiguracijsku datoteku ssh-a. Moramo to dopustiti. Također, uvijek je preporučljivo navesti koji protokol port koristi, TCP ili UDP!

> ```shell
> sudo ufw allow SSH_PORT/tcp
> ```

Zatim moramo omogućiti vatrozid.

> ```shell
> sudo ufw enable
> ```

Kako bismo provjerili koja su pravila dopuštena, možemo koristiti sljedeće:

> ```shell
> sudo ufw status
> ```

## Onemogući ICMP (ping)

Obično je naredba **ping** korisna mrežnim administratorima i hakerima. Najbolja praksa je onemogućiti ping!

Da bismo onemogućili ping, moramo urediti ufw konfiguraciju. 

> ```shell
> sudo nano /etc/ufw/before.rules 
> ```

Pod odjeljkom pod nazivom **ok icmp codes for INPUT**, zalijepite ovaj redak tako da bude prvi (odmah ispod ok icmp codes for INPUT).

> ```shell
> -A ufw-before-input -p icmp --icmp-type echo-request -j DROP
> ```

Ponovno pokrenite poslužitelja:

> ```shell
> sudo reboot now
> ```

Ping je sada onemogućen!

## Zaključak

Poslužitelj koji se ne može hakirati ne postoji! Imajte na umu da je svaki poslužitelj moguće hakirati, ali ovo je dobra praksa koju biste trebali razmisliti o pokušaju da ojačate svog poslužitelja.

## Hvala na vašem vremenu 💙

