# Setup and Verification

## 1. Install Asterisk

```bash
sudo apt update
sudo apt install asterisk
```

Check the service:

```bash
sudo systemctl status asterisk --no-pager
```

## 2. Install configuration files

Back up the existing configuration before replacing it:

```bash
sudo cp /etc/asterisk/pjsip.conf /etc/asterisk/pjsip.conf.bak
sudo cp /etc/asterisk/extensions.conf /etc/asterisk/extensions.conf.bak
sudo cp /etc/asterisk/rtp.conf /etc/asterisk/rtp.conf.bak
```

Copy the repository configuration:

```bash
sudo cp config/pjsip.conf /etc/asterisk/pjsip.conf
sudo cp config/extensions.conf /etc/asterisk/extensions.conf
sudo cp config/rtp.conf /etc/asterisk/rtp.conf
```

Before restarting Asterisk, replace the password placeholders in `/etc/asterisk/pjsip.conf` with your own passwords.

## 3. Restart Asterisk

```bash
sudo systemctl restart asterisk
sudo systemctl status asterisk --no-pager
```

## 4. Find the Jetson IP

```bash
ip -4 addr
```

Use the IPv4 address of the network interface that the SIP clients can reach. If the Jetson is connected to multiple networks, it can have multiple IPv4 addresses.

## 5. Configure the two SIP clients

### Device 1

```text
Username: device1
Password: <DEVICE1_PASSWORD>
Domain / SIP server: <JETSON_IP>
Transport: UDP
Port: 5060
```

### Device 2

```text
Username: device2
Password: <DEVICE2_PASSWORD>
Domain / SIP server: <JETSON_IP>
Transport: UDP
Port: 5060
```

## 6. Verify registration

Open the Asterisk CLI:

```bash
sudo asterisk -rvvv
```

Run:

```text
pjsip show endpoints
pjsip show contacts
```

Both endpoints should have reachable contacts after successful registration.

## 7. Test functions

1. Send a SIP MESSAGE from Device 1 to `device2`.
2. Reply from Device 2 to `device1`.
3. Place a voice call from Device 1 to `device2` and test audio in both directions.
4. Start a video call and verify video transmission.
5. Reboot the Jetson and repeat registration, messaging, and calling tests.

## 8. Troubleshooting

Enable SIP logging temporarily inside the Asterisk CLI:

```text
pjsip set logger on
```

Disable it after troubleshooting:

```text
pjsip set logger off
```

Check service logs:

```bash
sudo journalctl -u asterisk -n 100 --no-pager
```
