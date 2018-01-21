# NVIDIA

## Cuda Platform

```sh
# keep an eye on this for newer versions
# http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/
wget http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_9.1.85-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1604_9.1.85-1_amd64.deb
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
sudo apt-get update
sudo apt-get install -y cuda
```

Watch this for newer versions: http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/

## Drivers

```sh
# NVIDIA drivers from graphics-drivers PPA
sudo add-apt-repository ppa:graphics-drivers/ppa
apt-get update
apt-get -y install nvidia-390-dev nvidia-opencl-icd-390
```

Watch this for newer versions: https://launchpad.net/~graphics-drivers/+archive/ubuntu/ppa

## Overclocking

Ref: https://unix.stackexchange.com/questions/367584/how-to-adjust-nvidia-gpu-fan-speed-on-a-headless-node
```

Make generic nvidia X11 config

```sh
nvidia-xconfig --enable-all-gpus
```

# X11

Get card IDs:

```sh
lspci | grep "VGA compatible controller: NVIDIA"

Example config

```conf
#/etc/X11/xorg.conf
# note: change PCI IDs as needed
# Important part is “Coolbits” “31”
# Make sure you have the correct BusID for your cards
Section "ServerLayout"
    	Identifier "dual"
    	Screen 0 "Screen0"
    	Screen 1 "Screen1" RightOf "Screen0"
EndSection
Section "Device"
	Identifier 	"Device0"
	Driver     	"nvidia"
	VendorName 	"NVIDIA Corporation"
	BusID      	"PCI:1:0:0"
	Option     	"Coolbits"   	"31"
	Option     	"AllowEmptyInitialConfiguration"
EndSection
Section "Device"
	Identifier 	"Device1"
	Driver     	"nvidia"
	VendorName 	"NVIDIA Corporation"
	BusID      	"PCI:2:0:0"
	Option     	"Coolbits"   	"31"
	Option     	"AllowEmptyInitialConfiguration"
EndSection
Section "Screen"
    	Identifier 	"Screen0"
    	Device     	"Device0"
EndSection
Section "Screen"
    	Identifier 	"Screen1"
    	Device     	"Device1"
EndSection
```

Overclock Script

This only works if the X11 config is configured correctly and X is started.

Install

```sh
# download https://raw.githubusercontent.com/Cyclenerd/ethereum_nvidia_miner/master/files/nvidia-overclock.sh
wget https://raw.githubusercontent.com/Cyclenerd/ethereum_nvidia_miner/f42de74da4144c67a61926b8fb78124a6436db49/files/nvidia-overclock.sh
chmod a+x nvidia-overclock.sh
```
Configure

`settings.conf`:
```sh
# settings.conf: https://github.com/Cyclenerd/ethereum_nvidia_miner/blob/master/files/settings.conf
# MY_ADDRESS : Your public ethereum address
# MY_RIG     : Your mining rig name
# MY_WATT    : Set power limit for all NVIDIA grafic cards.
#              Input in watts (W). Allowed characters 0-9.
#              Only on supported devices from Kepler family.
# MY_CLOCK   : Set GPU graphics clock offset (GPUGraphicsClockOffset) for all NVIDIA grafic cards.
#              Allowed characters 0-9 and -.
# MY_MEM     : Set GPU memory transfer rate offset (GPUMemoryTransferRateOffset) for all NVIDIA grafic cards.
#              Allowed characters 0-9.
# MY_FAN     : Set GPU target fan speed (GPUTargetFanSpeed) for all NVIDIA grafic cards.
#              Input in percent (%).
MY_RIG="mine"
# it’s cool to use fewer watts. Literally. 120 is stock for a 1060, see how low you can go without crashing or losing hash rate.
MY_WATT="90"
# increasing clock helps for some algorithms, makes no difference for others.  If it doesn’t help hash rate, you can even go negative. -200 drops clocks by 200 from stock.
MY_CLOCK="50"
# Memory overclock has the greatest impact on ETH mining, less so on other algorithms. 600 usually works, see how high you can go. I have seen 1000 on some cards.
MY_MEM="600"
# set as high as you can tolerate. 100 = full speed
MY_FAN="80"	
```

Run

```sh
./ nvidia-overclock.sh
```
