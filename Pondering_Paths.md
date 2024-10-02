# Pondering Paths

_Module Description: To know the basics of linux filepaths and how to navigate through the filesystem_


## The Root

> Challenge Statement: In this level, we've added a program right in /, called pwn, that will give you the flag. All you need to do for this level is to invoke this program! 

> You can invoke a program by providing its path on the command line. In this case, you'll be giving the exact path, starting from /, so the path would be /pwn. This style of path, one that starts with the root directory, is referred to as an "absolute path". 

> Start the challenge, launch a terminal, invoke the pwn program using its absolute path, and Capture that Flag! Good luck!

`pwn` can't be invoked straight from the `~` home directory as it resides in the `/` root directory. 

Therefore, flag will only be obtained after `$ /pwn` is ran

Flag: `pwn.college{gtXwtCKvE5AJA4Rt7QdBhWCP7Jj.dhzN5QDL2MDO0czW}`

## Program and absolute paths

> Challenge Statement: Except for in the previous level, challenges in pwn.college are in the challenge directory and the challenge directory is, in turn, right in the root directory (/). The path to the challenge the directory is, thus, /challenge. The name of the challenge program in this level is run, and it lives in the /challenge directory. Thus, the path to the run challenge program is /challenge/run.

> This challenge again requires you to execute it by invoking its absolute path. You'll want to execute the run file that is in the challenge directory that is, in turn, in the / directory. If you invoke the challenge correctly, it will give you the flag. Good luck!

This time the `run` file is in the `challenge` directory which is in the `/` root directory. To execute the `run` file regardless of the present working directory, we need to invoke it using it's absolute path which will be `/challenge/run`

On running `$ /challenge/run` we will get the flag.

Flag: `pwn.college{44cULa5PkZeUip8FGjQtGBV-HWJ.dVDN1QDL2MDO0czW}`

## Position thy self

> Challenge Statement: You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

> `hacker@dojo:~$ cd /some/new/directory`
> `hacker@dojo:/some/new/directory$ cd /some/new/directory`

> This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

> As an aside, now you can see what the ~ was in the prompt! It shows the current that your shell is located at.

> This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

On executing `$ /challenge/run` we receive 

```

Incorrect...
You are not currently in the /proc/206 directory. 
Please use the 'cd' utility to change directory appropriately.

```

We need to cd to the `/proc/206/` which we can do by `$ cd /proc/206/`

Now from this directory, we need to execute the `run` file by putting the absolute path: `/proc/206$ /challenge/run`

We will finally get the flag: `pwn.college{svl8gBmayAHVrQkQhk_rqPMLWxi.dZDN1QDL2MDO0czW}`

## Position elsewhere

> Challenge Statement: This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

Similar to the previous challenge, 

On executing `$ /challenge/run` we receive 

```
Incorrect...
You are not currently in the /sys/kernel directory.
Please use the `cd` utility to change directory appropriately.
```

We `cd` to the `/sys/kernel/` directory then run the `/challenge/run` file

Flag: `pwn.college{sd8x2o0whUNDpYNBH_QHai4L6UD.ddDN1QDL2MDO0czW}`

## Position yet elsewhere

*EXACTLY SAME AS 'Position elsewhere' challenge (have the same required current working directory)*

Flag: `pwn.college{Y5WM1tKbhnihWn1Cpb9ZhADi_4o.dhDN1QDL2MDO0czW}`

## Implicit relative paths, from /

> Challenge Statement: You'll need to run /challenge/run using a relative path while having a current working directory of /. For this level, I'll give you a hint. Your relative path starts with the letter 'c'

As the challenge description says, we need to run `/challenge/run` using a relative path while `/` is our cwd.

Run:

```
cd `/`
challenge/run
```

Flag: `pwn.college{YnX2FRVz8pZLV6ETY8HH16bbP86.dlDN1QDL2MDO0czW}`

## Explicit relative paths, from /

> Challenge Statement: Previously, your relative path was "naked": it directly specified the directory to descend into from the current directory. In this level, we're going to explore more explicit relative paths.

> In most operating systems, including Linux, every directory has two implicit entries that you can reference in paths: . and ... The first, ., refers right to the same directory, so the following absolute paths are all identical to each other:

> `/challenge`
> `/challenge/.`
> `/challenge/./././././././././`
> `/./././challenge/././`
>
> The following relative paths are also all identical to each other:

> `challenge`
> `./challenge`
> `./././challenge`
> `challenge/.`
> Of course, if your current working directory is /, the above relative paths are equivalent to the above absolute paths.

> This challenge will get you using . in your relative paths. Get ready!

Just like the previous challenge, a relative path from `/` is required starting from `.` which denotes the current working directory as per the statement

```
cd /
./challenge/run
```

Flag: `pwn.college{wLTb8AqVbdv-TwdLyrlj9oESQQf.dBTN1QDL2MDO0czW}`

## Implicit relative path

> Challenge Statement: In this level, we'll practice refering to paths using . a bit more. This challenge will need you to run it from the /challenge directory. Here, things get slightly tricky.

> Linux explicitly avoids automatically looking in the current directory when you provide a "naked" path. Consider the following:

> `hacker@dojo:~$ cd /challenge`
> `hacker@dojo:/challenge$ run`

> This will not invoke /challenge/run. This is actually a safety measure: if Linux searched the current directory for programs every time you entered a naked path, you could accidentally execute programs in your current directory that happened to have the same names as core system utilities! As a result, the above commands will yield the following error:

> `bash: run: command not found`
> We'll explore the mechanisms behind this concept later, but in this challenge, will learn how to explicitly use relative paths to launch run in this scenario. The way to do this is to tell Linux that you explicitly want to execute a program in the current directory, using . like in the previous levels. Give it a try now!

Challenge statement says that if we `cd` into `/challenge` directory we can't execute `/challenge/run` file just by `$ run`, we will need to `$ ./run` to execute that file. This is a safety measure to prevent those programs from executing which have the same name as core system utilities.

```
$ cd /challenge/
$ ./run
```
Flag: `pwn.college{QrPc1HGdwk0UDa_HXOdLtt8w4rt.dFTN1QDL2MDO0czW}`

## Home sweet home

> Challenge Statement: In this challenge, /challenge/run will write a copy of the flag to any file you specify as an argument on the commandline, with these constraints:

> 1. Your argument must be an absolute path.
> 2. The path must be inside your home directory.
> 3. Before expansion, your argument must be three characters or less.

The challenge statement says on running `$ /challenge/run` the flag will be written to any file specified as the argument on the aforementioned 3 conditions. 

```
:~ $ touch a
:~ $ /challenge/run/ ~/a
```
Flag: `pwn.college{Q6UHbk3jgg01Rys6LHeDGDeR0vE.dNzM4QDL2MDO0czW}` 

