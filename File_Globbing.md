# File Globbing 

Module Description: to learn file globbing which allows us to reference files without typing entire file paths

## Matching with *

The challenge instructs us to `cd` (using file globbing) to `/challlenge` by keeping the argument to at most four characters to execute the `run` file to obtain the flag. This can be done by:-

```
~$ cd /ch*
/challenge$ ./run
```

flag: `pwn.college{wUBI7ti0aGLNeTH8kOey0Wzm0JO.dFjM4QDL2MDO0czW}`

## Matching with ?


Challenge statement instructs us to `cd` to `/challenge` directly by replacing 'c' and 'l' characters with '?' in the argument

This can be done by:-

```
~$ cd /?ha??enge
/challenge$ ./run
```

flag: `pwn.college{QFa_i-RvY531crwQ7x-EdkjWH7d.dJjM4QDL2MDO0czW}`

## Matching with []

Challenge instructs us to `cd` into `/challenge/files` and run `/challenge/run` with an argument that bracket-globs into `file_b`, `file_a`, `file_s` & `file_h`

on `cd`ing to `/challenge/files` and running `echo Look: file_[absh]` we see:-

```
Look: file_a file_b file_h file_s
```

now on running `/challenge/files$ ./run file_[absh]` we get the flag.

flag: `pwn.college{MSbSsexDrcMlDkVkW0mJ4nPFCJ_.dNjM4QDL2MDO0czW}`

## Matching paths with []

similar to the previous challenge except this time we have to enter an argument which globs into the absolute paths to `file_b`, `file_a`, `file_s` and `file_h` from our home directory

flag will be obtained on running:-

```
~$ /challenge/run /challenge/files/file_[absh]
```

flag: `pwn.college{gh1HFz_03h3yNdQyQPakocOYWI1.dRjM4QDL2MDO0czW}`

## Mixing globs

the challenge instructs to write a command with `/challenge/files` as PWD using file globbing such that it will math the files `challenging`, `educational` & `pwning`


looking for files using `echo Look: [cep]*` and we get:-

```
Look: challenging educational pwning
```

which proves passing `[cep]*` as the argument is enough.

running, `/challenge/files$ /challenge/run [cep]*` we get the flag.

flag: `pwn.college{ICAmHDmI0M2bPjKfydPFAjx6CNp.dVjM4QDL2MDO0czW}`

> NOTE: running `echo Look: [cep]` didn't give the expected result because of the missing `*` at the end which looks for files beginning with either 'c', 'e' or 'p' and searches further.

## Exclusionary globbing

similar to the previous challenge, except for exclusionary globbing, challenge statement directs us to find files not starting with 'p', 'w' or 'n'. The challenge can be done by:-

```
~$ cd /challenge/files
/challenge/files$ /challenge/run [!pwn]*
```

flag: `pwn.college{4p5MGZTJaiOUA_HCdzXOP0ghupw.dZjM4QDL2MDO0czW}`
