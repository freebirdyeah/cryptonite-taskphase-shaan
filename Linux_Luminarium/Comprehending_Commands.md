# Comprehending Commands

_Module Description: To learn about useful linux commands_

## cat: not the pet, but the commmand

Just reading the `flag` file using `$ cat flag` will give us the flag.

Flag: `pwn.college{0hGLYpCW5nFMiCnj0jjp6CyCs-8.dFzN1QDL2MDO0czW}`

## catting absolute path

The challenge statement guides us to use absolute path for catting `flag` file by passing it as an argument for the `cat` command. 

Running `$ cat flag` won't work as the filepath for flag file is `/flag` i.e. flag file is in `/` root directory

Simply, `$ cat /flag` will give us the flag

Flag: `pwn.college{kjq6r2PILE9fIFnaEg6DuWDlcfk.dlTM5QDL2MDO0czW}`

## more catting practice

`cd`ing into the specified `/lib/x86_64-linux-gnu/glib-2.0/` isn't allowed. Hence, absolute path must be used to get the flag

`$ cat /lib/x86_64-linux-gnu/glib-2.0/flag` will give us the flag

Flag: `pwn.college{svVRc-i0P_sArq5qnPlxDAP7QOO.dBjM5QDL2MDO0czW}`

## grepping for a needle in a haystack

This time directly catting the `/challenge/data.txt` file won't work as it has too many lines of text. Using `grep` we will only get those strings which have SEARCH_STRING in them.

