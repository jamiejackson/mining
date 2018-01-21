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


