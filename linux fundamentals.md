<h2>Linux commands</h2>

```pwd print working directory```

```cd change directory```

```whoami print the current user```

```cd .. step back in file system```

```ls listing everything in the current directory```

```cat cancatenate / open a file```

```touch create a file```

We can also search a file with the following command
```
find -name file.txt
```
If we look for a specific file extension we can do the following
```
find -name *.txt
```
Another great utility that is a great one to learn about is the use of ```grep```. 
The ```grep``` command allows us to search the contents of files for specific values that we are looking for

```grep "81.143.211.90" access.log```

<h2>Shell Operators</h2>

```&```	This operator allows you to run commands in the background of your terminal.

For example ```cp largefile.txt /destination/path/ &```

```&&```	This operator allows you to combine multiple commands together in one line of your terminal.

For example ```command1 && command2```


```>```	This operator is a redirector - meaning that we can take the output from a command (such as using cat to output a file) and direct it elsewhere.

Let's say we wanted to create a file named "welcome" with the message "hey". We can run ```echo hey > welcome``` where we want the file created with the contents "hey" like so:

Using the ```>``` Operator
```tryhackme@linux1:~$ echo hey > welcome```

Using ```cat``` to output the "welcome" file

```tryhackme@linux1:~$ cat welcome```

```hey```

```>>```	This operator does the same function of the ```>``` operator but appends the output rather than replacing (meaning nothing is overwritten).

This operator is also an output redirector like in the previous operator (```>```) we discussed. However, what makes this operator different is that rather than overwriting any contents within a file, for example, it instead just puts the output at the end.

The ```>>``` operator allows to append the output to the bottom of the file — rather than replacing the contents like so:

```tryhackme@linux1:~$ echo hello >> welcome```

```tryhackme@linux1:~$ cat welcome```
```hey```
```hello```
