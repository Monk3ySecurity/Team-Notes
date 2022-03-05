# Info gathering

Finding out about underlying web server technology and frameworks is useful to get a clear picture of the web server and application. 
Goal is to find out as much information as possible about web server's operating system, programming language, frameworks and versions.  

# Whois 
`whois SERVER`  
Online whois: https://www.whois.com/


# Whatweb
Extracts information about web server from HTTP headers, reverse dns resolution and IP info lookup.  
`whatweb -v http://SERVER/`

# Wappalyzer
Gain information about website's underlying technologies and frameworks.  
[Link](https://chrome.google.com/webstore/detail/wappalyzer-technology-pro/gppongmhjkpfnbhagpmjfkannfbllamg) - wappalyzer as a chrome extension.  
[Link](https://addons.mozilla.org/en-US/firefox/addon/wappalyzer/) - wappalyzer as a firefox extension.  

# Damn Small Javascript Scanner
[DSJS](https://github.com/stamparm/DSJS), Lightweight javascript vulnerability scanner.   
`python3 dsjs.py -u http://SERVER:PORT`  

# Find web server's physical geolocation
`nmap --script ip-geolocation-* -p80,443 SERVER`     

# Nikto
Web app vulnerability scanner and information gathering tool.    
`nikto -host http://SERVER:PORT/`  

# Nmap
Among many other things, nmap can be used for web information gathering.  
`nmap -sV -sC SERVER -p 80,443`  
`nmap -p80,443 --scripts http-php-version,http-methods,http-headers,http-errors,http-vhosts SERVER` 
