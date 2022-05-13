The list can be updated by visiting the following website:

1. https://www.freewebhostingarea.com/ (provides a list of domain for choosing)
2. https://www.infinityfree.net/ (you need to register to get the list)
3. https://x10hosting.com/ (needs registration)
4. https://www.dynu.com/ControlPanel/AddDDNS (no need for registring)
5. This is a little bit tricky as it provides 10s of thousand of domains.
here is the link: https://freedns.afraid.org/domain/registry/page-2.html

In order to scrape it, do the following:

1. replace the number of pages in the following for-loop
2. All the results will be saved in a file `result.scrape`

```bash
for x in {1..457}; do curl --silent curl "https://freedns.afraid.org/domain/registry/page-$x.html"   -H 'Connection: keep-alive'   -H 'Pragma: no-cache'   -H 'Cache-Control: no-cache'   -H 'sec-ch-ua: " Not A;Brand";v="99", "Chromium";v="99", "Google Chrome";v="99"'   -H 'sec-ch-ua-mobile: ?0'   -H 'sec-ch-ua-platform: "Linux"'   -H 'Upgrade-Insecure-Requests: 1'   -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.82 Safari/537.36'   -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9'   -H 'Sec-Fetch-Site: none'   -H 'Sec-Fetch-Mode: navigate'   -H 'Sec-Fetch-User: ?1'   -H 'Sec-Fetch-Dest: document'   -H 'Accept-Language: en-US,en;q=0.9'   -H 'Cookie: tz=OLDt5SztMMJA5dhrcIUKtc4o; __utmz=4955364.1650974913.1.1.utmccn=(direct)|utmcsr=(direct)|utmcmd=(none); PHPSESSID=pfu3u0hsgggnr2fqkl7kti9rhv; dns_cookie=MSWJbwTSUJ3j4z7GJCrJdOzz; __utma=4955364.1257632780.1650974913.1650974913.1652438506.2; __utmb=4955364; __utmc=4955364'   --compressed >> result.scrape; sleep 2;echo $x; done
```

(The curl command can be coppied from the browser by clicking `copy as cURL`)


Then parse the file using the following command:

(removing all those that are freenom domains)

```bash
cat result.scrape | grep -E "<a href=/subdomain/edit\.php\?edit_domain_id=[0-9]{1,}>[-.a-zA-Z0-9]{1,}</a>" --only-matching | sed -n -E "s/.*edit_domain_id=[0-9]{1,}>(.*)<\/a>.*/\1/p"|sort | uniq | grep -E "[-.0-9a-zA-Z]{1,}\.(ml|ga|gq|cf|tk)" -v |sed -n 's/$/, fsp/p'
```

### NOTE (IMPORTANR)

It's not a good practice to go after those that are not very famous. So we select only those that have more than 1,000 subdomains.




