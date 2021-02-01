# Digital Sign
Display any URL on a balena device connected to a display via HDMI

## Hardware required

The list of items you’ll need is also included below:

- Raspberry Pi 3B/3B+ (**Note:** this project will not work with the Pi Zero or older devices with < 1GB RAM)
- 16GB Micro-SD Card (we recommend Sandisk Extreme Pro SD cards)
- Display (PiDisplay or a TV/Monitor via HDMI)
- Micro-USB cable
- Power supply

## Setup and configuration

You can deploy this project to a new balenaCloud application in one click using the button below:
[![](https://balena.io/deploy.svg)](https://dashboard.balena-cloud.com/deploy?repoUrl=https://github.com/phil-d-wilson/digital-sign)

## Controlling content

### Loading a URL

To configure the URL displayed, set the **`LAUNCH_URL`** environment variable.

### Switching URLs quickly using your web browser or Slack

Your device is also running a small webserver on port 8080. The screen will show the URL configured at `LAUNCH_URL` normally, but the webserver allows you to put other URLs on screen quickly and easily. If you tell balenaCloud to expose your device's public URL, then you can even control it with Slack (or `curl`, or anything that can use webhooks). [More details](https://github.com/mozz100/tohora/blob/master/README.md)

## Using WiFi Connect

This project includes [wifi-connect](https://github.com/balena-io/wifi-connect) which enables your device to operate as a WiFi access point and allow you to join a different WiFi network using captive portal functionality. Although you can specify a WiFi network to join when you first add your device and download the image from the balenaCloud dashboard, there may be situations where you need to change that.

WiFi Connect periodically tests for a functional internet connection. If nothing is found, the device sets itself up as a WiFi access point named `balenaDash` that you can join with a mobile device.

To use WiFi Connect you need to join the `balenaDash` network and you should see a captive portal popup. The passphrase is `balenaDash`. If not, ensure that you remain connected to the `balenaDash` network and visit the IP address of the device in a browser on port `80`. For example `http://<ip of balenaDash device>`. This will allow you to access WiFi Connect, perform a site survey and join a different WiFi network.

## Automate backlight switching

To use automatic backlight switching you’ll need to configure a few service variables for the scheduler service.

`ENABLE_BACKLIGHT_TIMER=1`
`BACKLIGHT_ON=0 8 * * *`
`BACKLIGHT_OFF=0 23 * * *`

The `BACKLIGHT_ON` and `BACKLIGHT_OFF` variables accept standard cron syntax; take a look at https://crontab.guru if you’re not familiar. For more instructions check out [our blog post](https://www.balena.io/blog/automate-the-backlight-timer-on-your-balenadash-display/).

To change the timezone for the scheduler, set the `TZ` service variable to something from the [TZ database list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).
