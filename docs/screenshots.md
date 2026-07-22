## Reproducible screenshot capture

Refresh the public screenshots from a clean, named disposable simulator so the
images are consistent and contain no personal data. The screenshots are not
created by this guide; capture them when the app state is ready for review.

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
| `docs/images/nearby-devices.png` | The discovery screen, with **Nearby devices** visible and only demo or redacted device details. |
| `docs/images/dashboard.png` | The connected or demo dashboard, showing live power and port status without personal identifiers. |

## Documentation acceptance check

- [ ] A first-time owner can follow Quick Start without a router.
- [ ] Bluetooth permission and nearby-device discovery are explained.
- [ ] The README distinguishes optional OpenWrt/wattlined access from BLE.
- [ ] Every image has descriptive alt text and no sensitive identifiers.
- [ ] The companion repository link resolves.
