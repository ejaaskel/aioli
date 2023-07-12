# Aioli

This the top-level repository for the multi-speaker audio streaming project of mine, known as Aioli (once I manage to update all the repositories to the new name).

Blog post explaining what the whole thing actually is will come soon, once I get it actually working.

### Building
The system consists of two images: Raspberry Pi 2 speaker image, and Raspberry Pi 4 controller image. The image is based on `core-image-base` in `meta-raspberrypi`. Follow these steps to build:

```
repo init -u https://github.com/ejaaskel/aioli.git -b master -m default.xml
repo sync
cd poky
TEMPLATECONF=meta-audiostreamer/conf/templates/rpi2-speaker source ./oe-init-build-env build-rpi2
bitbake core-image-base
cd ..
TEMPLATECONF=meta-audiostreamer/conf/templates/rpi4-controller source ./oe-init-build-env build-rpi4
bitbake core-image-base
```

meta-rust and meta-rtlwifi are using versions that don't list `mickledore` in their compatible layers. These need to be fixed manually until the meta-layers are updated to newer versions in the manifest.

### Relevant repositories
[meta-audiostreamer](https://github.com/ejaaskel/meta-audiostreamer "meta-audiostreamer")
Meta-layer for adding all the relevant bits and pieces for the Raspberry Pi based demo system

[audiostreamer-manager](https://github.com/ejaaskel/audiostreamer-manager "audiostreamer-manager")
Rust programs responsible for connecting the speakers to the controller and managing the audio streams.

[hostapd-server](https://github.com/ejaaskel/hostapd-server "hostapd-server")
Rust program responsible for creating a webserver that can be used to configure the wlan credentials of a device.

