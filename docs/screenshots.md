## Reproducible screenshot capture

Refresh the public screenshots from a clean, named disposable simulator so the
images are consistent and contain no personal data. The checked-in dashboard
uses the app's built-in Demo Mode; its readings are generated demo data, not
physical measurements.

1. In Xcode, create or select a disposable simulator with a clear name such as
   `Wattline Docs Capture`. Do not use a simulator that contains a personal
   account, contacts, notifications, or production data.
2. Select that simulator as the run destination, select the **Wattline**
   scheme, and launch the app.
3. Put the app in each state below. Before every capture, confirm that device
   names, serial numbers, locations, account information, and notifications are
   absent or redacted.
4. Find the simulator UDID, then use this exact capture form for the matching
   filename:

   ```bash
   xcrun simctl io <SIMULATOR_UDID> screenshot docs/images/<name>.png
   ```

5. Open and inspect each saved PNG at full size before committing it. Verify
   that the intended state is visible, the text is readable, no sensitive
   identifier appears, and the image will work with the README alt text.

Capture these three images:

| File | Required app state |
| --- | --- |
| `docs/images/onboarding.png` | The initial connection screen, with **Connect a device** and **Try Demo Mode** visible. |
| `docs/images/nearby-devices.png` | The discovery screen, showing the **Devices** title and **Looking for Wattline devices** scanning state, with only demo or redacted device details. |
| `docs/images/dashboard.png` | The Demo Mode dashboard, with the **DEMO** badge visible and no physical readings or personal identifiers implied. |

## Cold-read record

1. **Yes.** Quick Start begins with **Connect a device**, and the following section identifies Bluetooth Low Energy as Wattline's everyday, direct connection.
2. **Yes.** Quick Start says to allow Bluetooth access and then choose the power station under **Nearby devices**; the discovery capture shows the scanning state.
3. **Yes.** The Bluetooth section and troubleshooting steps say to enable Bluetooth, keep the power station on and nearby, then return to **Connect a device** to scan again.
4. **Yes.** The later Optional router access section explicitly says BLE is everyday, router access is optional, and it is not required for Bluetooth discovery or normal nearby use.

## Documentation acceptance check

- [x] A first-time owner can follow Quick Start without a router.
- [x] Bluetooth permission and nearby-device discovery are explained.
- [x] The README distinguishes optional OpenWrt/wattlined access from BLE.
- [x] Every image has descriptive alt text and no sensitive identifiers.
- [x] The companion repository link resolves.
