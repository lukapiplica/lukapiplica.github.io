---
title: "How to protect a Linux server"
draft: false
date: 2022-10-09
description: "A guide on how to protect a Linux server" 
categories:
  - Linux
---



<p align="center">
  <img width="40%" src="1.webp" />
</p>

<p align="center">
  <b>🐧 How to protect a Linux server ! 🐧</b>
</p>


Everyone already knows you should protect a server and make it more secure. Well, here are some basics steps to take to protect your servers. Let's get right into it: 

Firstly I would highly recommend using **HTTPS** protocol for your mirrors! 

I will assume you have a fresh install of a Linux server, keep in mind these commands are focused on the **apt** packet manager, but they should work with other packet managers with minor changes. 

## Updating your server 

After a fresh install, the first thing I do is update the server manually: 

 ```shell
 sudo apt update
 sudo apt upgrade
 ```

## Enabling automatic updates

After updating my server manually, I usually enable automatic updates. 

Keep in mind depending on how critical the server is you might not want updates to break it. 

To enable automatic updates you need a package called **unattended-upgrades** !

> ```shell
> sudo apt install unattended-upgrades
> ```

Then you have to enable it: 

> ```shell
> sudo dpkg-reconfigure --priority=low unattended-upgrades
> ```

## Secure Shell (SSH)

### Preparation

Usually, connecting to servers is done remotely via SSH protocol on the **default port of 22**. 

Firstly I will make a new folder if it doesn't exist in the **/home** directory called **.ssh**. 

>    ```shell
>    mkdir ~/.ssh
>    ```

Then we will give the folder permissions of **700**, which protects a file against access from other users while the issuing user still has full access.

>    ```shell
>    chmod 700 ~/.ssh
>    ```

Now we want to log out of our server if we are connected via ssh. 

>    ```shell    
>    logout
>    ```
    
### Generating a solid Secure Shell key pair 

Now let's generate a Public and a Private key pair so we can safely connect to the server. I use the ed25519 algorithm since it's fast and doesn't compromise security. 

I would also recommend using a passphrase.  

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
  
This will store the private and public keys in your home/.ssh folder depending on your OS, it might be hidden. 

### Copying the public key to the server remotely 

After the public and private keys are generated, we need to transfer them to the server. I will use **SCP** to move the key to the server. 

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

### Passwordless remote access and changing the default port

Now we need to lockdown our ssh and disable passwords so you can only log in with the generated key pairs. We will log into our server and edit the ssh config file. 

Opening the config file: 
        
> ```shell
> sudo nano /etc/ssh/sshd_config
> ```

Let's change the default **port** of **22**. Uncomment the **Port** line, delete the number 22 and put something to your liking. 
    
**Use higher numbers like 4723, for example**. 

Now on the **AddressFamily** line, you can specify if you want to use IPv4, IPv6 or both. I disable IPv6, but you don't have to. If you choose only to use IPv4, then replace **any** with **inet**

**Disable root login** by replacing **PermitRootLogin yes** to **PermitRootLogin no**.

Then disable password authentication by replacing **PasswordAuthentication yes** with **PasswordAuthentication no**

Now save the changes! 

### Restarting SSH to apply changes

After we made changes to the config file, we now need to restart the ssh service. 

> ```shell
> sudo systemctl restart sshd
> ```

{{< alert >}}
**NOTE**: Make sure you have a connection by trying to connect from another terminal/powershell. If you make a mistake, you can lock yourself out!
{{< /alert >}}

## Enabling firewall

Firstly check your used ports by: 

> ```shell
> sudo ss -tupln
> ```

You might have other ports used, do your research, but I'll only enable ssh so I can connect to the server. 

First, let's install ufw. 

> ```shell
> sudo apt install ufw
> ```

I will use **ufw** as my firewall. Remember the last port we put in the config file of ssh. We need to allow it. Also, it is always recommended to specify what protocol the port uses, either TCP or UDP! 

> ```shell
> sudo ufw allow SSH_PORT/tcp
> ```

Then we need to enable the firewall. 

> ```shell
> sudo ufw enable
> ```

To check what rules are allowed, we can use the following: 

> ```shell
> sudo ufw status
> ```

## Disable ICMP (ping)

Usually, the command **ping** is helpful for network administrators and hackers. The best practice is to disable ping!

To disable ping, we need to edit ufw config. 

> ```shell
> sudo nano /etc/ufw/before.rules 
> ```

Under the section called **ok icmp codes for INPUT**, paste this line so it will be first (right under ok icmp codes for INPUT). 

> ```shell
> -A ufw-before-input -p icmp --icmp-type echo-request -j DROP
> ```

Reboot the server: 

> ```shell
> sudo reboot now
> ```

Ping has now been disabled!

## Conclusion

The non-hackable server doesn't exist! Keep in mind that every server is hackable, but this is a good practice you should consider trying to harden your server. 

## Thank you for your time 💙

