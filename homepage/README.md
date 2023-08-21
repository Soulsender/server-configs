# Homepage Config
To get the stats working on the "Server" service in `services.yaml` you will need to install python glances to get the correct information. You can run it as a container but I run it as a OS level service via systemd.

Install it with:
```
pip install glances[all]
pip install --upgrade glances
pip install --upgrade psutil
pip install --upgrade glances[all]
```

You need the [all] version for the webserver.

Make a systemd service file with `sudo touch /etc/systemd/system/glances.service` then edit the file with:

```
[Unit]
Description=Glances service

[Service]
Type=simple
Restart=always
RestartSec=1
User=soul
ExecStart=/home/soul/.local/bin/glances -w

[Install]
```

Where `ExecStart` is wherever the glances binary is stored on your system (`which glances`). The `-w` flag makes it the web server version which homepage needs to access to get the actual stats. 

Then just start and enable it like any other systemd service.

```
sudo systemctl start glances
sudo systemctl enable glances
```
