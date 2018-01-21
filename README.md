# mining

## A8N-SLI Premium Mobo

## Error: `MP-BIOS BUG: 8254 Timer not connected to IO-APIC`

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

# Cuda

```sh
wget http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_9.1.85-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1604_9.1.85-1_amd64.deb
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
sudo apt-get update
sudo apt-get install -y cuda
```

