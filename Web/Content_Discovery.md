Web content discovery is important step in the web enumeration phase. Often times brute forcing for directories, files and subdomains is very effective using good wordlists, such as [SecLists](https://github.com/danielmiessler/SecLists).


# Manual discovery
`curl http://SERVER_IP:PORT/`

`curl http://SERVER_IP:PORT/robots.txt`

`curl http://SERVER_IP:PORT/sitemap.xml`

# Directory discovery
`ffuf -w /opt/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ`

`gobuster dir -t 40 -w /opt/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt --url http://SERVER_IP:PORT/`


# File discovery
`ffuf -w /opt/SecLists/Discovery/Web-Content/common.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1`

`ffuf -w /opt/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -e .html,.php` 

`ffuf -w /opt/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -e .asp,.aspx,.asm,.asmx` 

`ffuf -w /opt/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -e .jsp,.jspx,.wss` 

`ffuf -w /opt/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -e .log,.txt,.zip,.xml` 

`gobuster dir -t 40 -w /opt/SecLists/Discovery/Web-Content/common.txt --url http://SERVER_IP:PORT/`

`gobuster dir -t 40 -w /opt/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt --url http://SERVER_IP:PORT -x .html,php`

`gobuster dir -t 40 -w /opt/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt --url http://SERVER_IP:PORT -x .asp,aspx,asm,asmx`

`gobuster dir -t 40 -w /opt/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt --url http://SERVER_IP:PORT -x .jsp,jspx,wss`

`gobuster dir -t 40 -w /opt/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt --url http://SERVER_IP:PORT -x .log,txt,zip,xml`


# Subdomain discovery via VHOST
`ffuf -w /opt/SecLists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://DOMAIN.NAME:PORT/ -H "Host: FUZZ.DOMAIN.NAME:PORT/" -mc 200`

`gobuster vhost -t 40 -w /opt/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --url http://DOMAIN.NAME:PORT/`

# Subdomain discovery via DNS

[phonebook.cz](https://phonebook.cz/) - great online resource for subdomain and file discovery.

`amass enum -active -brute -d DOMAIN.NAME`
