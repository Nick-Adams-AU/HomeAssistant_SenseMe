## Custom Haiku with SenseME fan and light
The Haiku with SenseME fan is a WiFi connected fan and installable light. This custom component uses TomFaulkner's [SenseMe](https://github.com/TomFaulkner/SenseMe) library to communicate with the fan. This library will be automatically installed by Home Assistant.

### Installation
Requires Home Assistant release 0.88 or above. All you have to do to use this component is copy the senseme directory to your config/custom_components directory.

### Configuration
Automatic fan discovery using Tom's library was extremely patchy for me. Sometimes fans were found and other times, they weren't. I prefer to hard-code my fans with their fixed IP addresses.

For included fans you can now specify a ```friendly_name``` to use instead of ```name``` in Home Assistant. This is handy for grouped fans. Controlling any fan in a group will affect all fans of that group. Default value is the same as ```name ```. Also new in the include section is the ```has_light``` boolean which when ```true``` will add a light component along with the fan. The default for ```has_light``` is ```true```. The included fan section must have a ```name ``` variable and it must must match the name in the Haiku app.
```yaml
# enable Haiku with SenseMe ceiling fans
senseme:
  # used to include only specific fans
  include:
    - name: "Studio Vault Fan"
      friendly_name: "Studio Fan"
      has_light: false
      ip_address: 192.168.1.3
    - name: "Family Room Fan"
      friendly_name: "Family Fan"
      has_light: false
      ip_address: 192.168.1.4
```

### Problems
* Occasionally changes to the fan state fail to connect to fan and make the change, usually as a network (python socket) error. Same thing is true for the SenseMe background task which gets the complete fan state every minute.
* Originally the Senseme custom component auto-detected both the existence of a light and the fan's group but longer term usage showed a problem with consistently auto-detecting these values. This version no longer auto-detects these values and requires the user to specify them in advance.

### Thanks
This component is mostly created by [Mike Lawrence](https://github.com/mikelawrence/homeassistant-custom-components). Thanks Mike!
