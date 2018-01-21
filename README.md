# mining

## A8N-SLI Premium Mobo

Error: `MP-BIOS BUG: 8254 Timer not connected to IO-APIC`

### Temporary

* `f8` to get to grub boot list; `e` to edit; `f10` to boot
* add `noapic` to boot options (second to last line)

### Permanent

* /etc/default/grub
* add noapic to GRUB_CMDLINE_LINUX_DEFAULT
* sudo update-grub

## Excavator 

Uses [`excavator.service`](./excavator.service)

```sh
# enable
sudo systemctl enable excavator
# if service file changes
sudo systemctl daemon-reload
# start
systemctl start excavator
# logs
systemctl status excavator.service
# tail logs
journalctl -u excavator -b -f
```

## Cuda

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

## NVIDIA Drivers

```sh
# NVIDIA drivers from graphics-drivers PPA
sudo add-apt-repository ppa:graphics-drivers/ppa
apt-get update
apt-get -y install nvidia-390-dev nvidia-opencl-icd-390
```

Watch this for newer versions: https://launchpad.net/~graphics-drivers/+archive/ubuntu/ppa

## Misc

### Sensor Metrics

Install

```sh
# install util
sudo apt-get install -y lm-sensors
# detect & accept defaults
(while :; do echo ""; done ) | sudo sensors-detect

# or detect & "yes" to all
yes "" | sudo sensors-detect
```

Run

```sh
sensors-detect
```
