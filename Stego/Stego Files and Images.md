
# images

Online Analyzer: https://aperisolve.fr/

https://book.hacktricks.xyz/stego/stego-tricks

```bash
steghide --info TryHackMe.jpg
steghide extract -sf TryHackMe.jpg
```

# ADS NTFS Streams

```ps
Get-Item -Path file.exe -Stream *
# run file from antoher file
wmic process call create $(Resolve-Path file.exe:streamname)
```

type 'echo hello > test:stream'. You've just created a stream named 'stream' that is associated with the file 'test'. Note that when you look at the size of test it is reported as 0, and the file looks empty when opened in any text editor. To see your stream enter 'more < test:stream' (the type command doesn't accept stream syntax so you have to use more)



## hide

```ps
Set-Content -Path .\lists.exe -value $(Get-Content $(Get-Command C:\Users\littlehelper\Documents\db.exe).Path -ReadCount 0 -Encoding Byte) -Encoding Byte -Stream hidedb
```


## stego brute force
https://github.com/RickdeJager/stegseek

