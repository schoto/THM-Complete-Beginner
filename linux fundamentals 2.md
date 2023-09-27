<h4>Here we go for the second part of Linux Fundamentals</h4>

We are going to deploy a Linux VM on browser to try some cool stuff

For instance we learned this command to connect to another machine via internet with ```ssh```

```ssh tryhackme@10.10.238.28```

If we want to list stuff we will execute this command ```ls``` , but if we want to see even hidden files, we do

```ls -a``` The ```-a``` is for "all"

If we execute ```ls --help``` it will show us what we can do with ```ls``` command

<h2>More commands</h2>

```touch``` Create file

```mkdir``` Create folder

```cp``` Copy a file or folder

```mv``` Move a file or folder

```rm``` Remove a file or folder

```file``` Determine the type of a file

To create a file

```
tryhackme@linux2:~$ touch note
tryhackme@linux2:~$ ls           
folder1 note
```

To create a folder

```
tryhackme@linux2:~$ mkdir mydirectory
tryhackme@linux2:~$ ls           
folder1 mydirectory note
```

To remove a file

```
tryhackme@linux2:~$ rm note
tryhackme@linux2:~$ ls           
folder1 mydirectory
```

To remove a directory / folder

```
tryhackme@linux2:~$ rm -R mydirectory
tryhackme@linux2:~$ ls           
folder1
```

<h3>Copying and Moving Files and Folders (cp, mv)</h3>

Copying and moving files is an important functionality on a Linux machine. Starting with ```cp```, this command takes two arguments:

1. the name of the existing file

2. the name we wish to assign to the new file when copying

```cp``` copies the entire contents of the existing file into the new file. In the screenshot below, we are copying "note" to "note2".

Using ```cp``` to copy a file

```
tryhackme@linux2:~$ cp note note2
tryhackme@linux2:~$ ls           
folder1 note note2
```

Using mv to move a file
```
tryhackme@linux2:~$ mv note2 note3
tryhackme@linux2:~$ ls           
folder1 note note3
```

Determining File Type

What is often misleading and often catches people out is making presumptions from files as to what their purpose or contents may be. 
Files usually have what's known as an extension to make this easier. For example, text files usually have an extension of ".txt". 
But this is not necessary.

So far, the files we have used in our examples haven't had an extension. Without knowing the context of why the file is there -- we don't really know its purpose. 
Enter the ```file``` command. This command takes one argument. For example, we'll use ```file``` to confirm whether or not the "note" file in our examples is indeed a text file, like so file note.

```
tryhackme@linux2:~$ file note
note: ASCII text
```

<h2>Questions / Answers</h2>

How would you create the file named "newnote"?

```touch newnote```

On the deployable machine, what is the file type of "unknown1" in "tryhackme's" home directory?

```ascii text```

How would we move the file "myfile" to the directory "myfolder" 

```mv myfile myfolder```

<h2>Switching between users</h2>

Switching between users on a Linux install is easy work thanks to the ```su``` command. 
Unless you are the root user (or using root permissions through sudo), then you are required to know two things to facilitate this transition of user accounts:

The user we wish to switch to

The user's password

<h2>Common directories</h2>

<h3>/etc</h3>

This root directory is one of the most important root directories on your system. 

The etc folder (short for etcetera) is a commonplace location to store system files that are used by your operating system. 

For example, the sudoers file highlighted in the screenshot below contains a list of the users & groups that have permission to run sudo or a set of commands as the root user.

Also highlighted below are the "passwd" and "shadow" files. These two files are special for Linux as they show how your system stores the passwords for each user in encrypted formatting called sha512.

```
tryhackme@linux2:/etc$ ls
shadow passwd sudoers sudoers.d
```

<h3>/var</h3>

The "/var" directory, with "var" being short for variable data,  is one of the main root folders found on a Linux install. 
This folder stores data that is frequently accessed or written by services or applications running on the system. For example, 
log files from running services and applications are written here (/var/log), or other data that is not necessarily associated with a specific user (i.e., databases and the like).

```
tryhackme@linux2:/var$ ls
backups log opt tmp
```

<h3>/root</h3>

Unlike the /home directory, the /root folder is actually the home for the "root" system user. 
There isn't anything more to this folder other than just understanding that this is the home directory for the "root" user. 
But, it is worth a mention as the logical presumption is that this user would have their data in a directory such as "/home/root" by default.

```
root@linux2:~# ls
myfile myfolder passwords.xlsx
```

<h3>/tmp</h3>

This is a unique root directory found on a Linux install. Short for "temporary", the /tmp directory is volatile and is used to store data that is only needed to be accessed once or twice. 
Similar to the memory on your computer, once the computer is restarted, the contents of this folder are cleared out.
What's useful for us in pentesting is that any user can write to this folder by default. Meaning once we have access to a machine, it serves as a good place to store things like our enumeration scripts.

```
root@linux2:/tmp# ls
todelete trash.txt rubbish.bin
```

<h2>Questions / Answers</h2>

What is the directory path that would we expect logs to be stored in?

```/var/logs```

What root directory is similar to how RAM on a computer works?

```/tmp```

Name the home directory of the root user 

```/root```


