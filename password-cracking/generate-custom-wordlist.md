# Generate Custom Wordlist

Cracking passwords is good to know.

If we are able to do a dictionary-attack against a service it is important that we use a good dictionary. We can use e generic one. But we can also generate a custom wordlist based on certain criteria. That is what we are going to do in this chapter.

Remember people often use their birth dates, address, street address, pets, family members, etc.

### Who is the target? <a id="who-is-the-target"></a>

The target might be a specific company or person.

### Password rules <a id="password-rules"></a>

The service you want to hack might have specific password rules. Must contain certain characters, must be of certain length etc.

### Combine a small/semi-small dict with a custom <a id="combine-a-smallsemi-small-dict-with-a-custom"></a>

To combine two wordlists you can just do

```text
cat wordlist.txt >> wordlist2.txt
```

### Create a custom wordlist <a id="create-a-custom-wordlist"></a>

**Use crunch**

```text
crunch 10 10 -t ,%Curtains -o ./worlist.curtains

this would create a 10 character length passwords (min & max are =), and uses the pattern "Upper case/Number/Curtains"
```

**Html2dic - Build dictionary from html**

You can build a dictionary from a html-page.

```text
curl http://example.com > example.txt
```

Then run:

```text
html2dic example.txt
```

Then you should probably remove duplicates.

**Cewl - Spider and build dictionary**

```text
cewl -w createWordlist.txt https://www.example.com
```

Add minimum password length:

```text
cewl -w createWordlist.txt -m 6 https://www.example.com
```

**Improve the custom wordlist**

As we all know few password are just simple words. Many use numbers and special characters. To improve our password list we can use john the ripper. We can input our own rules, or we can just use the standard john-the-ripper rules

```text
john --wordlist=wordlist.txt --rules --stdout > wordlist-modified.txt
```

### to modify an already built wordlist further for specials \(i.e. append two numbers to the end\) <a id="to-modify-an-already-built-wordlist-further-for-specials-ie-append-two-numbers-to-the-end"></a>

add a custom rule to the john config \( /etc/john/john.conf\)

```text
# Add two numbers to the end of each password 
[List.Rules:Addtwonum]
$[0-9]$[0-9]
```

then utilize it

./john --wordlist=password.lst --stdout --rules:Addtwonum &gt; /home/usr/Desktop/mutatedpswds.lst

