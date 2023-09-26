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




