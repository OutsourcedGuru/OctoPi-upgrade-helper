# OctoPi-upgrade-helper
A shell script to assist in backing up and restoring OctoPrint data suitable for OctoPi image upgrades.

> [OctoPrint](https://octoprint.org) is the underlying programming interface which is being exercised here under the hood of the printer. It's the product of the talented Gina Häußge.

> [OctoPi](https://github.com/guysoft/OctoPi) is a distribution image for the Raspberry Pi computer as maintained by Guy Sheffer.

## Overview
The current distribution method of OctoPi requires that each user manually back up their `~/.octoprint` folder structure and to remember a number of configuration changes that they'd made in the past.

At some point, the collection of changes, tweaks and adjustments can be a little overwhelming. This script hopes to minimize some of that anxiety.

## What the script does
This script will assist you in making a backup copy of your `~/.octoprint` folder area, to download this to your workstation and to upload it back. This is the main functionality provided.

Additionally, the script provides the shell commands to save things like `/boot/octopi-wpa-supplicant.txt`, for example.

## Assumptions
I assume that you have an OctoPi—imaged Raspberry Pi of some kind and that it will run a shell script. I further assume that you're comfortable remoting into your Raspi.

I wrote this with the assumption that you did not change the original hostname of `octopi`. There are places in the script where it provides you with commands to run with this hostname in it. You are expected to edit those commands on the command line for your printer's name.

## Instructions
Much of the script itself contains the instructions involved in backing up and restoring your OctoPrint data.

The instructions here are enough to get that script onto your Raspberry Pi computer so that you may run it there.

1. Remote into your Raspberry Pi computer as in `ssh pi@octopi.local`
2. `curl -o ~/scripts/upgrade-help https://raw.githubusercontent.com/OutsourcedGuru/OctoPi-upgrade-helper/master/upgrade-help`
3. `chmod a+x ~/scripts/upgrade-help`
4. `~/scripts/upgrade-help backup`

## Notes
* If you develop software on your Raspberry Pi then this script will not backup your development efforts. A better solution might be to use something like [ApplePi-Baker](https://www.tweaking4all.com/software/macosx-software/macosx-apple-pi-baker/) to clone images as a safety margin against loss.
* Personally, I maintain a collection of perhaps ten microSD cards which contain cloned images of my printer and would recommend something like this if you're at all active with your printer and you'd like to minimize downtime.
* You'll still need to run `sudo raspi-config` on the new image burned to adjust the timezone minimally as well as anything else you've changed in the past.
* This script makes no attempt to assist you if you've turned on access control and have created additional users. You will need to recreate those so it's a good idea to create a checklist before proceeding in this case.
* This script will not save the entire collection of wifi zones/passwords only the first. If you take your printer to other venues and you've introduced it to other wifi zones, then make sure to create a checklist of those.
* Given that the `~/.octoprint/config.yaml` is backed up, any settings you have made in your plugins will be preserved; you'll just need to re-install them however