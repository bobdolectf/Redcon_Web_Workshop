# Redcon_Web_Workshop

## Welcome

Welcome to the Redcon 2022 Web Workshop!

Twitter: @bobhacksthings @systemdumb
Discord: BobDole#7758 Gambit#1303

## Getting Started

A fresh kali is already prebuilt for you running [websploit labs] (https://websploit.org/index.html) via docker here: https://bit.ly/3RziogR 

Pick an IP and place an X in checked out, if an IP is already checked out please grab one that is free. 

1) Download Redcon.pem under the Key column
2) Determine your access method (in order from least invasive/downloads):
  2a) VNC through HTTPS (should require no downloads)
  -  https://<IP>:6080/vnc.html  (self signed cert, please accept) 
  -  click connect password is: redcon 
  -  on the left click expand to go fullscreen 1920x1080 
  -  to use the shared clipboard open the noVNC panel on the left and click "clipboard" to copy paste between host and Kali
  2b) VNC through SSH tunnels (grab your favorite vnc viewer, password is redcon)
  ``````
  ssh NfL 11111:127.0.0.1:5901 -i ~/Downloads.Redcon.pem kali@<IP>
  vncviewer 127.0.0.1:11111
  ``````
  
## Documentation

Once your are settled on your desktop session open up Firefox and your Workbook will be your home page. As mentioned previously we are going to work through some labs that Omar Santos combined into a self-contained deployment. 

In the titlebar you will see multiple other bookmarks, these will take you to the bridged vulnerable web apps that we will be working through.
