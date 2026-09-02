# Jetson TX2 SIP Server

Local SIP server demonstration on an NVIDIA Jetson TX2 using Asterisk/PJSIP and Linphone clients.

## Environment

- Hardware: NVIDIA Jetson TX2
- OS: Ubuntu 18.04.6 LTS
- Architecture: `aarch64`
- Asterisk: `13.18.3~dfsg-1ubuntu4`
- SIP server: Asterisk with PJSIP
- Network: phone hotspot / local Wi-Fi
- Jetson LAN address used during the demo: `10.142.81.126`
- SIP transport: UDP/5060
- RTP demo range: UDP/10000-10100

## SIP identities

- Device 1: `device1`
- Device 2: `device2`


## Demonstrated functions

- SIP registration for Device 1 and Device 2
- SIP MESSAGE between the two devices
- Two-way voice call
- Video call
- Asterisk server-side verification through the CLI
- Asterisk persistence after reboot

## Jetson settings:
On the Jetson:

```bash
sudo asterisk -rvvv
```

Inside the Asterisk CLI:

```text
pjsip show endpoints
pjsip show contacts
dialplan show internal
dialplan show messages
```


## Client settings

For Device 1:

```text
Username:   device1
Domain:     <JETSON_IP>
SIP server: <JETSON_IP>
Transport:  UDP
Port:       5060
```

For Device 2:

```text
Username:   device2
Domain:     <JETSON_IP>
SIP server: <JETSON_IP>
Transport:  UDP
Port:       5060
```

Use the current Jetson Wi-Fi IP reported by `ip -4 addr` rather than hard-coding the example address above after a reboot/network change.
