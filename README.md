# 000000000000.cfg
# Master config for Polycom VVX &amp; Trio device families

This repo is the updated and open-source version of my blog post [Optimising the Polycom VVX for Lync/SfB] (https://greiginsydney.com/optimising-the-polycom-vvx-for-lync/).  You can read some of the history and more detailed explanations there, but all the config now resides here.

## How-To

1. Copy this repo to your provisioning server
2. Unzip the lot into the root folder your FTP server directs the phones to. In my deployments that's usually something like `C:\Polycom-UCS\`
3. Download the "split" version of the [Polycom firmware ZIP] (https://support.polycom.com/content/support/north-america/usa/en/support/voice.html) into the relevant folder
  
   e.g. `Firmware-VVX`
4. Unzip the archive to create a separate folder structure for each firmware version. I name mine with the version and release date:
  
   e.g. `Firmware-VVX\5.8.0.12386-June2018`
5. Edit the Master config file (000000000000.cfg):
   - set the `APP_FILE_PATH` to point to the file "sip.ld" in this folder
  
     e.g. `APP_FILE_PATH="FIRMWARE-VVX/5.8.0.12386-June2018/sip.ld"`
   - set `CONFIG_FILES` to reference a comma-separated list of config files for the phone to load
  
     e.g. `CONFIG_FILES="customisations.cfg,AU-DST.cfg,AU-TONES.cfg"`
  
     Delete or amend these files as appropriate. If you're not in Australia, remove the references to the two AU- files.
     Note that if the same element appears multiply, first takes precedence - the first reference is the one that's applied: any repeat references are ignored
6. Review customisations.cfg. Replace my placeholder values with those relevant to your deployment
  
   e.g. `#Your410Background.jpg#` and the two references to "Contoso" 
7. Reboot a phone
8. Good luck!


## The CFG files
In the root of this repo you'll find multiple XML ".cfg" files:
- 000000000000.cfg
  
  Sometimes referred to as "zeroes.cfg", this is the Master Config File. When the phone boots it looks first for a config file named for its MAC address (e.g. 0004fe123456.cfg) and in the absence of that it pulls the master config file
- customisations.cfg
  
  This file contains all of my customisations. It's full of explanatory notes, options you may want to customise (e.g. 12/24hr time display) and some placeholder values you need to update before it goes into production
- custom-trio.cfg
  
  This is the customisations file for a Trio running as a Lync/SfB user or meeting room device
- trio-usb.cfg
  
  This forces a Trio into "SkypeUSB" mode. This disables its SIP stack entirely, turning it into a USB peripheral, typically a slave device hanging off an SRS
- AU-DST.cfg
  
  This has the daylight saving time settings for the relevant Australian states and territories
- AU-TONES.cfg
  
  Customises the tones for Australia
- courtesy.cfg
  
  This file locks down a phone that will go into a public or otherwise untrusted area. It disables all external ports and disables ALL buttons other than the digit keypad and the volumn up/down buttons.  If you don't change it, when the handset goes off-hook it will Hotline to "1231". Change the "call.autoOffHook.1.contact" line to your required destination, or remove the line to make it a very basic phone. Refer my blog post [A VVX Courtesy Phone] (https://greiginsydney.com/a-vvx-courtesy-phone/) for some more details
- wifi.cfg
  
  With a VVX 500 or 600-series and a Obihai USB Wifi dongle, this config file will ensure the phone automatically connects to the specified network. Read more in [A Fully Wireless VVX] (https://greiginsydney.com/a-fully-wireless-vvx/)


## Tips
- I generally use [Notepad++] (https://notepad-plus-plus.org/) for editing, but as a final test of the file before I make it live I open it with [XML Notepad 2007] (https://www.microsoft.com/en-us/download/details.aspx?id=7973). This will quickly highlight any bugs in your XML syntax
- Once the phone's rebooted, Home - Settings - 4 - 1 - 3 (on all VVX models) will show the status screen, confirming the files were found and applied, and the count of any errors or duplicates


## Credits

Thanks to [Jeff Schertz] (http://blog.schertz.name/) for all his contributions to the product family over the years, [James Cussen] (https://www.myskypelab.com/) for his tools, and to my colleagues, customers and peers for their tips, suggestions & corrections.




\- Greig.
