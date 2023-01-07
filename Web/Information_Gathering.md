# Info gathering

Finding out about underlying web server technology and frameworks is useful to get a clear picture of the web server and application. 
Goal is to find out as much information as possible about web server's operating system, programming language, frameworks and versions and possibly known vulnerabilities or misconfigurations.

## Whois 
`whois domain.com`  
[whois](https://www.whois.com/), online version.  

## Whatweb
[Whatweb](https://github.com/urbanadventurer/WhatWeb) extracts information about web server from HTTP headers, reverse dns resolution and IP info lookup.  
`whatweb -v http://domain.com`

## Wappalyzer
Gain information about website's underlying technologies and frameworks.  
[Link](https://chrome.google.com/webstore/detail/wappalyzer-technology-pro/gppongmhjkpfnbhagpmjfkannfbllamg) - wappalyzer as a chrome extension.  
[Link](https://addons.mozilla.org/en-US/firefox/addon/wappalyzer/) - wappalyzer as a firefox extension.  

## WhatRuns
Can gain additional information about website's underlying technologies and frameworks.  
[Link](https://chrome.google.com/webstore/detail/whatruns/cmkdbmfndkfgebldhnkbfhlneefdaaip) - WhatRuns as a chrome extension.  
[Link](https://addons.mozilla.org/en-US/firefox/addon/whatruns/) - WhatRuns as a firefox extension.  

## Webanalyze
[Webanalyze](https://github.com/rverton/webanalyze) is a command line version of wappalyzer.  
`webanalyze -host domain.com -crawl 1`  

## Vuln scanners
[Nikto](https://github.com/sullo/nikto) for general security issues.  
[Nuclei](https://github.com/projectdiscovery/nuclei) for CVE and misconfiguration discovery.  
`nikto -host http://domain.com/`  
`nuclei -u http://domain.com/`  

## Damn Small Javascript Scanner
[DSJS](https://github.com/stamparm/DSJS), Lightweight javascript vulnerability scanner.   
`python3 dsjs.py -u http://domain.com/`    

## Nmap
Among many other things, [Nmap](https://nmap.org/) can be used for web information gathering.  
`nmap -sV -sC -p 80,443 IP`  
`nmap -p80,443 --script http-php-version,http-methods,http-headers,http-errors,http-vhosts IP` 
