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

Maintaining Your System: Automation

Users may want to schedule a certain action or task to take place after the system has booted. 
Take, for example, running commands, backing up files, or launching your favourite programs on, such as Spotify or Google Chrome.

We're going to be talking about the ```cron``` process, but more specifically, how we can interact with it via the use of ```crontabs```.
Crontab is one of the processes that is started during boot, which is responsible for facilitating and managing cron jobs.

![cron1](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/8a33dc02-20fb-41b1-9255-e4545e2b2393)

A crontab is simply a special file with formatting that is recognised by the ```cron``` process to execute each line step-by-step. Crontabs require 6 specific values:

```Value```	Description

```MIN```	What minute to execute at

```HOUR```	What hour to execute at

```DOM```	What day of the month to execute at

```MON```	What month of the year to execute at

```DOW```	What day of the week to execute at

```CMD```	The actual command that will be executed.

Let's use the example of backing up files. You may wish to backup "cmnatic"'s  "Documents" every 12 hours. We would use the following formatting: 

```0 *12 * * * cp -R /home/cmnatic/Documents /var/backups/```

An interesting feature of crontabs is that these also support the wildcard or asterisk (```*```). 
If we do not wish to provide a value for that specific field, i.e. we don't care what month, day, or year it is executed -- only that it is executed every 12 hours, we simply just place an asterisk.

Crontabs can be edited by using ```crontab -e```, where you can select an editor (such as Nano) to edit your crontab.

![cron2](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/d7a405a0-8441-4718-b889-c73c07263e42)

![cron3](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/41f61f35-370f-4e51-9b6d-632ff68bf431)

<h3>Questions / Answers</h3>

When will the crontab on the deployed instance (10.10.61.194) run?

```@reboot```


Introducing Packages & Software Repos

When developers wish to submit software to the community, they will submit it to an  "apt" repository. 
If approved, their programs and tools will be released into the wild. 
Two of the most redeeming features of Linux shine to light here: User accessibility and the merit of open source tools.

When using the ```ls``` command on a Ubuntu 20.04 Linux machine, these files serve as the gateway/registry.

![apt1](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/8495cf9e-46f9-426b-b452-4d54912e9b7e)

![apt2](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/73032a2a-b74e-4a2d-9c5f-2571e3a168d0)


Whilst Operating System vendors will maintain their own repositories, you can also add community repositories to your list! This allows you to extend the capabilities of your OS. 
Additional repositories can be added by using the ```add-apt-repository``` command or by listing another provider! 
For example, some vendors will have a repository that is closer to their geographical location.


Maintaining Your System: Logs

We briefly touched upon log files and where they can be found in Linux Fundamentals Part 1. However, let's quickly recap. Located in the /var/log directory, these files and folders contain logging information for applications and services running on your system. The Operating System  (OS) has become pretty good at automatically managing these logs in a process that is known as "rotating".

I have highlighted some logs from three services running on a Ubuntu machine:

- An Apache2 web server
- Logs for the fail2ban service, which is used to monitor attempted brute forces, for example
- The UFW service which is used as a firewall

![log1](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/87758855-a9b2-442c-a4da-dda1bec8ff2d)

These services and logs are a great way in monitoring the health of your system and protecting it. Not only that, but the logs for services such as a web server contain information about every single request - allowing developers or administrators to diagnose performance issues or investigate an intruder's activity. For example, the two types of log files below that are of interest:

- access log
- error log

![log2](https://github.com/schoto/THM-Complete-Beginner/assets/69323411/b6db5d6d-b141-4dd4-b8e7-c55ebdc3880e)



