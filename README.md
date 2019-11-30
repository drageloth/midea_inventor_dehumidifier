                                      NEW README!!!
# midea_dehumi
This is a midea_dehumi component from barban-dev with fixed HVAC modes for use with Home Assistant

                                                    DISCLAIMER
THIS COMPONENT WAS NOT CREATED BY ME! In fact I've got minimum programming skills, as you'll probably realise from the files.
I just made the conversion so it can "properly" work on newer versions of Home Assistant (v.0.93 and up)
Original programmer is @barban-dev
https://github.com/barban-dev/midea_inventor_dehumidifier
Since I've already stated I'm not a programmer, I cannot guarantee future operation for the component, nor fully operational mode!
But it's a way to have the Midea Dehumidifier back in action to Home Assistant!

                                                READ BEFORE YOU TRY
This is a "butchered" version of @barban-dev because of little HVAC modes from Hassio. Since Midea Dehumidifier has 8 modes and Hassio
has half of that, so half the actions will be missing, but you can work the major ones without issues.

Since normal operation modes don't work anymore, they are replaced with HVAC modes. Problem with that is you don't know
which mode is which! They are posted below, so remember them or come back here to review! For a person that makes minimum usage on the
dehumidifier and doesn't care about target humidities etc, you'll only use AUTO (which is Smart Mode, ion off), DRY (which is Dryer mode
ion off for clothes) and OFF (guess what that does).
Operation modes are as follow:

EDIT!!!!
I've changed some modes (Manual doesnt state target mode for the Dehumi, so removed it) and now some have ioniser!
They are as follow:
```
Some modes now include Ioniser
FAN_ONLY -> Continious mode - Ion OFF 
AUTO  ->  Smart Mode - Ion OFF  
DRY  - >  Dryer Mode 
COOL  -> Continious mode - Ion ON
HEAT  -> Smart Mode - Ion ON
```


If someone has py knowledge and wants to fix the files, you're more than welcome!


                                                HOW TO INSTALL
                                                
Copy the 2 folders from custom_components to your hassio custom_components folder. If you have samba enabled, you can copy the entire custom_components folder inside config folder, selecting yes when you get a warning that the folder exists. It won't delete any folders you already have inside.
Restart, preferably 2 times (there seems to be a bug about libraries not loading properly the first time). 
Go to configuration.yaml and add:

```
midea_dehumi:
  username: asdf@ghjk.lz
  password: whatapassword
``` 
Where username and password are e-mail and password from the Invmate app on your phone.
Save, restart and the entity should be loaded!

If you get an error about midea_inventor_lib not found, make a duplicate copy of the midea_inventor_lib folder to /config/deps/lib/python3.6/site-packages/
If the folders don't exist, create them. ###DON"T DO THIS UNLESS NECESSARY!

If it still doesn't work, I don't know if I can help you but I'll be happy to try!
