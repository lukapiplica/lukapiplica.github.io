---
title: "HSKY Token"
date: 2022-01-22 17:42:00 +0800
categories:
  - Crypto
tags:
  - Solana
  - Crypto
  - HSKY
---


<p align="center">
  <img width="75%" src="/assets/images/hsky/btc.gif" />
</p>

<p align="center">
  <b>💸 HSKY Token 💸</b>
</p>


## Šta je to Crypto Token ?


Danas sve više ljudi koristi kriptovalute, neke od poznatih su Bitcoin, Dogecoin, Etherium, Solana itd. sve ove kriptovalute imaju svoj blockchain. Mi pravimo kripto token, on za razliku od ovih ostalih popularnih kriptovaluta koje imaju svoj blockchain, radi na blockchain-u drugih kriptovaluta. Specifično mi čemo koristiti Solanu zbog jeftine naknade koja se dešava prilikom prebacivanje ovog token-a i zbog brzine (Solana ima jako brz blockchain za razliku od ostalih).


## Šta je sve potrebno:

+ **Operativni sistem:** [Debian Linux](https://www.debian.org/)  
+ **Github profil** [Github](https://github.com)
+ **Kripto mjenjačnica** [Binance](https://www.binance.com/en)
+ **Phantom wallet** [PhantomWallet](https://phantom.app/)
+ **Solflare** [Solflare](https://solflare.com/)

**NAPOMENA: Potrebno je kupiti Solana-u !**


## Uputstva

Prva stvar koju moramo uraditi je napraviti neku virtualnu mašinu, a zatim instalirati Debian linux u CLI-u (bez grafičkog interfejsa). 

<p align="center">
  <img width="100%" src="/assets/images/hsky/1.png" />
</p>


<p align="center">
  <img width="100%" src="/assets/images/hsky/2.png" />
</p>

Nakon instalacije Debian-a prvu stvar što trebate je updejtovati sistem. 

## Updejtovanje **Debian-a**: 

   ```shell
   sudo apt update
   sudo apt upgrade
   ```

## Instalacija **Solaninog alata**:

     ```shell 
     sh -c "$(curl -sSfL https://release.solana.com/v1.8.5/install)"
     ```
     
    Zatim ukucati **exit** i ponovno se logovati u CLI.

## Pravljenje **Crypto Wallet-a**:

    ```shell
     solana-keygen new
    ```

    Pritisnuti enter dva puta i uspješno ste napravili wallet. 

    **NAPOMENA: PUBLIC KEY JE ZAPRAVO VAŠA WALLET ADRESA, A SEED PHRASE SAČUVAJTE NEGDJE U SLUČAJU DA IZGUBITE WALLET !**

<p align="center">
  <img width="100%" src="/assets/images/hsky/4.png" />
</p>

## Kupovina Solana-e.

Da bismo napravili naš token, moramo kupiti Solane. Moja preporuka je Binance.

<p align="center">
  <img width="100%" src="/assets/images/hsky/6.png" />
</p>

## Prebacivanje Solana-e:

Nakon što kupimo Solana-u, ona trenutno stoji na Binance-u. Moramo je prebaciti u wallet na virtualnoj mašini. 

**NAPOMENA: ADRESA NA KOJU ŠALJETE IZ BINANCE-A JE PUBLIC KEY KOJI SMO NAPRAVILI U VIRTUALNOJ MAŠINI !**

<p align="center">
  <img width="100%" src="/assets/images/hsky/7.png" />
</p>

Nakon što prebacimo Solana-u, da bi mogli vidjeti koliko imamo Solana-e u CLI kucamo:  

```shell
 solana balance
```

## Instalacija **Rust-a**:

```shell
 curl https://sh.rustup.rs -sSf | sh
```
Nakon što kliknemo enter, pritisnuti 1 za default instalaciju. 

<p align="center">
  <img width="100%" src="/assets/images/hsky/8.png" />
</p>

Ukucati **exit** i ponovno se prijaviti na virtualnu mašinu.

## Instalacija potrebnih paketa:

```shell
 sudo apt install libudev-dev libssl-dev pkg-config build-essential
```

## Instalacija **SPL-a**:

```shell
 cargo install spl-token-cli
```

## Pravljenje kripto token-a:

```shell
 spl-token create-token
```

## Pravljenje account-a koji će čuvati naš token. 

```shell
 spl-token create-account *TOKEN ID*
```
**NAPOMENA: TOKEN ID JE TOKEN ŠTO SMO DOBILI POKRETANJEM PROŠLE KOMANDE !**

<p align="center">
  <img width="100%" src="/assets/images/hsky/14.png" />
</p>

## Mintovanje token-a i dodavanje količine vašeg token-a.

```shell
 spl-token mint *PRVI TOKEN ID* *BROJ KOLIČINE (KOLIKO ŽELITE VAŠIH TOKEN-A UKUPNO)* *DRUGI TOKEN ID OD ACCOUNT-A*
```

<p align="center">
  <img width="100%" src="/assets/images/hsky/15.png" />
</p>

Uspješno ste napravili vaš token. 

## Prebacivanje Token-a drugima. 

Da bismo prebacili vaš token drugima, moraju prvo napraviti wallet ili na telefonu ili u webbrowser-u. Ako pravite wallet na telefonu onda Solflare je odličan wallet, a ako pravite wallet u web pretraživaču onda Phantom Wallet. 

```shell
 spl-token transfer --fund-recipient --allow-unfunded-recipient *PRVI TOKEN ID* *KOLIKO ŽELIMO POSLATI* *WALLET ADRESA NA KOJU ŠALJEMO*
```
<p align="center">
  <img width="100%" src="/assets/images/hsky/16.png" />
</p>

## [Solscan](https://solscan.io/) stranica

Da bi provjerili naš token, možemo zalijepiti prvi TOKEN ID na ovoj stranici. 

<p align="center">
  <img width="100%" src="/assets/images/hsky/17.png" />
</p>

## Dodavanje Token-a u Solana registry: 

+ Napraviti sliku za vaš token, mora biti manja od 200kb
+ Napraviti Github Account

+ Napraviti novu repozitoriju i prenijeti sliku vašeg token-a u taj repozitorij (imenovati je logo.png). 

<p align="center">
  <img width="100%" src="/assets/images/hsky/19.png" />
</p>

+ Otići na https://github.com/solana-labs/token-list i Fork-ovati.

<p align="center">
  <img width="100%" src="/assets/images/hsky/20.png" />
</p>

+ Pritisnuti . da bi se otvorio Visual Studio Code.

<p align="center">
  <img width="100%" src="/assets/images/hsky/21.png" />
</p>

+ Sa lijeve strane otići na **assets/mainnet** kliknuti desni klik i napraviti novi folder i zalijepiti Token adresu.

+ Desni klik na folder i kliknuti upload, zatim upload-ati sliku vašeg token-a.

+ Zatim sa lijeve strane otići u folder **src**, zatim u folder **tokens** i otvoriti **solana.tokenlist.json** fajl.

+ Otići na dno fajl-a i onda dodati vaš token u JSON formatu, najlakše je kopirati i zalijepiti informacije od token-a prije vašeg i onda samo promjeniti vrijednosti.

+ Na lijevoj strani ima ikonica sa tri kruga kliknuti na nju, a zatim dodati poruku o tome šta radimo i kliknuti na kvačicu.

+ Zatim vratiti se na Solanin github i ići na pull request.

+ Uraditi merge i sačekati da taj proces završi. Solana svakih sat vremena radi provjeru tako da moguće je da vaš pull request bude primljen tek nakon sat vremena. 

## Finalni produkt: 

<p align="center">
  <img width="100%" src="/assets/images/hsky/22.png" />
</p>

<p align="center">
  <img width="100%" src="/assets/images/hsky/23.png" />
</p>



## Zaključak

Zanimljiv projekat, mnogo toga se može naučiti pogotovo o kriptovalutama i kako one funkcionišu. Trenutno ovaj projekat nema nikakve primjene i nije pojekat na kojem se može zaraditi, ali znanje je dovoljno.    


### Hvala puno na izdvojenom vremenu !

