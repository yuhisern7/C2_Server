[![forthebadge made-with-python](http://ForTheBadge.com/images/badges/made-with-python.svg)](https://www.python.org/)
[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](http://www.gnu.org/licenses/gpl-3.0)

![](https://github.com/reveng007/C2_Server/blob/main/images/banner.png?raw=true)

# ***C2 Server***

## So, What the heck is a C2 Server and what it's gonna do ?

Well, Command & Control server, also called C2 or C&C server. It is actually a centralized server or computer or simply control centre that attackers use to control their target machine (or victim). Attacker just need to send the reverse shell script(exploit) and execute it (in someways) on the target machine and that's it. Reverse shell is basically a code which is injected into the trgt machine, so that target machine alone can send an initiating connection request back to attacker machine where C2 server is running/listening on open/listening port. Here also, we are doing the same thing. Once the C2 Server is connected to target machine, anything on victim machine can be accessed by the attacker depending on the efficiency of the C2 server.

![](https://miro.medium.com/max/1162/1*aNtBQC4GG8klpMxvZ2_WuQ.png)

## Currently, this C2 Server have these functionalities:

```

List of available Commands:
----------------------------------------------------------------------------------------

exit                          :    To terminate session

mkdir <directory>
(linux/windows)               :    To make folders

touch <file>
(linux/win)                   :    To make files

echo "<something>"            :    To display line of text/string that are passed as an argument

echo "<something>" >/>> file  :    To redirect text to a file, make files
(linux/windows)

cd <directory>
(linux/win)                   :    To change directory/folder

del <file>                    :    To remove files
(linux/win)

rmdir <folder>
OR                            :    To remove folder
rm -r <folder>
(linux/windows)

clear / cls (linux/windows)   :    To clear terminal/cmd
(Can be used interchangeably)

ls_h                          :    List files in host's present working directory

take <file> (linux/windows)   :    To exfiltrate file from trgt

drop <file> (linux/windows)   :    To infiltrate file from C2 server to trgt

screenshot OR  ss             :    To take screenshot and self destructs the screenshot from trgt

keylog_on                     :    To start keylogger

keylog_dump                   :    To print keystrokes

keylog_off                    :    To close keylogger and self destruct the logged file

spoof_passwd                  :    To spoof password as a file from trgt machine's browser (windows 10, Chrome browser Version 89.0.4389.90 (Official Build) (64-bit)) and sents to C2Server
(windows only)

spoof_wanip                   :    Spoofs public/wan ip of the trgt machine


You can also use other commands related to networking, etc for linux as well as windows
------------------------------------------------------------------------------------------
```
## To test this C2 Server:
Clone the repository:
```
$ git clone https://github.com/reveng007/C2_Server.git
```
#### Install the required python dependencies on both attacker and victim machines:
&nbsp;
##### For win machine:
```
$ pip install -r win_requirement.txt
```
##### For linux machine:
```
$ pip install -r lnx_requirement.txt
```
### NOTE:
Just a reminder, win32crypt can't be installed in linux, so I have made seperate requirement files

## Now, we are all set, but how to use this scripts ?

At first move the rev_shell.py script to the trgt machine, linux or windows (above 7).
Then back in the attacker machine, run the server script:
```
$ python3 server.py
```
Then server will keep on listening for connection. Start the rev_shell.py on the victim machine:
```
$ python3 rev_shell.py
```
Now, we will get a shell on the C2 Server to play around:
![](https://github.com/reveng007/C2_Server/blob/main/images/shell.png?raw=true)

_In this case, I actually used Windows10 as victim machine._

## Why am I making this ?

1. I'm making this to know, how things work. Exploring the things which are most of the time present behind the curtains and also to experience, how it feels to be on the developing side ;)

2. Aiming to make a more stable version of C2 server, as most C2 servers tend to lag/hang and even terminate sessions unreliably.

## To Do List:
- Response becomes slow sometimes.

  One of the Eg: 
 
  If I use 'touch' to make a file in linux, then I do 'ls'(1st time) to list down files on pwd, nothing will be shown, again I do 'ls'(2nd time), then it shows us the updated file list. But now if we again type any command except 'ls'
    we can see that again file listing is shown. As 1st 'ls' result was shown when 2nd time 'ls' was
    used  by me and the result for 2nd time use of 'ls' was shown now. And this goes on.
In this way the server lags...

- Exfiltration : Adding receiving folder section
- Infiltration : Adding sending folder section
- Wan/public ip spoofer (Though mentioned in help section, but that func is not uploaded, coming soon...)
- Ransomeware
- Adding persistance for windows
- PrivEsc
- If possible : mimikatz (support)

### Advancement of some functionalities:

- Adding screenshot functionalities with **ctypes** python library by removing Pillow, as Pillow library does not come with default installation of python but **ctypes** library does.
- Adding threading
