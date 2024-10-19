# Untangling Users

Module Description: To learn more about users on Linux Systems


## becoming root with su

Challenge describes the `su` command to us and instructs us to run the command in the terminal and enter the password `hack-the-planet` to become the root and read the flag:-


```
~$ su
Password: 

/home/hacker# cat /flag
```

flag: `pwn.college{oitgsDj2SLbZAcUFjg8x4F1uZDO.dVTN0UDL2MDO0czW}`


## other users with su

The challenge instructs us to use the `su` command to switch to another user `zardus` and then run `/challenge/run` to get the flag, this can be done by:-


```
hacker@users~other-users-with-su:~$ su zardus
Password:
zardus@users~other-users-with-su:/home/hacker$ /challenge/run

```

flag: `pwn.college{MuZV5TZ0xzHAG15P1WNAKvTCAYT.dZTN0UDL2MDO0czW}`


## cracking passwords

This challenge gives us a leaked `/etc/shadow` file which contains users and their encrypted passwords, we are instructed to crack the password using `John The Ripper` tool by passing the leaked file (which is `/challenge/shadow-leak`) as the argument then change user into `zardus` and run the `/challenge/run` file to obtain the flag:-

first we need to crack the password:-

```
~$ john /challenge/shadow-leak

Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
aardvark         (zardus)
1g 0:00:00:20 100% 2/3 0.04972g/s 289.5p/s 289.5c/s 289.5C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

we can see user `zardus` has the password `aardvark`, now we `su` into `zardus`:-

```
~$ su zardus
Password: 		
/home/hacker$ /challenge/run
```

flag: `pwn.college{MimxhWlAOtmSKV4uaK3krwy9LG3.ddTN0UDL2MDO0czW}`

## using sudo

In this challenge with the help of `sudo` we can directly read the `/flag` file to get the flag

```
~$ sudo cat /flag
```

flag: `pwn.college{05l3enHuxrY_FFoSWs96ukYEZmI.dhTN0UDL2MDO0czW}`
