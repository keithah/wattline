# Wattline

Wattline is an iPhone, iPad, and Mac companion for compatible power devices.

## Quick Start

1. Install and open Wattline.
2. Choose **Connect a device** and allow Bluetooth access when asked.
3. Turn on the power station and keep it nearby.
4. Choose it under **Nearby devices**.
5. Use the dashboard to view live power and port status.

![Wattline welcome screen with a Connect a device button](docs/images/onboarding.png)

## Bluetooth is the everyday connection

Wattline connects directly to your power device over Bluetooth Low Energy.
You do not need a router or cloud account to discover, connect to, and use a
nearby device.

Bluetooth permission lets Wattline look for compatible devices in range. If
you do not see your device under **Nearby devices**, make sure Bluetooth is
enabled, the power station is on and close by, then return to the **Devices**
screen. Wait for scanning to resume or pull down to refresh it.

![Wattline Devices screen looking for nearby power devices](docs/images/nearby-devices.png)

![Wattline demo dashboard showing power-device status](docs/images/dashboard.png)

The dashboard screenshot uses Wattline's built-in Demo Mode, so every displayed
reading is generated demo data rather than a physical measurement.

## Screenshots

For the reproducible capture procedure, see [the screenshot guide](docs/screenshots.md).

## Troubleshooting

- **Bluetooth access was denied:** On the **Devices** screen, choose **Open
  Settings** when Wattline shows its Bluetooth-access explanation. Enable
  Bluetooth access for Wattline, then return to the app.
- **No device appears:** On the **Devices** screen, keep the power station
  switched on and nearby, confirm Bluetooth is enabled, then wait for scanning
  or pull down to refresh.
- **Need a safe tour first:** Choose **Try Demo Mode** from the connection
  screen to explore the app without connecting hardware.
- **A connected device stops updating:** Move closer to the power station and
  reconnect from **Nearby devices**.

## Optional router access

BLE is the direct, everyday connection. If you also run an OpenWrt router with
`wattlined`, Wattline can use that optional local-network setup when it is
available. It is not required for Bluetooth discovery or normal nearby use.

Setup and router details live in the companion project:
[openwrt-wattline](https://github.com/keithah/openwrt-wattline).

Remote relay deployment still needs hardware validation; it is not presented
here as a deployed or validated connection path.

## Development

Open the Wattline project in Xcode. Select **Wattline** for an iPhone, iPad, or
iOS Simulator, or **WattlineMac** for macOS. Use **Try Demo Mode** when you
need a repeatable UI tour without a nearby power device. Follow the [screenshot
guide](docs/screenshots.md) when refreshing the images above.

To verify the project and its Swift packages, run the relevant Xcode command
(replace the iOS simulator placeholder with an installed destination), then:

```bash
xcodebuild test -project Wattline/Wattline.xcodeproj -scheme Wattline -destination 'platform=iOS Simulator,name=<installed iPhone simulator>' CODE_SIGNING_ALLOWED=NO
xcodebuild test -project Wattline/Wattline.xcodeproj -scheme WattlineMac -destination 'platform=macOS' CODE_SIGNING_ALLOWED=NO
swift test --package-path WattlineCore
swift test --package-path WattlineUI
swift test --package-path WattlineNetwork
```

## License

Wattline is licensed under the [GNU Affero General Public License, version 3
or later](LICENSE).
