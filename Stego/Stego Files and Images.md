
## Stego-toolkit
Easy install popular stego tools like jphide, jsteg, stegdetect, f5, outguess, spectrology, steganabara, stegsolve, zsteg and much more.. <br>

`git clone https://github.com/DominicBreuker/stego-toolkit.git` <br>
`cd stego-toolkit/install` <br>
`./stegdetect.sh`


# Images

Online Analyzer: https://aperisolve.fr/

https://book.hacktricks.xyz/stego/stego-tricks

## Exiftool
File metadata read/write tool <br>
`exiftool image.png` <br>
`exiftool -b image.png`

## Stegdetect
Tool that detects possible steganography methods used on an jpg image, based on sensitivity value provided <br>
`stegdetect -s 10 image.jpg` <br>

## Zsteg
Secret data extractor that uses LSB steganography method in PNG and BMP files <br>
`zsteg -a image.png`

## Jsteg
Secret data extractor that uses LSB steganography method in JPG files <br>
`jsteg reveal image.jpg secret.txt` <br>
`cat secret.txt`

## Steghide
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



## Hide

```ps
Set-Content -Path .\lists.exe -value $(Get-Content $(Get-Command C:\Users\littlehelper\Documents\db.exe).Path -ReadCount 0 -Encoding Byte) -Encoding Byte -Stream hidedb
```


## Stego brute force
https://github.com/RickdeJager/stegseek

