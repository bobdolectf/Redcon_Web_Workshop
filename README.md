# R3dc0n_Web_Workshop

## Welcome

Welcome to the Red Team Village R3dc0n 2022 Web Workshop!

Twitter: @bobhacksthings @systemdumb

Discord: BobDole#7758 Gambit#1303

## Getting Started

A fresh kali is already prebuilt for you running websploit via docker here: <https://bit.ly/3RziogR>

Pick an IP and place an X in checked out, if an IP is already checked out please grab one that is free. 

1. Download R3dc0n.pem under the Key column
2. Determine your access method (in order from least invasive/downloads):
    1. VNC through HTTPS (should require no downloads)
    -  https://< IP >:6080/vnc.html  (self signed cert, please accept) 
    -  click connect password is on spreadsheet 
    -  on the left click expand to go fullscreen 1920x1080 
    -  to use the shared clipboard open the noVNC panel on the left and click "clipboard" to copy paste between host and Kali
    2. VNC through SSH tunnels (grab your favorite vnc viewer, password is on spreadsheet)
```
  ssh NfL 11111:127.0.0.1:5901 -i ~/Downloads.redcon.pem kali@< IP >

  vncviewer 127.0.0.1:11111
```
  
## Documentation

Once your are settled into your desktop session open up Firefox and the Lab Guide will be your home page. As mentioned previously we are going to work through some labs that Omar Santos combined into a self-contained deployment. Skip past the Docker walkthrough to page 9 as that is already setup for you.

In the titlebar you will see multiple other bookmarks, these will take you to the bridged vulnerable web apps that we will be working through.
