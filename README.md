# device-setup

## Hardware setup

The project is guaranteed to run with the following hardware:
* a Raspberry Pi 3 with Raspbian Jessie-lite
* a MPU-6050 accelerometer ([look how to connect on your Pi](http://blog.bitify.co.uk/2013/11/interfacing-raspberry-pi-and-mpu-6050.html))
* [Jabra conference speaker](http://www.jabra.com/Business/speakerphones/jabra-speak-series/jabra-speak-510)

It should work also OK with some differences: Raspberry Pi 2 with a WiFi dongle,
other accelerometers or other microphones/speakers.

## Software setup

To setup an Abigail device for the first time, on the device clone the
[`abigail-device`](https://github.com/project-abigail/abigail-device/),
[`wifi-setup`](https://github.com/project-abigail/wifi-device/)
repositories and execute the setup scripts.

Use the following commands:

```shell
sudo apt-get install -y git
git clone https://github.com/project-abigail/abigail-device
git clone https://github.com/project-abigail/wifi-setup
sudo ./abigail-device/bootstrap-scripts/raspberry-pi-setup.sh
sudo ./wifi-setup/setup-scripts/raspberry-pi-setup.sh
(cd abigail-device && npm install)
(cd wifi-setup && npm install)
```

Note: these scripts take approximately 1.5 hours to execute.

When the scripts are finished executing, run the following command:
```
sudo raspi-config
```
and choose 'Advanced Options' and then 'I2C' and then 'Yes' to enable the ARM I2C interface.

Then, reboot the device.

While it reboots, clone the
[`user-setup`](https://github.com/project-abigail/user-setup/) repository on your laptop:
```shell
git clone https://github.com/project-abigail/user-setup/
```

After rebooting:

 * From the laptop, monitor available networks and connect to `Abigail wifi setup` when it appears in the list
 * Run the user-setup script to create users and the family group
   * `node user-setup/index.js`
 * Copy the file containing the device web token to the device:
   * `scp user-setup/secret.json pi@raspberrypi.local:~/abigail-device`
 * Visit http://10.0.0.1 in the browser to connect the device to wifi
 * Reboot the device

When the device starts up, you should hear the "hello" greeting.


