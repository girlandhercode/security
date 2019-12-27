# Search Engine Discovery

Search engines can be very useful for finding information about the target. Search engines can be used for two things:

* Finding sensitive information on the domain that you are attacking
* Finding sensitive information about the company and its employees in on other parts of the internet. Like forums, newsgroups etc.

Remember that the world is bigger than google. So test out the other search engines.

Baidu, binsearch.info, Bing, DuckDuckGo, ixquick/Startpage, Shodan,PunkSpider

Google is a good tool to learn more about a website.

## Finding specific filetypes <a id="finding-specific-filetypes"></a>

```text
filetype:pdf
```

### Search within webaddress <a id="search-within-webaddress"></a>

```text
site:example.com myword
```

### Find in url <a id="find-in-url"></a>

```text
inurl:test.com
```

### Wild cards <a id="wild-cards"></a>

You can use the asterisk to as a wildcard:

```text
*
```

Example:

```text
"I've been * for a heart"
```

This will return answers where \* is anything.

## Exclude words <a id="exclude-words"></a>

```text
-
```

the dash excludes a specific word

This query searches for pages that used the word bananasplit.

```text
-banana bananasplit
```

### Cached version <a id="cached-version"></a>

So if a website has been taken down you can still find the cached version, of the last time google visited the site

```text
cache:website.com
```

[https://www.blackhat.com/presentations/bh-europe-05/BH\_EU\_05-Long.pdf](https://www.blackhat.com/presentations/bh-europe-05/BH_EU_05-Long.pdf)

## Examples <a id="examples"></a>

Find login-pages on sites that use the ending .bo. For bolivia.

```text
site:bo inurl:admin.php
```

## More <a id="more"></a>

Here are some more

Great guide for google dorks  
[https://www.blackhat.com/presentations/bh-europe-05/BH\_EU\_05-Long.pdf](https://www.blackhat.com/presentations/bh-europe-05/BH_EU_05-Long.pdf)

[http://www.googleguide.com/advanced\_operators\_reference.html](http://www.googleguide.com/advanced_operators_reference.html)

[http://www.searchcommands.com/](http://www.searchcommands.com/)

[https://support.google.com/websearch/answer/2466433?hl=en](https://support.google.com/websearch/answer/2466433?hl=en)

[https://www.exploit-db.com/google-hacking-database/](https://www.exploit-db.com/google-hacking-database/)

