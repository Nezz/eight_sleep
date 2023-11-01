# Eight Sleep Integration for Home Assistant
[![hacs_badge](https://img.shields.io/badge/HACS-Custom-41BDF5.svg?style=for-the-badge)](https://github.com/hacs/integration)

Home Assistant Eight Sleep integration that works with Eight Sleep's V2 API and OAUTH2

## Installation
### HACS (Recommended)

1. Add this repository to HACS *AS A CUSTOM REPOSITORY*.
2. Search for *Eight Sleep*, and choose install. 
3. Reboot Home Assistant and configure from the "Add Integration" flow.

## Prerequisites ##
### Authentication ###
To get the OAuth2 login to work you need:

- client_id
- client_secret
- user email
- user password

To get the client_id and client_secret you can setup a packet capture and a mitm CA to get the unencrypted traffic from your app. You can also decompile the APK to get the values.

The process I used was:
- Open pcapdroid and install PCAPDroid mitm
- download and install rootAVD https://github.com/newbit1/video-files/blob/master/rootAVD_Windows.gif 
  - 2 ways to root an AVD (android studio); Magisk (rootAVD) and SuperSU
- Should auto install magisk
- Run the avd root install steps then open a cmd in ..\rootavd\rootAVD
- Install the mitm cert (mitmproxy-ca-cert.cert)
- https://emanuele-f.github.io/PCAPdroid/tls_decryption the MagiskTrustUserCerts module, and then install the hashed certificate (replace mitmproxy-ca-cert.cer with the PCAPdroid certificate name) as a system certificate. 	
- Run the app and capture date in pcapdroid. 
  - Make sure you capture the data during an app login session. The data should be in the POST request from the app to auth-api.8slp.net.

## Usage ##
The integration will function similarly to the previous Home Assistant core Eight Sleep integration. It will import the Eight Sleep bed sides and account as devices.

There are a few services you can use on the <..>_bed_temperature entities:
- Heat Set
  - Sets heating/cooling level for a <..>_bed_temperature entity.
- Side Off
  - Turns off 8 sleep side. Input entity must be a <..>_bed_temperature entity.
- Side On
  - Turns on 8 sleep side in smart mode. Input entity must be a <..>_bed_temperature entity.

## TODO ##
- Streamline process for getting client_id and client_secret. It would be nice to have it (mostly) scripted or to have a preconfigured AVD available to get the values.
- Translate "Heat Set" values to temperature values in degrees for easier use.

### Credits ###
Thanks to @mezz64 for developing the previous Eight Sleep integration.

This is also based on work from https://github.com/lukas-clarke/pyEight and I will likely maintain this repo over the aforementioned one.