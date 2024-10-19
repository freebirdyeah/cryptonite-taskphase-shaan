# Digesting Documentation

Module Description: learning how to look for help by reading documentation

## Learning from Documentation

> The following is given as documentation:-
> Welcome to the documentation for `/challenge/challenge`! To properly run this program, you will need to pass it the argument of `--giveflag`. Good luck!

simply run:-

`~$ /challenge/challenge --giveflag`

flag: `pwn.college{cBu7YCFTaaCiX8EeWnmjbnRdA3m.dRjM5QDL2MDO0czW}`

## Learning complex usage

Following the given documentation:-

> Welcome to the documentation for `/challenge/challenge`! This program allows you to print arbitrary files to the terminal, when given the `--printfile` argument. The argument to the `--printfile` argument is the path of the flag to read. For example, `/challenge/challenge --printfile /challenge/DESCRIPTION.md` will print out the description of the level

simply run:-

`~$ /challenge/challenge --printfile /flag`

flag: `pwn.college{cZ16XyrVaH5myt4_wMpv3m8K7uy.dVjM5QDL2MDO0czW}`

## reading manuals

`man [CMD]` can be used to look up a centralised database of manual pages of commands. As per the challenge we need to look up `man challenge`

```
~$ man challenge
```

which will give us:-


```
CHALLENGE(1)                                 Challenge Commands                                CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --vtucoq NUM
              print the flag if NUM is 564

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>
--More--
```

following the documentation we can get the flag by running:-

```
~$ /challenge/challenge --vtucoq 564
```

flag: `pwn.college{MvXt5IucoDqIqOpQ6Ev4qB_muVR.dRTM4QDL2MDO0czW}`

## searching manuals

we can search man pages by entering `/` and entering `n` and `N` to search it normally and backwards respectively, in the challenge we are supposed to go through `man challenge` and find the correct argument for the flag.

On searching by enetering `/` and putting `flag` as searchword then followed by repeated `n` I find:-

```
--aftlzd
              This argument will give you the flag!
```

on running `/challenge/challenge --aftlzd` we get the flag!

flag: `pwn.college{gq5WLMY_A5DCJUs3cGJ5LRyGs5z.dVTM4QDL2MDO0czW}`

## searching for manuals

as instructed, on running: `man man` I see:-

```
man -k printf
           Search the short descriptions and manual page names for the keyword printf  as  regular  expres‐
           sion.  Print out any matches.  Equivalent to apropos printf.
```

as per docs found, on running `~$ man -k challenge` I get:-

```
odrufckvmd (1)       - print the flag!
```

then I run `man odrufckvmd`:-

```
CHALLENGE(1)                                 Challenge Commands                                CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --odrufc NUM
              print the flag if NUM is 364

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>
```

to get the flag run: `/challenge/challenge --odrufc 364`

flag: `pwn.college{o36LCdGCGrOWVSufRJCc4-kUvUm.dZTM4QDL2MDO0czW}`

## helpful programs

as per the challenge instructions on running `~$ /challenge/challenge -h` to find help we get:-


```
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag
```

now on running `/challenge/challenge -p` we will get the required value to make the program print the flag:-

```
The secret value is: 537
```

now on running `/challenge/challenge -g 537` we will get the flag

flag: `pwn.college{gr-loy5d3DapmZBqTlgmvwMUte7.ddjM4QDL2MDO0czW}`

## help for builtins

as directed, on running `~$ help challenge` we get:-

This builtin command will read you the flag, given the right arguments!

```
    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "QNaEgkcO".
```

on running `~$ challenge --secret QNaEgckO` we will get the flag:-

flag: `pwn.college{QNaEgkcOyd_v4Y46GkML7Ip0xJT.dRTM5QDL2MDO0czW}`


