<h2>AAAAALLRIGHT, this is the the part 3 of Linux Fundamentals with THM</h2>

<h3>Terminal Text Editors</h3>

There are a few options that you can use, all with a variety of friendliness and utility. This task is going to introduce you to ```nano``` but also show you an alternative named ```VIM```

Nano

It is easy to get started with Nano! To create or edit a file using nano, we simply use nano filename -- replacing "filename" with the name of the file you wish to edit.

```
tryhackme@linux3:/tmp# nano myfile
  GNU nano 4.8                                             myfile                                                       

^G Get Help    ^O Write Out   ^W Where Is    ^K Cut Text    ^J Justify     ^C Cur Pos     M-U Undo       M-A Mark Text
^X Exit        ^R Read File   ^\ Replace     ^U Paste Text  ^T To Spell    ^_ Go To Line  M-E Redo       M-6 Copy Text
```

Once we press enter to execute the command, ```nano``` will launch! Where we can just begin to start entering or modifying our text. 
You can navigate each line using the "up" and "down" arrow keys or start a new line using the "Enter" key on your keyboard.

```
tryhackme@linux3:/tmp# nano myfile
  GNU nano 4.8                                             myfile                                             Modified  

Hello TryHackMe
I can write things into "myfile"


^G Get Help    ^O Write Out   ^W Where Is    ^K Cut Text    ^J Justify     ^C Cur Pos     M-U Undo       M-A Mark Text
^X Exit        ^R Read File   ^\ Replace     ^U Paste Text  ^T To Spell    ^_ Go To Line  M-E Redo       M-6 Copy Text
```

Nano has a few features that are easy to remember & covers the most general things you would want out of a text editor, including:

Searching for text
Copying and Pasting
Jumping to a line number
Finding out what line number you are on
You can use these features of nano by pressing the "Ctrl" key (which is represented as an ```^``` on Linux or MAC)  and a corresponding letter. 
For example, to exit, we would want to press "Ctrl" and "X" to exit Nano.


VIM

VIM is a much more advanced text editor. Whilst you're not expected to know all advanced features, 
it's helpful to mention it for powering up your Linux skills.

Some of VIM's benefits, albeit taking a much longer time to become familiar with, includes:

- Customisable - you can modify the keyboard shortcuts to be of your choosing
- Syntax Highlighting - this is useful if you are writing or maintaining code, making it a popular choice for software developers
- VIM works on all terminals where nano may not be installed
- There are a lot of resources such as cheatsheets, tutorials, and the sorts available to you use.


<h3>General/Useful Utilities</h3>

Downloading Files

A pretty fundamental feature of computing is the ability to transfer files. For example, you may want to download a program, a script, or even a picture. 
Thankfully for us, there are multiple ways in which we can retrieve these files.

We're going to cover the use of ```wget```.  This command allows us to download files from the web via HTTP -- as if you were accessing the file in your browser. We simply need to provide the address of the resource that we wish to download. For example, if I wanted to download a file named "myfile.txt" onto my machine, assuming I knew the web address it -- it would look something like this:

```wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt```

<h3>Processes 101</h3>

Processes are the programs that are running on your machine. They are managed by the kernel, 
where each process will have an ID associated with it, also known as its PID. 
The PID increments for the order In which the process starts. I.e. the 60th process will have a PID of 60.

Viewing Processes

We can use the friendly ```ps``` command to provide a list of the running processes as our user's session and some additional information such as its status code, '
the session that is running it, how much usage time of the CPU it is using, and the name of the actual program or command that is being executed:

![ps1](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/fbf646e8-7cd5-43f3-a001-ff93302c9ac9)

Note how in the screenshot above, the second process ```ps``` has a PID of 204, and then in the command below it, this is then incremented to 205.

To see the processes run by other users and those that don't run from a session (i.e. system processes), we need to provide aux to the ps command like so: ```ps aux```

![ps2](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/fb1ab363-2303-4ff1-bb06-590d0a741be6)

Note we can see a total of 5 processes -- note how we now have "root"  and "cmnatic"

Another very useful command is the top command; top gives you real-time statistics about the processes running on your system instead of a one-time view. These statistics will refresh every 10 seconds, but will also refresh when you use the arrow keys to browse the various rows. Another great command to gain insight into your system is via the ```top``` command

![top1](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/95c9b6b0-9b54-4d0a-b59b-c7f1d1acbd9d)

