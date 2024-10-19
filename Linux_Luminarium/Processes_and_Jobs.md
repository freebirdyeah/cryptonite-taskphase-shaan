# Processes and Jobs

Module Description: To learn what are processes/jobs and how to interact with them


## Listing Processes

> NOTE: `ps -ef` and `ps aux` are both quite similar and show us all of the running processes in 'full format'

Challenge Statement says that the `/challenge/run` has been renamed to a random filename which can be found running in the process list to get the flag we need to find the file and execute it to get the flag:-

```
~$ ps -ef
```

We get:-

```
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 06:49 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init /run/dojo/bin/
root           7       1  0 06:49 ?        00:00:00 /run/dojo/bin/sleep 6h
root          68       1  0 06:49 ?        00:00:00 /challenge/12884-run-19237
root          72      68  0 06:49 ?        00:00:00 sleep 6h
hacker        73       0  0 06:49 pts/0    00:00:00 /run/dojo/bin/ssh-entrypoint
hacker       112      73  0 06:58 pts/0    00:00:00 ps -ef
```

on running `~$ /challenge/12884-run`:-

```
Yahaha, you found me! Here is your flag:
pwn.college{IDLo9Yp8PpflD0TxbcqGHlEleS9.dhzM4QDL2MDO0czW}

Now I will sleep for a while (so that you could find me with 'ps').
```


## Killing Processes


The challenge statement instructs us to kill the process `/challenge/dont_run` and then execute `/challenge`. First we can find `/challenge/dont_run` process by using `grep` on `ps -ef` output then check the PID and kill it.


```
~$ ps -ef | grep dont_run
```

which gives us:-

```
hacker        73      71  0 07:06 ?        00:00:00 /challenge/dont_run
hacker        93      75  0 07:06 pts/0    00:00:00 grep --color=auto dont_run
```

we can see that the PID of `/challenge/dont_run` is `73`, now we kill the process:-

```
~$ kill 73
~$ /challenge/run
```

flag: `pwn.college{8VDSyVRs4h8q5DvZ5LJ7jAoVEMg.dJDN4QDL2MDO0czW}`


## Interrupting Processes

The challenge statement instructs us to run `/challenge/run` and then get the flag by interrupting the process. The process can be interrupted by the hotkey `Ctrl-C`

```
~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember,
you can force me to exit with Ctrl-C. Try it now!
```

on `^C` we get the flag.

flag: `pwn.college{UmUxLblDuj6uTW7ESCU_TbNZo7N.dNDN4QDL2MDO0czW}`


## Suspending Processes

The challenge statement instructs us to run `/challenge/run` and then suspend the process with `Ctrl-Z` and then run `/challenge/run` again to get the flag:-

```
:~$ /challenge/run
```

gives:-

```
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          82      65  0 08:21 pts/0    00:00:00 bash /challenge/run
root          84      82  0 08:21 pts/0    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can
background me with Ctrl-Z or, if you're not ready to do that for whatever
reason, just hit Enter and I'll exit!
```

on `^Z`:-

```
[1]+  Stopped                 /challenge/run
```

now on running `~$ /challenge/run` again we get:-


```
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          82      65  0 08:21 pts/0    00:00:00 bash /challenge/run
root          89      65  0 08:22 pts/0    00:00:00 bash /challenge/run
root          91      89  0 08:22 pts/0    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:

pwn.college{cQEXStqsHYioaFPko7IkKG-YeVC.dVDN4QDL2MDO0czW}
```


## Resuming Processes

The challenge statement instructs us to run `/challenge/run` then suspend the process and then restart the process to get the flag. This can be done in simple steps:-

```
~$ /challenge/run
```

we get:-

```
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with
the 'fg' command! Or just press Enter to quit me!
```

on `^Z` we get:-

```
[1]+  Stopped                 /challenge/run
```

on `fg /challenge/run` we get:-

```
/challenge/run

I'm back! Here's your flag:
pwn.college{oNVNVF1W6LPTZp2iCjJKY_cfSty.dZDN4QDL2MDO0czW}

Don't forget to press Enter to quit me!
```

## Backgrounding Processes

In this Challenge, we basically need to have two processes of `/challenge/run` going on in the same terminal. We can do this by using the `bg` command

first we run `/challenge/run`:-

```
~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         148 S+   bash /challenge/run
root         150 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the
background, and then launch a new version of me! You can background me with
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to
do that for whatever reason, just hit Enter and I'll exit!
```

after `^Z` and suspending the process, we run `/challenge/run` in the background using `bg`:-

```
~$ bg /challenge/run
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out.
```

Now we run `/challenge/run` again:-

```
~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         148 S    bash /challenge/run
root         158 S    sleep 6h
root         159 S+   bash /challenge/run
root         161 R+   ps -o user=UID,pid,stat,cmd


Yay, I found another version of me running in the background! Here is the flag:
pwn.college{QBExrM5esnKb3uSMn0uy2rlHZFM.ddDN4QDL2MDO0czW}
```


## Foregrounding Processes

On running `~$ /challenge/run` we see what the challenge wants from us:-


```
To pass this level, you need to suspend me, resume the suspended process in the
background, and *then* foreground it without re-suspending it! You can
background me with Ctrl-Z (and resume me in the background with 'bg') or, if
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
```

On suspending the process using `^Z` and backgrounding the process using `bg` we see:-

```
~$ bg /challenge/run
[1]+ /challenge/run &



hacker@processes~foregrounding-processes:~$ Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out. After that, resume me into the foreground with 'fg';
I'll wait.
```

now we foreground the same process using `fg`;-

```
~$ fg /challenge/run
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!
```

flag: `pwn.college{ElIZ509BmWi47wYyeUbARLmNfRn.dhDN4QDL2MDO0czW}`


## Starting Backgrounded Processes

Challenge instructs us to run the `/challenge/run` in the background to get the flag which can be done by appending a `&` to the command:-

```
~$ /challenge/run &
```

flag: `pwn.college{sAxplosDxGXJAfKRfaXkMW3quQ9.dlDN4QDL2MDO0czW}`


## Process Exit Codes

Challenge instructs us to retrieve the exit code returned by `/challenge/get-code` and then run `/challenge/submit-code` with that error code as an argument:-

```
~$ /challenge/get-code
```

we get:-

```
Exiting with an error code!
```

which we can find out by:-

```
~$ echo $?
231
```

now to get the flag:-

```
~$ /challenge/submit-code 231
```

flag: `pwn.college{oufphn6KBe0QfSCkVP4kz9Cw5Nx.dljN4UDL2MDO0czW}`


