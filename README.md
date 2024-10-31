# iPod Management on Windows
A Windows Virtual Machine to format your iPod as a Win-pod (FAT32) !

## FAQ
### My Mac is too old to run UTM
The simplest option for you if to create a Linux live CD/USB then boot on it to be able to use the simple Linux instructions that I provide in this documentation. You can get Ubuntu from here https://ubuntu.com/download/desktop and burn it into a USB stick by using Balena Etcher https://etcher.balena.io/, good luck !

### How to update the Virtual Machine to a newer version ?
Remove the .utm file and all the compressed .7z parts which were used to extract it. All .7z files must be downloaded again. Make sure your computer doesn't rename the downloaded files to something like "filename(1)" since the files were already downloaded before. Rename the downloaded files accordingly if necessary.

### [Linux] The script "start_qemu.sh" does not start on my machine, what can I do ?
It looks like your computer is an ARM64 one or a very old Intel/AMD computer, so you should use ```slow_start_qemu.sh``` instead to start the virtual machine.

## How to use
### Requirements
- (Recommended) A Mac computer that can run UTM (https://mac.getutm.app/). Don't download the Mac App Store version because it has limitations. An Intel Mac is preferable for speed but all of this was developed and tested on an Apple Silicon Mac where it run slowly but just fine.
- (Recommended) A Linux Intel/AMD x64 computer. Ubuntu 24.04 is recommended. If you can't install Linux, it should also work in a LiveCD directly. You can get Ubuntu from here: https://www.ubuntu-fr.org/ and burn the ISO into an USB stick easily using Rufus (https://rufus.ie/, Windows Only !) or Balena Etcher (https://etcher.balena.io/, Multiplatform !). This setup works very well and seems to be very reliable. I tested that setup on one of my Intel PC and it worked wonderfully and was a very fast way to boot easily the Virtual Machine and get a very high level performance with it.
- (Not Recommended) Windows Intel/AMD x64. I could not make this run under Hyper-V so it was running very slowly on my tests. Also, I could not make USB passthrough to work on Windows (the iPod was recognized as a generic "iPod" device and was not appearing in iTunes). But maybe in the future someone else will figure out how to make all of this working correctly on Windows, feel free to open a pull request with updated documentation.

Please be aware that it is probably possible to run this in a much more exotic setup as long as it is Qemu + USB passthrough compatible, but you will need to build yourself the exact command to make this boot and work for you.

Your computer need to be connected to the Internet or the restore process will not work.

**Don't forget also** if you are a Linux user to download this repo as a zip: https://github.com/Olsro/ipodmanagementonwindows/archive/refs/heads/main.zip or to clone it locally. It will be your workspace. **On MacOS, you can go ahead** and just download directly the .utm virtual machine file on the step just below.

### 1) Download the Virtual Machine
Unfortunately, the Virtual Machine is too heavy (around 10GB) to be hosted directly on GitHub. When the Virtual Machine will be completed, it will be shared as a torrent so it will avoid getting lost over time.

You can download the latest version from the following locations: 
#### GitHub Releases
https://github.com/Olsro/ipodmanagementonwindows/releases

Re-uploads appreciated !

Be aware that you need around **10 GB** of free space on your hard drive to extract the .utm file from the splitted archive !

### 2) Unzip the Virtual Machine
Due to its large size, I had to split the VM into multiple compressed 7zips files.
- On MacOS, "The Unarchiver" is recommended to unpack 7zip archives: https://theunarchiver.com/
- On Linux, open a Terminal in the folder and enter this: ```sudo apt update && sudo apt install -y p7zip-full && 7za x "iPod*Management*on*Windows.utm.7z.001"```

You need to extract "iPod Management on Windows.utm.7z.001" which will automatically find other parts (2, 3, 4, etc) to extract the full ".utm" Virtual Machine.

### 3) Booting up the Virtual Machine
- On MacOS
	- 1) Download and install UTM: https://mac.getutm.app/ (avoid the Mac App Store version, because it has some limitations)
	- 2) Just import the .utm virtual machine file into UTM
	![Alt text](images/mac/utm-file-open.png?raw=true "Import the VM in UTM")
	- 3) You should be able to launch it straight. Check the capture just below to know where to click to connect your iPod in the Virtual Machine.
	![Alt text](images/mac/utm-usb-passthrough.png?raw=true "USB Passthrough on Mac with UTM")
- On Linux:
	- 1) Copy the .utm file on this folder, because it will be needed by the script "start_qemu.sh".
	- 2) Open a Terminal on the folder of this cloned repo where start_qemu.sh is located.
	- 3) Install Qemu and dependencies: ```chmod a+x ./install_qemu.sh && ./install_qemu.sh``` (Ubuntu-only script, if not using Ubuntu 24.04 you will need to adapt it to your needs)
	- 4) Run Qemu: ```chmod a+x ./start_qemu.sh && ./start_qemu.sh``` or if your arch is ARM64 (for example if you are using an Apple Silicon Mac on Asahi Linux) you can emulate the x64 arch (which will be much slower) with this script ```chmod a+x ./slow_start_qemu.sh && ./slow_start_qemu.sh```.
	- 5) Now you can start Remmina to control it
	- 6) Setup a new SPICE connection with the following address: 127.0.0.1:17474 and connect to it
	![Alt text](images/linux/remmina.png?raw=true "Remmina")
	- 7) You should now see the Virtual Machine booting and be able to interact with it
	- 8) You can USB passthrough your iPod to the Virtual Machine by clicking on the "Adjustable wrench" icon that is located near the bottom of the left panel to redirect your iPod to the Virtual Machine.
	![Alt text](images/linux/virtualmachineusbredir.png?raw=true "Virtual Machine USB Passthrough")

### 4) Restoring using iTunes
The option "Disk use" (enabled by default) **must** be enabled. If it isn't enabled, you can enable it by connecting your iPod on your host machine through iTunes (or through the Finder syncing window for the most recent versions of MacOS).

I recommend letting the iPod connect to the host then eject it on the Finder before doing the passthrough to the Virtual Machine, it is more reliable this way.

Then, it's time to connect your iPod to the virtual machine using USB passthrough then open iTunes to do the restore.

## Credits
Project started, documented and maintained by OlsroFR

https://github.com/Olsro/ipodmanagementonwindows

## Contact
https://www.patreon.com/Olsro

https://www.reddit.com/user/OlsroFR/

Mail: olsroparadise@proton.me

Discord: Inurayama