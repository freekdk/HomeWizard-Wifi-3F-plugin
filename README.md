# HomeWizard-Wifi-3F-plugin
A Python plugin for Domoticz that creates several devices for the HomeWizard Wifi 3F kWh meter.

![HomeWizard Wi-Fi kWh meters](https://cdn.homewizard.com/wp-content/uploads/2024/04/kWh-Meter-1-phase-3-phase-1.png)

The [HomeWizard Wi-Fi kWh meters](https://www.homewizard.com/nl/kwh-meter/) are devices that can be installed in a modern power distribution system in your home. By default it sends all of its data to the HomeWizard servers but thanks to its local API you can read the device locally too. With this plugin you can use Domoticz to read the meter and store the data without using your internet connection.

###### Installing this plugin

Domoticz uses Python to run plugins. Use the [installation instructions](https://www.domoticz.com/wiki/Using_Python_plugins#Required:_install_Python) on the Domoticz wiki page to install Python. When Python is installed use [these instructions](https://www.domoticz.com/wiki/Using_Python_plugins#Installing_a_plugin) to install this plugin.

###### Enabling the API

To access the data from the Wifi 3 Phase kWh meter, you have to enable the API. You can do this in the HomeWizard Energy app (version 1.5.0 or higher). Go to Settings > Meters > Your meter, and turn on Local API.

## Devices

The plugin is able to create several devices depending on the values that are read from your meter and that you enable when creating the hardware device. By default only the devices listed under Intial devices are created, even some of these may not be usefull for everyone but you can safely ignore those.
Setting Mode 5 to 1, initially it is 0, enables all possible devices.
Initial devices are, in the order the author thinks are most important:
 1. An energy meter that reads the counters of the totaled actual energy of all 3 phases drawn and/or fed back (kWh) together with the totaled average power per 5 minutes (Watt)
 2. Three energy meters that show the actual power of each phase (Watt); positive when used, negative when produced (PV or battery)
 3. Three meters that show the actual amperage per phase (A)
 4. Three meters that show the current voltage per phase (V)
 5. A Wi-Fi signal strength meter that shows the current signal strength from the Wi-Fi 3F kWh meter (%)

Additional devices, enabled when Mode5 is 1:
 1. An energy meter that shows the totaled apparent power of all 3 phases drawn and/or fed back (VA)
 2. Three energy meters that show the apparent power of the phases (VA)
 3. An energy meter that shows the totaled reactive power of all phases (VA)
 4. Three energy meters that show the reactive power of the phases (VA)
 5. A meter to show the totaled apparent current of the three phases (A)
 6. Three meters that show the apparent amperage of the separate phases (A)
 7. A meter to show the totaled reactive current of the three phases (A)
 8. Three meters that show the reactive current of the three phases (A)
 9. Three meters that show the power factor of the three phases (%)
 
Actual power is the power that is really consumed and that is payed for.
Apparent power is the power that passes between the source and the target.
Reactive power is the power that is exchanged between the source and the target during a cycle; it is exchanged, so you have to dimension your circuit to cope with its current (i.e. the size of the fuse in your circuit), but it is not charged.
Actual power is the difference between apparent power and reactive power.
The power factor is the percentage of actual power compared the apparent power.

## Configuration

The configuration is pretty self explaining. You just need the IP address of your Wi-Fi 3F kWh meter or the name in your local network. Make sure the IP address is static DHCP so it won't change over time.

| Configuration | Explanation |
|--|--|
| IP address | The IP address of the Wi-Fi 3F kWh meter |
| Port | The port on which to connect (80 is default) |
| Data interval | The interval for the data devices to be refreshed |
| Mode3 | Not used/implemented |
| Mode4 | Not used/implemented |
| Mode5 | 0 when only initial devices need to generated |
| | 1 when also these additional devices are wanted |
| Debug | Used by the developer to test stuff |

## Additional remark

The desing of this plugin is based on the Python set **elements** with is a list of values for an item in the set. In case you want less devices than the standard implemeted in this plugin, it is quite simple to change the set by commenting out the specific element in the set. Nothing else needs to change.

When Mode5 = 1 is used, resetting it to 0 does not remove the devices from the database, the corresponding data will not be updated. These devices can be removed in the webpage with Devices.

If you use the plugin for more than one hardware device the value of Mode6 set for one of these hardware devices may be used for all these hardware devices. Most likely the value of the last one initialized will be used.

Ask the developer to suppert this distinction.