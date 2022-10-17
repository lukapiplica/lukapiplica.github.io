---
title: "[BSPWM] Pop OS Nordic"
date: 2021-07-19
draft: false
description: "Prilagodba Pop OS-a s nordijskom temom."
categories: 
  - Linux
---


<p align="center">
  <img width="75%" src="computer.webp" />
</p>

<p align="center">
  <b>🖥️ Pop! Linux konfiguracijske datoteke 🖥️</b>
</p>


<img src="1.webp" alt="img" align="center" width="400px">

Ovo su moje trenutne dot datoteke Pop! Linux distribuciju.

Instalacija će vam pomoći da stvorite isti izgled kao na slikama; ovdje su upute korak po korak.

Specifikacije sustava:

>+ **OS**: [Pop!_OS](https://pop.system76.com/) 
>+ **WM**: [BSPWM](https://github.com/baskerville/bspwm) 
>+ **Daemon tastature**: [Sxhkd](https://github.com/baskerville/sxhkd)
>+ **Bar**: [Polybar](https://github.com/polybar/polybar)
>+ **Kompozitor**: [Picom](https://github.com/ibhagwan/picom)
>+ **Pokretač aplikacija**: [Rofi](https://github.com/davatorium/rofi)
>+ **Terminal**: [Alacritty](https://github.com/alacritty/alacritty)
>+ **Shell**: [Oh-my-ZSH](https://ohmyz.sh/)
>+ **Shell tema**: [Powerlevel10k](https://github.com/romkatv/powerlevel10k)
>+ **Uređivač teksta**: [Vim-Airline](https://github.com/vim-airline/vim-airline)
>+ **Zaključani zaslon**: Slim and Slimlock
>+ **Notifikacije**: [Dunst](https://dunst-project.org/)
>+ **GTK tema**: [Nordic_Dark](https://www.gnome-look.org/p/1267246/)
>+ **Icon tema**: [Flatery_Dark](https://www.gnome-look.org/s/Gnome/p/1332404)
>+ **Cursor tema**: [Oreo_Blue](https://www.gnome-look.org/s/Gnome/p/1360254/)
>+ **Font**: [Source_Code_Pro](https://fonts.google.com/specimen/Source+Code+Pro)
>+ **Preglednik**: [Firefox](https://www.mozilla.org/en-US/firefox/new/)
>+ **Tema preglednika**: [Minimal_Functional_Fox](https://github.com/mut-ex/minimal-functional-fox)

## Instalacija

Za početak izrade ovog izgleda, pretpostavljam da imate svježe instaliran Pop! OS.

*Ako vas zanima što aplikacija radi, Wikipedia će vam pomoći.*

### Nadogradnja repozitorija i nadogradnja sustava

> ```shell
> sudo apt update
> sudo apt upgrade
> ```

### Instalacija BSPWM Tiling Window Manager

Prvo moramo instalirati nekoliko potrebnih paketa koji su nam potrebni za nastavak instalacije.

+ Instalacija potrebnih paketa:

>```shell 
> sudo apt install build-essential git vim xcb libxcb-util0-dev libxcb-ewmh-dev libxcb-randr0-dev libxcb-icccm4-dev libxcb-keysyms1-dev libxcb-xinerama0-dev libasound2-dev libxcb-xtest0-dev libxcb-shape0-dev
> ```
     

+ Kloniranje repozitorija:

> ```shell
> cd ~/Downloads
> git clone https://github.com/baskerville/bspwm.git
> ```

+ Kompajliranje i instaliranje BSPWM-a:

> ```shell
> cd bspwm
> make
> sudo make install
> ```
 
+ Kopirajte BSPWM konfiguracijske datoteke:

> ```shell
> mkdir ~/.config/bspwm
> cp examples/bspwmrc ~/.config/bspwm
> chmod +x ~/.config/bspwm/bspwmrc
> cd ..
> ``` 

### Instalacija daemon-a tipkovnice

Na primjer, moramo koristiti takozvani daemon tipkovnice za korištenje tipkovničkih prečaca za otvaranje terminala, drugih aplikacije itd. To je proces koji se izvodi u pozadini i daje upute BSPWM Tilling Window Manageru što učiniti ako netko pritisne određeni prečac na tipkovnici.

*Ako vas zanima što prečac radi prema mojim postavkama, dio prečaca će vam pomoći.*

+ Kloniranje repozitorija:

> ```shell
> cd ~/Downloads
> git clone https://github.com/baskerville/sxhkd.git
> ```

+ Kompajliranje i instaliranje sxhkd-a:
      
> ```shell
> cd sxhkd
> make 
> sudo make install
> ```

+ Kopirajte sxhkd konfiguracijske datoteke:

> ```shell
> mkdir ~/.config/sxhkd
> cp ../bspwm/examples/sxhkdrc ~/.config/sxhkd
> cd ..
> ```

{{< alert >}}
**NAPOMENA:** Ako mijenjate bilo što u datoteci sxhkdrc, obratite pozornost na koji terminal ste postavljeni; ako koristite obični Pop OS! terminal, trebate promijeniti OS u `gnome-terminal` pod emulatorom terminala.
{{< /alert >}}

### Instalacija Polybar-a

+ Instalacija potrebnih paketa: 

> ```shell
> sudo apt install cmake cmake-data pkg-config python3-sphinx libcairo2-dev libxcb1-dev libxcb-util0-dev libxcb-randr0-dev libxcb-composite0-dev python3-xcbgen xcb-proto libxcb-image0-dev libxcb-ewmh-dev libxcb-icccm4-dev libxcb-xkb-dev libxcb-xrm-dev libxcb-cursor-dev libasound2-dev libpulse-dev libjsoncpp-dev libmpdclient-dev libcurl4-openssl-dev libnl-genl-3-dev
> ```

+ Kloniranje repozitorija: 

> ```shell
> cd ~/Downloads
> git clone --recursive https://github.com/polybar/polybar
> ```

+ Kompajliranje i instalacija Polybar-a:

> ```shell
> cd polybar
> mkdir build
> cd build
> cmake ..
> make -j$(nproc)
> sudo make install
> ```

### Instalacija Picom-a

+ Instalacija potrebnih paketa:
   
> ```shell
> sudo apt install meson libxext-dev libxcb1-dev libxcb-damage0-dev libxcb-xfixes0-dev libxcb-shape0-dev libxcb-render-util0-dev libxcb-render0-dev libxcb-randr0-dev libxcb-composite0-dev libxcb-image0-dev libxcb-present-dev libxcb-xinerama0-dev libpixman-1-dev libdbus-1-dev libconfig-dev libgl1-mesa-dev  libpcre2-dev  libevdev-dev uthash-dev libev-dev libx11-xcb-dev
> ```

+ Kloniranje repozitorija: 

> ```shell
> cd ~/Downloads
> git clone https://github.com/ibhagwan/picom.git
> ```

+ Izrada Picom-a s Ninja-om:

> ```shell
> cd picom
> git submodule update --init --recursive
> meson --buildtype=release . build
> ninja -C build
> ```

+ Instalacija Picom kompozitora: 

> ```shell 
> sudo ninja -C build install
> cd ..
> ```

### Instalacija Rofi-a

> ```shell
> sudo apt install rofi
> ```

### Instalacija Alacritty terminala

> ```shell
> sudo apt install alacritty
> ```

+ Kloniranje repozitorije:

> ```shell
> cd ~/Downloads
> git clone https://github.com/lukapiplica/dots.git
> ```

+ Postavljanje Alacritty teme: 

> ```shell
> mkdir ~/.config/alacritty
> cp dots/alacritty/alacritty.yml ~/.config/alacritty/
> ```

{{< alert >}}
**NAPOMENA**: Ako dobijete pogrešku: `GLSL 3.30 not supported`, učinite ovo:
{{< /alert >}}
    
> ```shell
> nano /usr/share/applications/com.alacritty.Alacritty.desktop
> ```

*Promijenite `Exec=alacritty` u `Exec=bash -c "LIBGL_ALWAYS_SOFTWARE=1 alacritty"`.*

{{< alert >}}
**NAPOMENA:** Nakon ovog koraka, spremni ste za prijavu na BSPWM; prvo se morate odjaviti s trenutnog sučelja radne površine; zatim kliknite na ikonu ⚙️ u donjem desnom kutu i odaberite BSPWM.
{{< /alert >}}

### Instalacija fontova

> ```shell
> cd ~/Downloads
> cd dots
> sudo cp -r Source_Code_Pro /usr/share/fonts
> fc-cache -v
> ```

### Postavljanje pozadinske slike

+ Instalacija **Feh-a**
   
> ```shell
> sudo apt install feh
> ```

+ Premještanje pozadinskih slika :

> ```shell
> mkdir ~/Wall
> cp -r ~/Downloads/dots/Wallpapers/ ~/Wall
> ```

+ Postavljanje pozadinske slike:

> ```shell
> echo 'feh --bg-fill $HOME/Downloads/dots/Wallpapers/wallpaper2.jpeg' >> ~/.config/bspwm/bspwmrc 
> ```

### Konfiguracija Polybar-a

> ```shell
> mkdir ~/.config/polybar
> cd ~/Downloads/dots/polybar
> cp * -r ~/.config/polybar
> echo '~/.config/polybar/./launch.sh' >> ~/.config/bspwm/bspwmrc
> cd fonts
> sudo cp * /usr/share/fonts/truetype/
> ```

### Instalacija Oh-My-ZSH-a 

> ```shell
> sudo apt install zsh
> sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)
> ```

### Instalacija Powerlevel10k-a

+ Kloniranje repozitorija: 

> ```shell
> git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
> ```

+ Nakon kloniranja, moramo postaviti ovu temu u datoteku `~/.zshrc`; to radimo upisivanjem u datoteku `.zshrc` ovom naredbom `ZSH_THEME="powerlevel10k/powerlevel10k"`

+ Upisujemo u terminal:

> ```shell 
> p10k configure
> ```

Slijedimo upute na terminalu da napravimo temu koju želimo.

### Instalacija Vim teme

> ```shell
> mkdir -p ~/.vim/colors
> cd ~/Downloads
> cp dots/nord.vim ~/.vim/colors
> ```

+ Kloniranje Vim Airline repozitorije: 

> ```shell
> cd ~/Downloads
> git clone https://github.com/vim-airline/vim-airline.git
> cd vim-airline
> cp * -r ~/.vim
> echo 'colorscheme nord' >> ~/.vimrc
> echo 'let g:airline_theme='base16'' >> ~/.vimrc
> ```

### Postavljanje rofi teme

> ```shell 
> mkdir -p ~/.config/rofi/themes
> cp ~/Downloads/dots/nord.rasi ~/.config/rofi/themes
> rofi-theme-selector
> ```

+ Rofi Theme Selector pokazat će nam neke od tema. Za odabir naše teme idite na `Nord theme` kliknite **Enter**, a zatim da biste je postavili zauvijek, pritisnite **Alt + a**

> ```shell 
> nano ~/.config/sxhkd/sxhkdrc
> ```

+ Otvara uređivač nano teksta u terminalu i moramo promijeniti **`dmenu`** u **`rofi -show drun`**

### Instalacija Slim-a i Slimlock-a

> ```shell
> sudo apt instll slim libpam0g-dev libxrandr-dev libfreetype6-dev libimlib2-dev libxft-dev
> sudo dpkg-reconfigure gdm3 
> ```

{{< alert >}}      
**Napomena**: Ako dobijemo izbornik, moramo odabrati Slim kao opciju.
{{< /alert >}}

+ Za postavljanje teme:

> ```shell
> cd ~/Downloads/dots
> sudo cp slim.conf /etc && sudo cp slimlock.conf /etc
> sudo cp default /usr/share/slim/themes
> ```

## Razni programi

Uspješno smo postigli izgled ovog operativnog sustava; sada instaliramo nekoliko programa sa slika.

### Instalacija tty-clock-a

> ```shell
> sudo apt-get install tty-clock
> ```

### Instalacija CAVA Audio Visualizer

> ```shell
> sudo add-apt-repository ppa:hsheth2/ppa
> sudo apt-get update
> sudo apt-get install cava
> ```

### Instalacija htop-a

> ```shell
> sudo apt-get install htop
> ```

### Instalacija cmatrix-a

> ```shell
> sudo apt-get install cmatrix
> ```

### Instalacija sxiv-a

> ```shell
> sudo apt-get install sxiv
> ```

### Instalacija Ranger-a

> ```shell
> sudo apt-get install ranger
> ```

### Instalacija pfetch-a

> ```shell
> cd ~/Downloads
> git clone https://github.com/dylanaraps/pfetch.git
> sudo install pfetch/pfetch /usr/local/bin/
> ls -l /usr/local/bin/pfetch
> ```

### Instalacija chafa-e

> ```shell
> cd ~/Downloads
> git clone https://github.com/hpjansson/chafa.git
> cd chafa
> ./autogen.sh
> make 
> sudo make install
> ```

### Instalacija igre zmije
      
> ```shell 
> sudo apt install python3-pip
> python3 -m pip install -U pygame --user
> cd ~/Downloads
> git clone https://github.com/Unixado/Snake.git
> cd Snake
> python src/game.py
> ```

### Instalacija of lollypop

> ```shell
> sudo add-apt-repository ppa:gnumdk/lollypop
> sudo apt install lollypop
> ```

### Instalacija Minimal Functional Fox-a

> ```shell
> sh -c "$(curl -fsSL https://raw.githubusercontent.com/mut-ex/minimal-functional-fox/master/install.sh)"
> ```
   
+ Postavite temu za Firefox

> ```shell
> cp -r ~/Downloads/dots/.firefoxthemes ~/
> ```

+ Zatim otvorimo `Firefox` i idemo na `preferences`, zatim na `Home` i tamo gdje piše `Homepage and new windows` izaberemo `Custom URLs ...`, ispod pišemo ovo:

> ```shell
> file:///home/*YOUR USERNAME*/.firefoxthemes/startpage/Startpage/index.html
> ```
 
+ `Restartovati Firefox` 

## Instalacija GTK teme 

### Instalacija Lxappearance-a
      
> ```shell
> sudo apt-get install lxappearance
> ```
   
### Instalacija Nordic Dark teme

+ **Link: https://www.gnome-look.org/p/1267246/**

+ Preuzmite zip datoteku, izdvojite je i umetnite u Lxappearance.
 
### Instalacija Flattery Dark teme za ikone

+ **Link: https://www.gnome-look.org/s/Gnome/p/1332404**

+ Preuzmite zip datoteku, izdvojite je i umetnite u Lxappearance.
   
### Instalacija Oreo Blue kursor teme

+ **Link: https://www.gnome-look.org/s/Gnome/p/1360254/** 

+ Preuzmite zip datoteku, izdvojite je i umetnite u Lxappearance.

## Wikipedia

Nakon što smo napravili ovu BSPWM konfiguraciju, vrijeme je da razjasnimo što svaka aplikacija radi. Unutar direktorija `~/.config/` možete pronaći sve datoteke koje su vam potrebne za pokretanje BSPWM-a.

+ 🧠 `[BSPWM]`

   BSPWM je alat za upravljanje prozorima koji se, za razliku od drugih sučelja radne površine, svaki novi prozor otvara prema algoritmu.

    Ako imamo npr. dva prozora, oni će biti otvoreni na cijelom ekranu i ne mogu se nalaziti jedan preko drugog, kao što je slučaj u Windows ili GNOME sučeljima. Teoretski, učinkovito koristi prostor na zaslonu tako da je cijeli zaslon ispunjen. Ako nam ponestane prostora na prvoj radnoj površini, možemo se prečicom na tipkovnici ili mišem prebaciti na drugu radnu površinu i nastaviti koristiti ovaj operativni sustav.

+ ⌨️ `[SXHKD]`

   SXHKD je demon tipkovnice. Radi za nas kao pozadinski proces i govori BSPWM-u koju aplikaciju otvoriti ako korisnik pritisne određeni prečac na tipkovnici.

+ 🍫 `[Polybar]`

   Polybar je naša statusna traka na vrhu radne površine.

    Služi nam za prikaz obavijesti, datuma i vremena, interneta, baterije, gašenja i ponovnog pokretanja izbornika operativnog sustava te najvažnijih radnih prostora iz BSPWM-a.

+ 📚 `[Picom]`

   Picom je skladatelj; služi nam kao proces koji postavlja zaobljene rubove na svakoj aplikaciji koju otvorimo.

+ 🤓 `[Rofi]` 

   Rofi je proces koji otvara druge aplikacije, od najveće pomoći u pokretanju GTK aplikacija (aplikacija korisničkog sučelja).

+ 💻 `[Alacritty]` terminal.

   Alacritty služi kao emulator terminala, odnosno zamjena za standardni GNOME terminal.

    Koristimo ga uglavnom jer nam daje mogućnost postizanja boljeg izgleda uređivanjem njegovih konfiguracijskih datoteka.

+ 🐚 `[Oh-My-ZSH]` shell.

   Oh-My-ZSH je okvir koji nam olakšava upravljanje ZSH konfiguracijama.

   U ovom slučaju, uglavnom se koristi za dodavanje tema na terminal koji ima `ZSH shell`.

   `ZSH (Zshell)` je odabran jer je noviji, a većina ažuriranja iz drugih distribucija Linuxa već prelazi na njega u usporedbi s `Bash shellom`.

   + Koristili smo konfiguraciju `Powerlevel10k` za postavljanje tema.


+ 📋 `[Vim]` uređivač teksta

  Kako mnogi ljudi koriste notepad na Windows operativnim sustavima, mi koristimo nano i Vim.

  Nano uređivač teksta puno je lakši za korištenje, dok je Vim više namijenjen programerima zbog svojih prečaca.

   + Vim Airline je tema koja nam daje drugačiji izgled od običnog Vima.


+ 📺 `[Slim]` zaslon za zaključavanje

   Slim je naš zaslon za zaključavanje. 

   Slimlock je tema koju smo koristili za zaključani zaslon.

+ 💬 `[Dunst]` notifikacije

   Dunst je proces koji radi u pozadini, a primarna mu je namjena prikazivanje obavijesti na statusnoj traci (Polybar).

    Prednost dunsta je u tome što pruža mogućnost kodiranja tema za izgled i mnoge druge funkcije kao što su. Koje obavijesti prikazati itd.

+ 🕶️ `[Nordic Dark]` GTK tema

  Nordic Dark je GTK tema (tema za aplikacije korisničkog sučelja) koja nam daje mračni pogled na aplikacije s korisničkim sučeljem.

+ 🔷 `[Flattery Dark]` tema ikona

   Sam naziv govori da aplikacije s korisničkim sučeljem uglavnom imaju ikone na koje možemo kliknuti mišem; ova tema nam daje drugačiji pogled na ikone.

+ 🔵 `[Oreo Blue]` tema kursora

   Ova tema nam daje izgled plavog pokazivača, umetnuta je samo radi izgleda i jer odgovara svim drugim bojama ovog operativnog sustava.

+ 🔤 `[Source Code Pro]` font

   Font ovog operativnog sustava. 

+ 🔥🦊 `[Firefox]` web preglednik

   Koristim Firefox jer je to jedan od najboljih web preglednika orijentiranih na privatnost, po mom mišljenju.

+ 🦊 `[Minimal Functional Fox]` firefox tema.

   Ova tema je ovdje uglavnom zbog izgleda, ali i zato što je minimalna. 

+ ⏰ `tty-clock` 

   Tty-clock je aplikacija koja ima svrhu prikazivanja vremena i datuma na terminalu.
   
+ 🎚️ `CAVA` audio vizualizator.

   Cava je aplikacija koja služi kao audio vizualizator.

+ 📈 `HTop` 

   Aplikacija HTop pokazuje koji procesori trenutno rade i koliko RAM-a zauzimaju te mnoge druge stvari. Zamislite HTop kao upravitelj zadataka u operativnom sustavu Windows.
   
+ 😎 `CMatrix` 

   CMatrix je aplikacija koja je ovdje samo radi izgleda, a svrha joj je ispisati neki tekst u otvorenom terminalu koji ima za cilj dati prikaz hakiranja iz filma Matrix.

+ 🖼️ `SXIV` 

   SXIV je aplikacija za pregled slika koja nam otvara slike.

+ 🤠 `Ranger` 

   Ranger je aplikacija koja nam omogućuje pregled i pristup svim datotekama na računalu u terminalu.

+ 🗄️ `Pfetch`

   Svrha Pfetch aplikacije je pokazati koji operativni sustav koristimo, koji laptop/računalo imamo, koja je trenutna verzija kernela, koliko trenutno imamo uptime, koliko paketa imamo i koliko RAM-a imamo.

+ ⚙️ `Chafa`

   Chafa je aplikacija koja ispisuje sliku za korištenje u terminalu, čime se postiže retro/ASCII izgled slike.

+ 🐍 `Snake`

   U ovom slučaju, Snake app je stara igrica zmija s telefona Nokia 3310 koja je malo modificirana po pitanju boja i prilagođena za igranje na terminalu.

+ 🍭 `Lollypop` 

   Lollypop je glazbena aplikacija, kroz nju puštamo pjesme.


## Prečaci

Kao <kbd>super</kbd> koristimo tipku Windows na tipkovnici. Super je najvažnija tipka na našoj tipkovnici jer je koristimo za davanje uputa demonu tipkovnice SXHKD.

## Tipkovnica

| Tipke | Svrha |
| ----- | ----- |
| <kbd>super + enter</kbd> | Otvara terminal |
| <kbd>super + space</kbd> | Otvara Rofi preko kojeg otvaramo GTK aplikacije |
| <kbd>super + escape</kbd> | Ponovno učitava SXHKD i njegove konfiguracijske datoteke |
| <kbd>super + alt + r</kbd> | Ponovno pokreće BSPWM Tiling Window Manager |
| <kbd>super + w</kbd> | Isključuje trenutnu aplikaciju |
| <kbd>super + [1-0]</kbd> | Mijenja trenutni radni prostor |
| <kbd>super + g</kbd> | Mijenja trenutačni prozor koji je manji u područje većeg prozora, dok veći prozor stavlja na mjesto manjeg |
| <kbd>super + m</kbd> | Otvara aplikaciju preko cijele radne površine |
| <kbd>super + [h,j,k,l]</kbd> | Premješta fokus na drugi prozor |
| <kbd>super + alt + [h,j,k,l]</kbd> | Pomiče prozore prema van |
| <kbd>super + alt + shift + [h,j,k,l]</kbd> | Pomiče prozore prema unutra |
| <kbd>super + s</kbd> | Stavlja prozore u tzv. float mod, opciju gdje možemo staviti prozor na prozor kao u Windows operativnim sustavima |
| <kbd>super + ctrl + [strelice]</kbd> | Pomiče plutajuće prozore |



## Hvala vam na vašem vremenu 💙

