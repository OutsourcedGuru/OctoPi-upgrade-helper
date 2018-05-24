# Walk-through session using the helper script
This documents a session of exercising the helper script during a real-life upgrade of OctoPi image on my printer. Since I develop software directly on the Pi, I will be taking some extra precautions to preserve my original microSD card.

## Begin
I note that the time now is 10:55AM.

## Prep
It helps to prepare things so that everything can go as smoothly as possible.

1. Visit [this page](https://github.com/guysoft/OctoPi) and download the OctoPi image to a location on your computer, for example, your home directory. (5 minutes - 11:00)
2. If you're like me, you'll want to replace your original microSD with a new one, so have one available of the same capacity as the original
3. I have a previously-used 16GB microSD I would like to use for the upgrade but I first make a zipped image copy of it using ApplePi-Baker just to be on the safe side (10 minutes - 11:10)
4. I note that I already have Etcher installed on my workstation

I should now be ready to begin. The printer is on and OctoPrint is running. The new microSD is in my workstation and ready to be imaged.

## Following the README.md
1. Open two Terminal prompts on your workstation and orient them left/right on the screen, in the one on the right remote into the OctoPi computer `ssh pi@octopi.local`. I will refer to these as the **local** and **remote** terminal sessions.  (6 minutes - 11:16)
2. In the remote terminal, refer to the Instructions section of the README.md, starting the script in backup mode and answering 'y' to the first prompt (4 minutes - 11:20)
3. Scrolling up and reading everything in the output—especially anything in bold—and proceed with those instructions:
4. On the local session `scp pi@octopi.local:~/dot_octoprint.tar.gz ~/.` (1 minute - 11:21)
5. On the local session `scp pi@octopi.local:~/scripts/upgrade-help ~/.` (1 minute - 11:22)
6. On the local session `scp pi@octopi.local:/boot/octopi-wpa-supplicant.txt ~/.` (1 minute - 11:23)
7. On the local session `scp pi@octopi.local:/boot/octopi.txt ~/.` (1 minute - 11:24)
8. On the local session `scp pi@octopi.local:/boot/config.txt ~/.` (1 minute - 11:25)
9. Using Etcher, burn the downloaded image to the new microSD card (13 minutes - 11:38)
10. Since Etcher has unmounted the card, remove/re-insert it into your workstation; you should be able to see the `boot` partition
11. If you have previously edited your Raspi's `/boot/config.txt` to accommodate a TFT screen, edit/overcopy it now with the version saved in your workstation's home directory
12. Edit/overcopy the `/boot/octopi-wpa-supplicant.txt` file to preserve your wifi settings and verify the country code
13. Optionally edit/overcopy the `/boot/octopi.txt` file if you'd earlier modified it for your webcam
14. Safely eject the microSD card and remove it from your workstation (12 minutes - 11:50)
15. If you've not already done so, in the remote session, power off the Raspberry Pi `sudo poweroff`
16. Remove the existing microSD from your printer, mark it to minimize confusion, and put the new microSD into it, booting it and noting that the default hostname is `octopi` and the username is `pi`
17. In the remote session terminal, remote back into the Raspberry Pi
18. Run `sudo raspi-config`, set the localization settings for your timezone, set the wifi country code, a US-based keyboard (for example) and the default language
19. Optionally, change the hostname
20. Optionally, enable the VNC server
21. Select Finish and opt for the Reboot, remoting back in afterwards and noting a hostname change if you did that a moment ago

> It is possible that `ssh` isn't happy with all this and will complain about possible DNS spoofing. Look for the "Offending key" in the file, edit with `nano ~/.ssh/known_hosts` to remove the indicated line in this file. Exit/save and try again.
 
&nbsp;22. Optionally from the remote session, install the Desktop with `sudo /home/pi/scripts/install-desktop`, reboot and remote back in

&nbsp;23. `sudo raspi-config`, set the boot option to automatically log into the Desktop as pi, Finish and reboot

&nbsp;24. From the local session, `scp ~/upgrade-help pi@octopi.local:~/scripts/.`

&nbsp;25. From the local session, `scp ~/dot_octoprint.tar.gz pi@octopi.local:~/.`

&nbsp;26. From the remote session `~/scripts/upgrade-help restore`, answering 'y' to the first prompt

Note the list of plugins which need to be manually installed again. Making a screenshot at this point may be useful. For example:

```
  Bed Visualizer (0.1.0) = /home/pi/oprint/local/lib/python2.7/site-packages/octoprint_bedlevelvisualizer
  EEPROM Marlin Editor Plugin (1.2.1) = /home/pi/oprint/local/lib/python2.7/site-packages/octoprint_eeprom_marlin
  GCODE System Commands (0.1.1) = /home/pi/oprint/local/lib/python2.7/site-packages/octoprint_gcodesystemcommands
  Themeify (1.2.0) = /home/pi/oprint/local/lib/python2.7/site-packages/octoprint_themeify
```

&nbsp;27. On your workstation's browser, visit http://octopi.local and install your plugins again, noting that since `~/.octoprint/config.yaml` has been restored, you should not have to re-introduce all your changes in those plugins
