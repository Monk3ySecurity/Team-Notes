
## Stego-toolkit
Easy install popular stego tools like jphide, jsteg, stegdetect, f5, outguess, spectrology, steganabara, stegsolve, zsteg and much more.. <br>

`git clone https://github.com/DominicBreuker/stego-toolkit.git`  
`cd stego-toolkit/install`  
`./stegdetect.sh`  

Online Analyzers  
https://aperisolve.fr/  
https://29a.ch/photo-forensics  
http://magiceye.ecksdee.co.uk/

https://book.hacktricks.xyz/stego/stego-tricks  

## File type identification
Sometimes file type is not known. Usually file has lost it's integrity or extension is not known.  
This [resource](https://www.garykessler.net/library/file_sigs.html) can be used as a reference for file signatures.  
`file unknownfile`  
`xxd unkownfile | head`  
`xxd unknownfile | tail`  
`strings unknownfile | more`  
`strings -n 6 -t x file.ext | more`  
`strings file.ext | tr '[A-Za-z]' '[N-ZA-Mn-za-m]' | more`  
`cat image.png | tr -c [:graph:] " " | tr -s " " | xargs -P 5 -n 2  | more`  

## Exiftool
File metadata read/write tool  
`exiftool image.png`  
`exiftool -b image.png`  

## Stegdetect
Tool that detects possible steganography methods used on an JPG image, based on sensitivity value provided  
`stegdetect -s 10 image.jpg`  

## Zsteg
Secret data extractor that uses LSB steganography method in PNG and BMP files  
`zsteg -a image.png`  

## Jsteg
Secret data extractor that uses LSB steganography method in JPG files  
`jsteg reveal image.jpg secret.txt`  
`cat secret.txt`  

## Binwalk
Searches for embedded files inside other files and extracts them using file signatures  
`binwalk -e image.jpg`  
`binwalk -e --dd=".*" image.jpg`  

## Foremost
Searches for embedded files inside other files and extracts them using header, footer and internal data structure signatures  
`foremost -i image.png -v`

## Steghide
[Steghide](https://linuxhint.com/steghide-beginners-tutorial/), tool that can hide secret data inside an image and extract it  
`steghide --info TryHackMe.jpg`  
`steghide extract -sf TryHackMe.jpg`

## Stegsolve
Tool that has few neat features like stereogram solver, image combiner, frame browser and different bit planes view  
`stegsolve -jar stegsolve.jar`

# ADS NTFS Streams

```ps
Get-Item -Path file.exe -Stream *
# run file from antoher file
wmic process call create $(Resolve-Path file.exe:streamname)
```

type 'echo hello > test:stream'. You've just created a stream named 'stream' that is associated with the file 'test'. Note that when you look at the size of test it is reported as 0, and the file looks empty when opened in any text editor. To see your stream enter 'more < test:stream' (the type command doesn't accept stream syntax so you have to use more)



## Hide

```ps
Set-Content -Path .\lists.exe -value $(Get-Content $(Get-Command C:\Users\littlehelper\Documents\db.exe).Path -ReadCount 0 -Encoding Byte) -Encoding Byte -Stream hidedb
```


## Stego brute force
https://github.com/RickdeJager/stegseek