```
cd /challenge
grep pwn.college data.txt
````

since the flag starts with 'pwn.college', we will get the flag as the output
Flag: `pwn.college{kyhfEyjsNiVTgM6rcPlE24whjOc.ddTM4QDL2MDO0czW}`

## listing files

`ls` command can be used to list all files present in a directory. According to the challenge statement, the `/challenge/run` file has been named as something else. Hence, to find it we will havr to `cd` to `/challenge/` directory and look for the file.

```
cd /challenge/
ls
./8580-renamed-run-29739
```
Flag: `pwn.college{cABn1v7zkNnuMRFG5y93DR4SH3-.dhjM4QDL2MDO0czW}`

## touching files

Files can be created by using the `touch` command. `/challenge/run` can't be executed directly here as to get the flag we need to make two files with paths `/tmp/pwn` & `/tmp/college`

```
touch /tmp/pwn
touch /tmp/college
/challenge/run
```

Flag: `pwn.college{UshsK6pOk3yZFeOHdnuq_Mjc7Xc.dBzM4QDL2MDO0czW}`

## removing files

Files can be removed by using the `rm` command. The challenge statement tells us to remove `delete_me` me file under the home directory then run `/challenge/check` to get the flag

```
rm delete_me
/challenge/check
```

Flag: `pwn.college{wCUcknsMNfX7uT7fCagIJfYmNGH.dZTOwUDL2MDO0czW}`

## hidden files

Files which are dot-prepended aren't shown by the `ls` command by default. To see them `ls` has to be invoked along with `-a` flag. We need to find a dot-prepended file in `/` which will be the flag 

```
cd /; ls -a
cat .flag-274361953010690
```

Flag: `pwn.college{8NLLRCpX7Jx0F4nUQzSYF3Ob1Q-.dBTN4QDL2MDO0czW}`

## An epic filesystem quest

In this challenge, the hidden flag file will be buried somewhere in the `/` root directory and we have to find it using clues starting with the files in root directory.

On `cd`ing into `/` and running `ls`, A file named `INSIGHT` is found. On `cat`ting it:-

```
Lucky listing!
The next clue is in: /opt/linux/linux-5.4/drivers/net/wireless/realtek/rtlwifi/rtl8192ce

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
```

On running `ls /opt/linux/linux-5.4/drivers/net/wireless/realtek/rtlwifi/rtl8192ce`, I see a file named `INFO-TRAPPED`, on running `cat INFO_TRAPPED` I get:-

```
Yahaha, you found me!
The next clue is in: /opt/linux/linux-5.4/Documentation/admin-guide/blockdev

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
```

On `cd`ing into `/opt/linux/linux-5.4/Documentation/admin-guide/blockdev` and running `ls -a` I see a `.HINT` file, `cat .HINT` shows:-

```
Yahaha, you found me!
The next clue is in: /usr/lib/ruby/2.7.0/rubygems/ssl_certs

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
```
	
`cd` into `/usr/lib/ruby/2.7.0/rubygems/ssl_certs` and running `ls -a`, I see a file named `DOSSIER`. `cat DOSSIER` gives:-

```
Tubular find!
The next clue is in: /opt/ghidra/Ghidra/Processors/DATA/ghidra_scripts

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
```

`cd` into `/opt/ghidra/Ghidra/Processors/DATA/ghidra_scripts` and running
`ls`, I find a file named `BRIEF`, `cat BRIEF` gives:-

```
Great sleuthing!
The next clue is in: /usr/lib/python3/dist-packages/openid/__pycache__
```

`cd` into `/usr/lib/python3/dist-packages/openid/__pycache__` and running `ls`, I find a file named `LEAD`, `cat LEAD` gives:-

```
Yahaha, you found me!
The next clue is in: /usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/TeX/Main/Italic
```

`cd` into `/usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/TeX/Main/Italic` and running `ls` I find a file named `SNIPPET`, `cat SNIPPET` gives:-
```
Tubular find!
The next clue is in: /usr/lib/ruby/2.7.0/rdoc/rd
```

`cd` into `/usr/lib/ruby/2.7.0/rdoc/rd` and running `ls` I find a file named `NUGGET`, `cat NUGGET` yields:-

```
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{kT9KU8X_39lUM_wYmYRNCuv9XWo.dljM4QDL2MDO0czW}
```


## Making directories

The challenge statement instructs us to make a directory `/tmp/pwn` and make a file `college` in it to obtain the flag from `/challenge/run`

This can be simply done by:-

```
~$ mkdir /tmp/pwn
~$ touch /tmp/pwn/college
~$ /challenge/run
```

flag: `pwn.college{YEXXcqC7XaRvUlTNcfriXFkR2tF.dFzM4QDL2MDO0czW}`

## Finding files

> NOTE: The `find` command searches for every file in the specified directory if a search criteria isn't specified, if the directory isn't specified as well then current working directory is taken

The challenge statement instructs us to find a file `flag` which is in some random directory in the filesystem (NOTE: Challenge Statement says that multiple files or directories can exist by this name and we can also get permission denied errors along the way). This can be done by:-

```
$ find / -name flag > find.txt 2>&1; grep -v "Permission denied" find.txt
```

Which will give us all possible permitted files or directories in `/` directory:-

```
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/usr/local/share/radare2/5.9.5/flag
/opt/linux/linux-5.4/include/linux/input/flag
/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
/opt/radare2/libr/flag
/nix/store/1yagn5s8sf7kcs2hkccgf8d0wxlrv5sz-radare2-5.9.0/share/radare2/5.9.0/flag
/nix/store/pmvk2bk4p550w182rjfm529kfqddnvh3-python3.11-pwntools-4.12.0/lib/python3.11/site-packages/pwnlib/flag
```

Flag: `pwn.college{0lFN5W3exT50ZPRBB2xFjSAq-s4.dJzM4QDL2MDO0czW}`

Now checking each of these we will see that some of these are directories (we are looking for a file not a directory), On checking `cd /opt/linux/linux-5.4/include/linux/input/flag`:

`cd: /opt/linux/linux-5.4/include/linux/input/flag: Not a directory`

Which means it's a file, On catting `/opt/linux/linux-5.4/include/linux/input/flag` we get the flag: 

`pwn.college{0lFN5W3exT50ZPRBB2xFjSAq-s4.dJzM4QDL2MDO0czW}`

> NOTE: I wanted to come up with a command which directly shows us all valid files/directories that the `find` command finds while neglecting all the non-permitted directories/files here is the explanation of the command

> The command searches the entirety of the filesystem for files/directories having the name 'flag' and quietly pipes the results into a file `find.txt` (`2>&1` directs both the stdout and stderr to the file itself) and then uses `grep` to get only those strings without the substring 'Permission denied'

## Linking files

Soft links a.k.a symlinks or symbolic links can be created using `ln -s [target file] [file to be linked to target file]`

The challenge statement asks us to get `/flag` by executing `/challenge/catflag` however, `/challenge/catflag` will read out `/home/hacker/not-the-flag`

```
~$ /challenge/catflag

About to read out the /home/hacker/not-the-flag file!
cat: /home/hacker/not-the-flag: No such file or directory
```
We can trick the `/challenge/catflag` file to give us the flag if we successfuly symlink `not-the-flag` file to `/flag` file

```
~$ ln -s /flag not-the-flag
~$ /challenge/catflag

About to read out the /home/hacker/not-the-flag file!
pwn.college{Q4imH6UhpRybDxpEywk5Mk3vHMS.dlTM1UDL2MDO0czW}
```

> NOTE: On noticing, `not-the-flag` doesn't exists, I entered `~$ touch not-the-flag` and then executed `~$ ln -s /flag not-the-flag` which gave the error: `ln: failed to create symbolic link 'not-the-flag': File exists` which happened because the file `not-the-flag` already existed and `ln` can't overwrite existing file or symlinks. In short it seems to me, if you're creating a symlink, the file that you want to link shouldn't exist beforehand.

> This Problem was resolved when `~$ ln -s -f /flag not-the-flag` was executed as the `-f` instructs `ln` to overwrite.

> NOTE 2: `/flag` was unreadable, however it contents could be accessed just by making a symlink to it. This seems to be some kind of a security flaw.
