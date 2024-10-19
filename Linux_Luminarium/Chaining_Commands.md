# Chaining Commands

Module Description: To learn how to chain commands aside from piping


## chaining with semicolons

Challenge Instructs us to run `/challenge/pwn` and then `/challenge/college` chaining them with a semicolon `;` 


```
~$ /challenge/pwn; /challenge/college
```

flag: `pwn.college{grp5MPbRez7ntZZYzn_qIDHK5T6.dVTN4QDL2MDO0czW}`


## your first shell script

This challenge instructs us to run `/challenge/pwn` and then `/challenge/college` via a shell script `x.sh` and then run it:-

```
~$ touch x.sh
~$ nano x.sh
~$ bash x.sh
```

flag: `pwn.college{8g958CRShueqVRpTcr7mJ8i9AQM.dFzN4QDL2MDO0czW}`


## redirecting script output

This challenge instructs us to create a script that calls the `/challenge/pwn` command followed by the `/challenge/college` command, and pipe the output of the script into a single invocation of the `/challenge/solve` command

We can use our old `x.sh` file:-

```
~$ bash x.sh | /challenge/solve
```

flag: `pwn.college{UcYvOsYeywbwZ2he-wEQD5-1792.dhTM5QDL2MDO0czW}`


## executable shell scripts

The challenge asks us to make the shell script executable and then run it without the `bash` command


```
~$ touch x.sh; echo /challenge/solve > x.sh; chmod +x x.sh; ./x.sh
```

flag: `pwn.college{kL1xk3Q4s3UiuiX-JJMSIZwLAXb.dRzNyUDL2MDO0czW}`
