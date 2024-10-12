# Shell Variables

Module Description: To leaarn about usage of variables in shell commands and scripts.


## Printing Variables

Challenge Statement instructs us to print out `$FLAG` to get the flag:-

```
~$ echo $FLAG
```

flag: `pwn.college{sRNMnCU8jcHh_SfFc5jF1McgPjK.ddTN1QDL2MDO0czW}`

> NOTE: `$` always needs to prepended before the variable name to access it


## Setting Variables

Challenge Statement instructs us to set the variable `PWN` to the value `COLLEGE` to get the flag, which is simply done by:-


```
~$ PWN=COLLEGE
```

flag: `pwn.college{4-4huar3LjeF0g8eGD02N_r6ZeM.dlTN1QDL2MDO0czW}`


## Multi-world Variables

Challenge Statement instructs us to set the variable `PWN` to the value `COLLEGE YEAH`, which is a multi-word value. Enclosing 'COLLEGE YEAH' in "" can enable us to do this:-

```
~$ PWN="COLLEGE YEAH"
```

flag: `pwn.college{oVL-HOufup_B6VsEVKO1beqcuAg.dBjN1QDL2MDO0czW}`


## Exporting Variables

Challenge statement asks us to set `PWN` to `COLLEGE` and export it & the variable `COLLEGE` to the value `PWN` and then run `/challenge/run` to get the flag. This can be done by:-

```
~$ PWN=COLLEGE; export PWN
~$ COLLEGE=PWN
~$ /challenge/run
```

flag: `pwn.college{ArRtUu0yUYwbaW4KHqGuvg8KRUj.dJjN1QDL2MDO0czW}`


## Printing Exported Variables

Challenge statement instructs us to run `~$ env` to see all exported variables in our shell. On running the command we see:-

```
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
PWD=/home/hacker
DOJO_AUTH_TOKEN=5af74ecdb446f25385c68e26ea14bec7cfa7834d7cb7add379584223ff3739a9
HOME=/home/hacker
LANG=C.UTF-8
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=00:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.7z=01;31:*.ace=01;31:*.alz=01;31:*.apk=01;31:*.arc=01;31:*.arj=01;31:*.bz=01;31:*.bz2=01;31:*.cab=01;31:*.cpio=01;31:*.crate=01;31:*.deb=01;31:*.drpm=01;31:*.dwm=01;31:*.dz=01;31:*.ear=01;31:*.egg=01;31:*.esd=01;31:*.gz=01;31:*.jar=01;31:*.lha=01;31:*.lrz=01;31:*.lz=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.lzo=01;31:*.pyz=01;31:*.rar=01;31:*.rpm=01;31:*.rz=01;31:*.sar=01;31:*.swm=01;31:*.t7z=01;31:*.tar=01;31:*.taz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tgz=01;31:*.tlz=01;31:*.txz=01;31:*.tz=01;31:*.tzo=01;31:*.tzst=01;31:*.udeb=01;31:*.war=01;31:*.whl=01;31:*.wim=01;31:*.xz=01;31:*.z=01;31:*.zip=01;31:*.zoo=01;31:*.zst=01;31:*.avif=01;35:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:*~=00;90:*#=00;90:*.bak=00;90:*.crdownload=00;90:*.dpkg-dist=00;90:*.dpkg-new=00;90:*.dpkg-old=00;90:*.dpkg-tmp=00;90:*.old=00;90:*.orig=00;90:*.part=00;90:*.rej=00;90:*.rpmnew=00;90:*.rpmorig=00;90:*.rpmsave=00;90:*.swp=00;90:*.tmp=00;90:*.ucf-dist=00;90:*.ucf-new=00;90:*.ucf-old=00;90:
FLAG=pwn.college{kaUGSpzTWddvyrerelf14ae72IM.dhTN1QDL2MDO0czW}
LESSCLOSE=/usr/bin/lesspipe %s %s
TERM=xterm
LESSOPEN=| /usr/bin/lesspipe %s
SHLVL=1
LC_CTYPE=C.UTF-8
PATH=/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
_=/run/workspace/bin/env
```

In the output we can see the `FLAG` variable

flag: `pwn.college{kaUGSpzTWddvyrerelf14ae72IM.dhTN1QDL2MDO0czW}`


## Storing Command Output

Challenge Statement instructs us to read the output of `/challenge/run` into a variable `PWM` then get the flag from the variable, this can be done by:-


```
~$ PWN=$(/challenge/run)
~$ echo $PWN
```

flag: `pwn.college{wlHASxj4DNGJCUAZOcOSFpkxHuf.dVzN0UDL2MDO0czW}`


## Reading Input

Challenge Statement asks us to use `read` command to set the `PWN` variable to the value `COLLEGE`, this can be done by:-

```
~$ read PWN
COLLEGE
```

flag: `pwn.college{o0v-PU1KmeHggNHD8rMvCod_get.dhzN1QDL2MDO0czW}`

> NOTE: `read -p` can be used to specify a prompt to make it easier to read


## Reading Files

Challenge statement asks us to read `/challenge/read_me` into the `PWN` environment variable to obtain the flag. This can be done by:-

```
~$ export PWN
~$ read PWN < /challenge/read_me
```

flag: `pwn.college{c7WPwGuhAKVoPcHcjfM6LPbPhpH.dBjM4QDL2MDO0czW}`
