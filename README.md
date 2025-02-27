# i-Drive

Model: i-Drive i11 dashcam and full series

Product link: https://youtu.be/vFdHuKhwXmQ

## Finding 1: Default Credentials Cannot be Changed

i-DRIVE dashcam's wifi password cannot be changed. Although this static, unchangeable password is paired with a second authentication factor (device pairing), its fixed nature effectively reduces security to a single factor. Since the default password is publicly known, an attacker nearby can connect to the dashcam's network and intercept traffic.

## Finding 2: Hardcoded credentials in APK to ports 9091 and 9092

a) Once i-DRIVE's SSID is connected to, the attacker sends a crafted command with "TibetList" and "000*" (redacted) to list settings of the dashcam at port 9091. 

b) There's a separate set of credentials for port 9092 (stream) that is exposed in plaintext as well, "admin" + "tib*". 

c) For settings, it's "adim" + "000*"

These credentials are used to retrieve the sensitive video footage and camera settings.

## Finding 3: Bypassing of device pairing

The dashcam's authentication mechanism relies on a default password combined with a second factor (device registration). However, the device pairing process is based on MAC address recognition, which can be bypassed. An attacker can obtain the MAC address of a paired device through methods such as ARP scanning, spoof the MAC address, and successfully connect to the dashcam without completing the pairing process. This grants unauthorized access to the device’s network.

## Finding 4: Remotely Dump Video Footage and Live Video Stream

An attacker with network access can remotely enumerate all video recordings stored on the dashcam’s SD card via port 9091. These recordings can then be converted from JDR to MP4 format. Additionally, by opening a secondary socket to port 9092 and successfully validating the challenge-response key, an attacker can stream live footage. Extracted recordings may contain sensitive information, including location data.

## Finding 5: Managing Settings to Obtain Sensitive Data and Sabotaging Car Battery

An attacker can remotely access and read the dashcam’s settings and configuration, exposing sensitive car and driver information. Additionally, they can manipulate device settings, such as lowering the volume to mask remote activity. Spoofing the MAC address of the paired device, an attacker can disable battery protection, potentially draining the vehicle's battery when parked. Further actions include deleting recorded footage, discreetly disabling recording, or performing a factory reset, effectively erasing critical evidence.

