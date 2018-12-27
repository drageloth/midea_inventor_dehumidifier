# Library for EVA II PRO WiFi Smart Dehumidifier appliance
Author: Andrea Barbaresi -2018-

Licence: GPL v3

This repo contains midea_inventor_lib which is a python package implementing a library to interface to the Web API provided by Midea/Inventor in order to remotely control a EVA II PRO WiFi Smart Dehumidifier device by using their cloud platform.

You can get info about the device here:

https://www.inventorappliances.com/dehumidifiers/eva-ii-pro-wi-fi-20l

The official companion Apps are available on the app stores from Google and Apple:

* Google Play: https://play.google.com/store/apps/details?id=com.inventor
* Apple Store: https://itunes.apple.com/gr/app/invmate-ii/id1109243423


Target devices
--------------
Even though the library has been designed to generically address any kind of existing midea devices, please note that at the moment the implemented functionalities work on the dehumidifier appliance only (0xA1 type devices).

If you are interested in code which is able to control Midea/Inventor Air Condition systems (0xA1 type devices) you can have a look at midea-air-condition Ruby&Rails library by Balazs Nadasdi available here:

https://rubygems.org/gems/midea-air-condition/versions/0.0.3


Prerequisites
-------------
In order to be able to control the EVA II PRO WiFi Smart Dehumidifier appliance using the provided python library, first it is necessary to download and install the official App in order to register a valid user to the cloud platform (a valid email address and password are required). Once connected with a valid user using the App, your home device has to be added to the list of configured devices (please refer to the manual of the Official App for this task).

Once having a valid registered user and the home device configured, you can use the python library to control the device via Internet using the available Web Api (both the client when the library is installed and the home device should be connected to the Internet).


Getting started
---------------
Minimal steps to use the library in your python code are reported below:

Step 1: Include the python package
```
from midea_inventor_lib import MideaClient
```

Step 2: Instantiate the MideaClient object

Using clear-text password:
```
client = MideaClient("user.example@gmail.com", "myPassword", "")
```

Using sha256 hash of the password:
```
client = MideaClient("user.example@gmail.com", "", "76549b827ec46e705fd03831813fa52172338f0dfcbd711ed44b81a96dac51c6")
```
Step 3: Activate a new session by logging in 
```
res = client.login()
if res == -1:
  print "Login error: please check log messages."
else:
  sessionId = client.current["sessionId"]
```

Step 4: Get the target deviceId by retrieving the list of configured appliances
```
appliances = {}
appliances = client.listAppliances()
for a in appliances:
  print "[id="+a["id"]+" type="+a["type"]+" name="+a["name"]+"]"
```

Step 5: Send commands to control the target device 
Get the device state:
```
res = client.get_device_status(deviceId)
if res == 1:
  print client.deviceStatus.toString()
```
Power-on:
```
res = client.send_poweron_command(deviceId)
if res:
  print client.deviceStatus.toString();
```
Power-off:
```
res = client.send_poweroff_command(deviceId)
if res:
  print client.deviceStatus.toString();
```



Client example
--------------
This repo comtains a full working client ("dehumi_control.py") which demonstrates how to use the library in order to control the EVA II PRO WiFi Smart Dehumidifier appliance.

To use the client, email address and password have to be provided via command line (clear-text password or its sha256 hash can be provided using the different options):
```
# python dehumi_control.py  -h
Usage:dehumi_control.py -e <email_address> -p <cleartext password> -s <sha256_password> -l <logfile> [-h] [-v] [-d]
```


Disclaimer
----------
Besides owning a EVA II PRO WiFi device, I have no connection with Midea/Inventor company. This library was developed for my own use and shared to other people interested on Internet of Things systems and domotic platforms. This software is provided as is, without any warranty, according to the GNU Public Licence version 3.
