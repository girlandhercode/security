# Offline Password Cracking



We might find passwords or other credentials in databases. These are often hashed, so we need to first identify which hash it is and then try to crack it. The first step is to identify the hash-algorithm that was used to hash the password.

### Identify hash <a id="identify-hash"></a>

There are generally speaking three pieces of data we can use to identify a hash.

* The length of the hash
* The character set
* Any special characters

In order to identify a hash we can either use specialized tools that analyze the hash and then return a guess on which algorithm it is. An easier way is of course to just look in the documentation of the software where you found the hashes. It usually says in the documentation or the source code which type of hash is being used.

In kali we can use `hash-identifier` or `hashid`:

```text
hash-identifier 
hashid
```

Or try these online services:

[http://www.onlinehashcrack.com/hash-identification.php](http://www.onlinehashcrack.com/hash-identification.php)

[https://md5hashing.net/hash\_type\_checker](https://md5hashing.net/hash_type_checker)

### Cracking the hash <a id="cracking-the-hash"></a>

Okay so now we know what hash it is, let's get cracking.

If you want to try out the functionality of hashcat or john the ripper you can find example hashes here: [http://openwall.info/wiki/john/sample-hashes](http://openwall.info/wiki/john/sample-hashes).

#### Hashcat <a id="hashcat"></a>

Look for the specific type of hash you want to crack in the list produced by the following command:

```text
hashcat --help
```

Example Hashes

[https://hashcat.net/wiki/doku.php?id=example\_hashes](https://hashcat.net/wiki/doku.php?id=example_hashes)

My hash was a SHA1, so I will use the corresponding hash code for it, `100`

`-a 0` - straight attack mode

`-o found.txt` - where the cracked hash outputs

`admin.hash` - the hash you want to crack.

`/usr/share/hashcat/rules/rockyou-30000.rule` - the wordlist we use

```text
hashcat -m 100 -a 0 -o found.txt admin.hash /usr/share/hashcat/rules/rockyou-30000.rule
```

#### You got a sick GPU bro? <a id="you-got-a-sick-gpu-bro"></a>

`-a 3` - Brute-force \(attack mode\)

```text
hashcat64.exe -m 100 -a 3 -o found2.txt admin.hash
```

#### John the ripper <a id="john-the-ripper"></a>

So this is how you usually crack passwords with john

```text
john --wordlist=wordlist.txt dump.txt

if need to specify format

john --wordlist=wordlist.txt --format=Raw-MD5 dump.txt
```

If you do not find the password you can add the john-rules. Which add numbers and such things to each password.

```text
john --rules --wordlist=wordlist.txt dump.txt
```

Password wordlists.

```text
john --wordlist=test.txt --stdout --rules:Jumbo >> mutilated.txt
```

**View previosuly cracked passwords**

```text
View the john.pot file 

usually /root/.john/john.pot
```

**Linux shadow password**

First you need to combine the passwd file with the shadow file using the unshadow-program.

```text
unshadow passwd-file.txt shadow-file.txt > unshadowed.txt
john --rules --wordlist=wordlist.txt unshadowed.txt
```

#### Rainbow tables <a id="rainbow-tables"></a>

So basically a rainbow table is a precalculated list of passwords. So instead of having to hash the word you want to try you create a list of hashes. So you do not have to hash them before comparing. This might take a long time to do, hashing a whole wordlist, but when you do the comparison between the password and the test-word it will go a lot faster.

### Using Online Tools <a id="using-online-tools"></a>

#### findmyhash <a id="findmyhash"></a>

You can use findmyhash

Here is an example of how to use it:

```text
findmyhash LM -h 6c3d4c343f999422aad3b435b51404ee:bcd477bfdb45435a34c6a38403ca4364
```

#### Cracking <a id="cracking"></a>

Hashes.org

[https://hashes.org/search.php](https://hashes.org/search.php)

Hashkiller  
[https://hashkiller.co.uk/](https://hashkiller.co.uk/)

Google hashes  
Search pastebin.

### Windows <a id="windows"></a>

If you find a local file inclusion vulnerability you might be able to retrieve two fundamental files from it. the `system` registry and the `SAM` registry. There two files/registries are all we need to get the machines hashes.  
These files can be found in several different locations in windows. Here they are:

```text
Systemroot can be windows
%SYSTEMROOT%\repair\SAM
windows\repair\SAM
%SYSTEMROOT%\System32\config\RegBack\SAM

System file can be found here
SYSTEMROOT%\repair\system
%SYSTEMROOT%\System32\config\RegBack\system
```

So if the manage to get your hands on both of these files you can extract the password hashed like this:

```text
pwdump system sam
```

