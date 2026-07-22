# Wattline owner documentation design

**Date:** 2026-07-22
**Status:** Approved for implementation planning

## Reader and outcome

The primary reader is a Wattline owner with a supported power device. After
reading the README, that person can install the app, grant Bluetooth access,
find a nearby powered-on device, connect to it directly over BLE, and recover
from the common discovery and permission problems.

## Scope

This documentation change creates a public, BLE-first README for the
standalone Apple-source repository. It adds real simulator screenshots,
reproducible capture instructions, a short contributor section, and a narrow
optional-router note that links to
[openwrt-wattline](https://github.com/keithah/openwrt-wattline).

The router note explains that `wattlined` on an OpenWrt or GL.iNet router can
add LAN and optional remote access. It does not make a router a prerequisite,
and it does not duplicate the companion project's installation guide.

## Information architecture

1. A concise introduction frames Wattline as an iPhone, iPad, and Mac
   companion for compatible power devices.
2. Quick Start gives the direct BLE path: install, allow Bluetooth, keep the
   power station nearby and on, choose it from Nearby devices, then use the
   dashboard.
3. A BLE section explains the direct, local connection and clearly states that
   everyday use does not require a router or cloud account.
4. Three real screenshots tell the journey visually: welcome/onboarding,
   nearby device discovery, and the connected dashboard or settings surface.
5. Troubleshooting covers Bluetooth permission, empty discovery, reconnecting,
   and Demo Mode.
6. Optional OpenWrt and remote access briefly describes the additional route
   and links to openwrt-wattline for setup and operational details.
7. Development gives the minimum Xcode and Swift Package verification commands
   needed by contributors.

## Visual and asset requirements

Screenshots come from the app running in an iOS simulator, not from mockups.
They use demo or simulator-safe data only, contain no account identifiers,
tokens, router addresses, or Bluetooth identifiers, and have useful alt text.
They live under `docs/images/` with a small capture guide that records the
simulator, screen, and command flow used to refresh them.

If a small transport diagram is added, it has exactly two paths: direct BLE as
the primary path and OpenWrt/wattlined as the optional path. It must not imply
that GoodCloud or a router participates in BLE pairing.

## Accuracy and acceptance criteria

- The README is understandable without prior repository context.
- BLE is the first and dominant setup path.
- Every screenshot matches a visible app state and has descriptive alt text.
- The companion repository URL is verified and its role is accurately scoped.
- The README links to the capture guide and is the discoverable entry point for
  the new documentation.
- A cold-reader pass can follow the Quick Start to the intended next action.

## Out of scope

- Replacing the companion project's OpenWrt deployment documentation.
- Publishing hardware compatibility claims beyond what the app exposes.
- Claiming deployed remote-relay validation before replacement hardware is
  available.
