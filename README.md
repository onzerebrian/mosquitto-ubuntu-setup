# 🐝 Mosquitto MQTT Broker Installation Guide (Ubuntu)

This guide walks you through the steps of installing and securely configuring the [Mosquitto MQTT Broker](https://mosquitto.org/) on an Ubuntu system. This setup includes password-based authentication and both TCP and WebSocket listeners.

## ✅ 1. Update Your System
```bash
sudo apt update
sudo apt upgrade
```

## ✅ 2. Install Mosquitto and Clients
```bash
sudo apt install mosquitto mosquitto-clients
```

## ✅ 3. Enable and Start Mosquitto
```bash
sudo systemctl enable mosquitto
sudo systemctl start mosquitto
```

## ✅ 4. Set Up MQTT User Authentication
```bash
sudo mosquitto_passwd -c /etc/mosquitto/passwd onzereb
```

## ✅ 5. Configure Mosquitto
```bash
sudo nano /etc/mosquitto/mosquitto.conf
```
Paste:
```conf
listener 1883
allow_anonymous false
password_file /etc/mosquitto/passwd
listener 9001
protocol websockets
persistence true
persistence_location /var/lib/mosquitto/
log_dest file /var/log/mosquitto/mosquitto.log
include_dir /etc/mosquitto/conf.d
```

## ✅ 6. Fix File Permissions
```bash
sudo chown mosquitto: /etc/mosquitto/passwd
sudo chmod 600 /etc/mosquitto/passwd
sudo mkdir -p /var/log/mosquitto /var/lib/mosquitto
sudo chown mosquitto: /var/log/mosquitto /var/lib/mosquitto
sudo chmod 755 /var/log/mosquitto /var/lib/mosquitto
```

## ✅ 7. Restart Mosquitto
```bash
sudo systemctl restart mosquitto
```

You're ready to go!
