# mining


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
