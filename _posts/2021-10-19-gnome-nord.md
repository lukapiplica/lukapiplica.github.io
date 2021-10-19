---
title: "[GNOME] Nord Ubuntu GNU/Linux OS"
date: 2021-10-19 15:32:00 +0800
categories:
  - Linux
tags:
  - GNOME
  - Desktop Environment
  - Ubuntu
---


<p align="center">
  <img width="50%" src="/assets/images/gnomenord/gif2.gif" />
</p>


<p align="center">
  <b>👋 GNOME goes NORD konfiguracijski fajlovi 👋</b>
</p>



### Hvala na posjeti!

<img src="/assets/images/gnomenord/edited2.png" alt="img" align="center" width="400px">
<img src="/assets/images/gnomenord/edited.png" alt="img" align="center" width="400px">

Ovo su moji trenutni dotfile-ovi Pop! OS Linux distribucije.

Instalacija će vam pomoći da napravite isti izgled kao na slikama, tu imate uputstvo korak po korak.

Sistemske Specifikacije:

+ **OS**: [Ubuntu](https://ubuntu.com/) 
+ **GTK Theme**: [Nordic](https://www.gnome-look.org/p/1267246)
+ **Icon Theme**: [Flatery_Dark](https://www.gnome-look.org/p/1332404)
+ **Cursor Theme**: [Oreo_Blue](https://www.gnome-look.org/s/Gnome/p/1360254/)
+ **Browser**: [Firefox](https://www.mozilla.org/en-US/firefox/new/)


## Instalacija

Da bismo počeli sa pravljenjem ovog izgleda, pretpostavljam da imate friško instaliran Ubuntu 20.04 sa minimalnom instalacijom.

*Ako vas zanima šta koja aplikacija radi Wikipedia 'e vam pomoći.*

1. Updejtanje repozitorija i upgrejdanje sistema: 

      ```shell
      sudo apt update
      sudo apt upgrade
      ```

2. Instalacija **Gnome Tweak Tool**:

   Prvo moramo instalirati gnome tweak tool, da bismo mogli instalirati gnome ekstensions.

   + **Instalacija Gnome Tweak Tool-a**:

     ```shell 
     sudo apt install gnome-shell-extensions
     ```

   + **Zatim otvoriti Firefox i otići na [LINK](https://extensions.gnome.org/) i skinuti add-on.**

 
   + **Skidanje potrebnih dodataka**:

    Nakon što skinemo Gnome Extension add-on moramo pomjeriti slider na On, na nekoliko dodataka, njih možete pronaći na linkovima ispod:

    [Dash to Panel](https://extensions.gnome.org/extension/1160/dash-to-panel/)
    [User Themes](https://extensions.gnome.org/extension/19/user-themes/)
    [Transparent Window Moving](https://extensions.gnome.org/extension/1446/transparent-window-moving/)


    Zatim provjeriti da li su uključeni u operativnom sistemu, tako što otvorimo aplikaciju Gnome Tweak Tool i provjerimo da li su uključene gore navedeni dodatci, također isključiti Desktop ikonice. 

    **NAPOMENA:** Dash to panel možete u postavkama postaviti po vašoj želji (da napravite ikonice manje itd.), također i Transparent Window moving moje postavke su na 0.2. 

   + **Instaliranje Pop Shell-a**:

     ```shell
     sudo apt install git node-typescript make
     ``` 

     Nakon instalacije potrebnih dependency-a, trebamo otići u Downloads folder u terminalu. 

     ```shell
     cd ~/Downloads 
     ```

     Zatim trebamo klonirati repozitoriju: 

     ```shell
     git clone https://github.com/pop-os/shell.git
     ```

     Zatim ulazimo u shell folder:

     ```shell
     cd shell
     ```

     Instalacija Pop Shell-a:

     ```shell
     make local-install
     ```



3. **Instalacija ostalih aplikacija**:

   + Instalacija neofetch-a: 

      ```shell
      sudo apt install neofetch
      ```

   + Instalacija zathura-e: 

      ```shell
      sudo apt install zathura
      ```

   + Instalacija tty-clock:

      ```shell
      sudo apt install tty-clock
      ```

    + Instalacija cmatrix-a:

      ```shell
      sudo apt install cmatrix
      ```

    + Instalacija htop-a:

      ```shell
      sudo apt install htop
      ``` 

    + Instalacija ranger-a:

      ```shell
      sudo apt install ranger
      ```

    + Instalacija Vim-a: 

      ```shell
      sudo apt install vim
      ```

    + Instalacija Lollypop-a: 

      ```shell
      sudo apt install lollypop
      ```

    + Instalacija cbonsai-a:

      ```shell
      cd ~/Downloads
      sudo apt install libncursesw5-dev
      git clone https://gitlab.com/jallbrit/cbonsai
      cd cbonsai
      make install PREFIX=~/.local
      ```
    
    + Instalacija tty-tetris-a:

      ```shell
      cd ~/Downloads
      sudo apt install cmake
      git clone https://github.com/Holixus/tty-tetris-v2.git
      cmake .
      make 
      sudo make install
      ```


    + Instalacija Cava-e:

      Prvo instaliramo potrebne dependecy-e:

      ```shell
      sudo apt install libfftw3-dev libasound2-dev libncursesw5-dev libpulse-dev libtool automake libiniparser-dev

      export CPPFLAGS=-I/usr/include/iniparser
      ```

      Zatim ulazimo u Downloads folder i kloniramo Cava repozitorij:

      ```shell
      cd ~/Downloads

      git clone https://github.com/karlstav/cava.git
      ```
      Zatim moramo kompajlirati Cavu:

      ```shell
      cd cava
      ./autogen.sh
      ./configure
      make
      ```

      Zatim instaliramo Cavu: 

      ```shell
      sudo make install
      ```

    + Instalacija Ttyper-a:

      ```shell
      sudo apt install cargo

      sudo apt install ttyper
      ```


4. **Instalacija GRUB teme**:

   + Kloniranje repozitorije:
   
      ```shell
      cd ~/Downloads
      git clone https://github.com/semimqmo/sekiro_grub_theme
      ```

   + Instalacija GRUB teme: 

      ```shell
      sudo ./install.sh
      ```

5. **Instalacija Tema**: 

    + **GTK Theme**: [Nordic](https://www.gnome-look.org/p/1267246)
    + **Icon Theme**: [Flatery_Dark](https://www.gnome-look.org/p/1332404)
    + **Cursor Theme**: [Oreo_Blue](https://www.gnome-look.org/s/Gnome/p/1360254/)

    **NAPOMENA**: Za instalaciju ovih tema, morate napraviti dva skrivena foldera u home direktoriji. 

    ```shell
    cd ~/
    mkdir .themes
    mkdir .icons
    ```
    U .themes folder moramo ubaciti GTK temu i Icon temu, a u .icons ubaciti Cursor temu. Nakon toga ih moramo uklju;iti iz aplikacije Gnome Tweak Tools.

6. Napraviti ili skinuti već neki postojeći Startpage i dodati ga u Firefox. 
7. Promjeniti Wallpaper kroz Gnome Tweak Tool.



## Wikipedia

Nakon što smo napravili ovu konfiguraciju GNOME-a vrijeme je da pojasnimo šta koja aplikacija radi. 

+ 🧠 `[Pop Shell]`

   Pop Shell nam daje opciju da na Desktop sistemu koristimo Tilling Window Manager, koji raspoređuje prozore na ekranu po skripti i tako štedi prostora na ekranu.

+ ⌨️ `[Neofetch]`

   Neofetch je komanda koja nam daje sistemske specifikacije plus ima cool izgled. 


+ 🍫 `[Zathura]`

   Zathura je čitač PDF-ova, gdje je moguće mijenjati izgled i mnoge druge opcije pomoću jednog konfiguracijskog fajla.


+ 🐚 `[Ranger]` 

   Ranger nam služi kao fajl manager u terminalu.


+ 📋 `[Vim]` text editor

  Kao što mnogi ljudi koriste notepad na Windows operativnim sistemima, mi koristimo nano i vim.

  Nano text editor je puno lakši za korištenje, dok Vim je napravljen više za programere zbog njegovih kratica. 


+ 🌳 `[cbonsai]`

  Cbonsai je skripta koja nam u terminalu napravi drvo od znakova, slova i brojeva.


+ 🎮 `[tty-tetris]`

  Tty-tetris je aplikacija koja nam omogućava igranje tetrisa u terminalu.

+ 📰 `[ttyper]`

  Ttyper nam je aplikacija koja mjeri brzinu kucanja u terminalu. 


+ 🕶️ `[Nordic]` GTK tema.

   Nordic Dark je GTK tema (tema za aplikacije sa korisničkim interfejsom) koja nam daje tamni izgled aplikacijama koje imaju korisnički interfejs.

+ 🔷 `[Flattery]` tema za ikonice.

   Samo ime kaže, aplikacije koje imaju korisnički interfejs većinom imaju ikonice na koje možemo kliknuti mišem, ova tema nam pruža drugačiji izgled ikonicama.

+ 🔵 `[Oreo Blue]` kursor tema.

   Ova tema nam daje plavi izgled kursoru, ubačena je samo radi izgleda kursora i zato što se slaže sa svim ostalim bojama ovog operativnog sistema.


+ 🔥🦊 `[Firefox]` web preglednik.

   Firefox koristim jer je jedan od po mome mišljenu najboljih web preglednika koji je orijentisan ka privatnosti.


+ ⏰ `tty-clock` 

   Tty-clock nam je aplikcija koja ima svrhu da u terminalu pokaže vrijeme i datum. 

+ 🎚️ `CAVA` audio visualizer.

   Cava nam je aplikacija koja služi kao audio vizualizator.

+ 📈 `HTop` 

   HTop aplikacija nam služi da prikaže koji procesori trenutno rade i koliko RAM memorije oni uzimaju kao i mnogo drugih stvari. Zamislite HTop kao Task Manager u Windows operativnom sistemu.

+ 😎 `CMatrix` 

   CMatrix nam je aplikacija koja je ovdje samo radi izgleda i njezina svrha je da u otvorenom terminalu ispisuje neki text kojem je cilj da daje prikaz hakovanja iz filma Matrix-a. 


+ 🤠 `Ranger` 

   Ranger je aplikacija koja nam omogućava da u terminalu vidimo i pristupimo svim fajlovima na računaru. 


+ 🍭 `Lollypop` 

   Lollypop je aplikacija za muziku, preko nje puštamo pjesme. 





### Hvala puno na izdvojenom vremenu 💙

