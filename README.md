# R3dc0n_Web_Workshop

## Welcome

Welcome to the Red Team Village R3dc0n 2023 Web Workshop!

## Getting Started

A fresh kali is already prebuilt for you running websploit via docker here: <https://bit.ly/3RziogR>

Pick an IP and place an X in checked out, if an IP is already checked out please grab one that is free. 

1. Download Redcon.pem under the Key column
2. Determine your access method (in order from least invasive/downloads):
    1. VNC through HTTPS (should require no downloads)
    -  https://< IP >:6080/vnc.html  (self signed cert, please accept) 
    -  click connect password is on spreadsheet 
    -  on the left click expand to go fullscreen 1920x1080 
    -  to use the shared clipboard open the noVNC panel on the left and click "clipboard" to copy paste between host and Kali
    2. VNC through SSH tunnels (grab your favorite vnc viewer, password is on spreadsheet)
```
ssh NfL 11111:127.0.0.1:5901 -i ~/Downloads/redcon.pem kali@< IP >

vncviewer 127.0.0.1:11111
```
  

