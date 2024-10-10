# Practicing Piping

Module Description: to learn how to handle output in the command line

## Redirecting output

Challenge statement asks us to put the word 'PWN' to a file `COLLEGE`. This can be done by:-

```
~$ echo PWN > COLLEGE
```

flag: `pwn.college{QgaLI6vCZ0j0VKxwQljWDG40Aqe.dRjN1QDL2MDO0czW}`

## Redirecting more output

Challenge asks us to redirect the output of `/challenge/run` to a file `myflag` to obtain the flag:-

```
~$ /challenge/run > myflag
~$ cat myflag
```

flag: `pwn.college{EISf170IId8hJfBoM0mnK7nk96C.dVjN1QDL2MDO0czW}`

## Appending output

The challenge statement asks us to write the flag's first half to `the-flag` file by putting the output once after running the `/challenge/run` file and again append the output of `/challenge/run` to `the-flag` file to get the second half of the flag

```
~$ /challenge/run > the-flag
~$ /challenge/run >> the-flag
```

and we will get:-

```
 |
\|/ This is the first half:
 v
pwn.college{wXMBt50g4HxKddnoXALcGrNzhZ8.ddDM5QDL2MDO0czW}
                              ^
     that is the second half /|\
                              |
```

## Redirecting errors

The challenge statement tells us to redirect the output of `/challenge/run` to `myflag` and the errors to `instructions` to obtain the flag.

This can be done by:-

```
~$ /challenge/run > myflag 2> instructions
~$ cat myflag
```

flag: `pwn.college{I77ANsWuAFNQS8L1GZKshpCE73e.ddjN1QDL2MDO0czW}`

## Redirecting input

The challenge instructs us to redirect the `PWN` file to `/challenge/run`, The `PWN` file must contain the value "COLLEGE". This can be done by:-

```
~$ echo COLLEGE > PWN
~$ /challenge/run < PWN
```

flag: `pwn.college{8AQKA675gw2NAeP9B7TpgbpNmj5.dBzN1QDL2MDO0czW}`


## Grepping stored results

The challenge instructs us to do the following:-

> 1. Redirect the output of /challenge/run to /tmp/data.txt. 
> 2. This will result in a hundred thousand lines of text, with one of them being the flag, in /tmp/data.txt.
> 3. Grep that for the flag!

which can be done by:-

```
~$ /challenge/run > /tmp/data.txt
~$ grep pwn /tmp/data.txt
```

which will give us this as output:-

```
pwning
pwn.college{UrSLay8QV9x8eAqTkPjZId3cQGI.dhTM4QDL2MDO0czW}
pwn
pwns
pwned
```

flag: `pwn.college{UrSLay8QV9x8eAqTkPjZId3cQGI.dhTM4QDL2MDO0czW}`

## Grepping live output

Challenge statement instructs us to pipe the contents of `/challenge/run` file to `grep` command to search for the flag:-

```
~$ /challenge/run | grep pwn
```

flag: `pwn.college{YYuOj2y0HV8_lhm97Dit1V493Aj.dlTM4QDL2MDO0czW}`

> NOTE: `|` only redirects the stdout! 

## Grepping errors

The challenge instructs us to pipe stderr to stdout and filter stdout using `grep` to find the flag

```
~$ /challenge/run 2>&1 | grep pwn
```

which will give us this as output:-

```
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{MahbLMLNbRvSfqqkJRK2MPVolJM.dVDM5QDL2MDO0czW}
pwning
pwn
pwns
pwned
```

flag: `pwn.college{MahbLMLNbRvSfqqkJRK2MPVolJM.dVDM5QDL2MDO0czW}` 

## Duplicating piped data with tee

The challenge statement directs us to pipe `/challenge/pwn` to `/challenge/college` but we will need to intercept data during piping using `tee` function to see what the `pwn` file requires

```
~$ /challenge/pwn | tee txt | /challenge/college
```

which will give us:-

```
Processing...
The input to 'college' does not contain the correct secret code! This code
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the
output of 'pwn' and figure out what the code needs to be.
```
the output of `pwn` was already saved into `txt` file, on reading it we see:-

```
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "s4ImzLKB"
```

Now we pipe the file `/challenge/pwn` file into `/challenge/college`:-

```
~$ /challenge/pwn --secret s4ImzLKB | /challenge/college
```
flag: `pwn.college{s4ImzLKBLWWxifNA4dt-m25k_h3.dFjM5QDL2MDO0czW}`

## writing to multiple programs

The challenge instructs us to write the ouput of `/challenge/hack` to the input of `/challenge/planet` & `/challenge/the`. This can be done by Process Substitution:-

```
~$ /challenge/hack | tee >(/challenge/the) >(/challenge/planet)
```

> Explanation: `/challenge/hack` file's output is piped to `/challenge/the` and `/challenge/planet` programs' (randomly hooked) input files using and the flag is obtained

> NOTE: Process Substitution creates a process thats run a command and inserts some input to it as directed

flag: `pwn.college{0jePM5Bqk30kjY6S0QUDUPfzyeG.dBDO0UDL2MDO0czW}`

## split-piping stderr and stdout

The challenge instructs us to write the contents of `/challenge/hack` file putting stderr to `/challenge/the` and stdout to `/challenge/planet`. This can be done by:-

```
~$ /challenge/hack 2> >(/challenge/the) | /challenge/planet
```

> NOTE: Initally I came up with: `/challenge/hack 2> /challenge/the | /challenge/planet` which wasn't working since I was trying to write stderr to `/challenge/the` instead of putting stderr into it's input using Process substitution

> NOTE 2: `|` using a pipe ONLY directs stdout. If stderr needs to be piped as well then `2>&1` or `2>` need to be used