Managing Processes

You can send signals that terminate processes; there are a variety of types of signals that correlate to exactly how "cleanly" the process is dealt with by the kernel. 
To kill a command, we can use the appropriately named ```kill``` command and the associated PID that we wish to kill. i.e., to kill PID 1337, we'd use ```kill 1337```.

Below are some of the signals that we can send to a process when it is killed:

```SIGTERM``` - Kill the process, but allow it to do some cleanup tasks beforehand

```SIGKILL``` - Kill the process - doesn't do any cleanup after the fact

```SIGSTOP``` - Stop/suspend a process


How do Processes Start?

Let's start off by talking about namespaces. The Operating System (OS) uses namespaces to ultimately split up the resources available on the computer to (such as CPU, RAM and priority) processes. 
Think of it as splitting your computer up into slices -- similar to a cake. Processes within that slice will have access to a certain amount of computing power, however, 
it will be a small portion of what is actually available to every process overall.

Namespaces are great for security as it is a way of isolating processes from another -- only those that are in the same namespace will be able to see each other.

We previously talked about how PID works, and this is where it comes into play. The process with an ID of 0 is a process that is started when the system boots. 
This process is the system's init on Ubuntu, such as systemd, which is used to provide a way of managing a user's processes and sits in between the operating system and the user. 

For example, once a system boots and it initialises, systemd is one of the first processes that are started. 
Any program or piece of software that we want to start will start as what's known as a child process of systemd. This means that it is controlled by systemd, but will run as its own process 
(although sharing the resources from systemd) to make it easier for us to identify and the likes.
![process1](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/767af8d0-0074-46fe-8834-8b19bda7b324)

An Introduction to Backgrounding and Foregrounding in Linux

Processes can run in two states: In the background and in the foreground. For example, commands that you run in your terminal such as "echo" 
or things of that sort will run in the foreground of your terminal as it is the only command provided that hasn't been told to run in the background. 
"Echo" is a great example as the output of echo will return to you in the foreground, but wouldn't in the background - take the screenshot below, for example.

![bg1](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/0d686ef3-0c3b-4ed1-8992-fdbfdab66f26)

Here we're running ```echo "Hi THM"``` , where we expect the output to be returned to us like it is at the start. 
But after adding the ```&``` operator to the command, we're instead just given the ID of the echo process rather than the actual output -- as it is running in the background.

This is great for commands such as copying files because it means that we can run the command in the background 
and continue on with whatever further commands we wish to execute (without having to wait for the file copy to finish first)

We can do the exact same when executing things like scripts -- rather than relying on the & operator, we can use ```Ctrl + Z``` on our keyboard to background a process. 
It is also an effective way of "pausing" the execution of a script or command like in the example below:

![bg2](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/6686d666-752a-4f43-b563-41868b8ae653)

This script will keep on repeating "This will keep on looping until I stop!" until I stop or suspend the process. 
By using ```Ctrl + Z``` (as indicated by ```T^Z```). Now our terminal is no longer filled up with messages -- until we foreground it, which we will discuss below.


Foregrounding a process

Now that we have a process running in the background, for example, our script "background.sh" which can be confirmed by using the ```ps aux``` command, 
we can back-pedal and bring this process back to the foreground to interact with.

![bg3](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/5b36cf26-19fe-4d17-9809-2c4f56849f12)

With our process backgrounded using either ```Ctrl + Z``` or the & operator, we can use ```fg``` to bring this back to focus like below, where we can see the ```fg``` 
command is being used to bring the background process back into use on the terminal, where the output of the script is now returned to us.

![bg4](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/b8bc0814-07b8-4c2b-81ab-c60a8bc5db9e)

![bg5](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/c3facf0a-a93b-47a2-a68b-c197d5687ab3)

<h3>Questions / Answers </h3>

If we were to launch a process where the previous ID was "300", what would the ID of this new process be?

```301```

If we wanted to cleanly kill a process, what signal would we send it?

```SIGTERM```

Locate the process that is running on the deployed instance (10.10.61.194). What flag is given?

```THM{PROCESSES}```

What command would we use to stop the service "myservice"?

```systemctl stop myservice```

What command would we use to start the same service on the boot-up of the system?

```systemctl enable myservice```

What command would we use to bring a previously backgrounded process back to the foreground?

```fg```

