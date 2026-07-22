# Wattline Owner Documentation Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish a BLE-first, owner-facing README with real Wattline screenshots and a concise optional OpenWrt/wattlined path.

**Architecture:** The root README is the public entry point and keeps its reader on the direct Bluetooth journey. Screenshot files live in `docs/images/`; `docs/screenshots.md` makes them reproducible. The router companion is linked, not duplicated, so the Apple repository remains focused on Wattline owners.

**Tech Stack:** Markdown, GitHub rendering, Xcode, iOS Simulator, `xcrun simctl`.

## Global Constraints

- Make BLE the primary and first connection method.
- Do not claim a router, GoodCloud, or remote access is needed for ordinary device use.
- Use only real simulator captures; do not include personal, device, router, account, token, or Bluetooth identifiers.
- Link the optional companion only as https://github.com/keithah/openwrt-wattline.
- Keep long-lived user documentation free of source paths and line numbers.
- Do not claim deployed relay validation before replacement hardware is available.

---

### Task 1: Establish the public documentation entry point

**Files:**
- Create: `README.md`
- Create: `docs/screenshots.md`

**Interfaces:**
- Consumes: visible app language: “Connect a device”, “Nearby devices”, “Settings”, and “Try Demo Mode”.
- Produces: the repository’s owner-facing landing page and the screenshot-refresh procedure used by Task 2.

- [ ] **Step 1: Write the acceptance checklist before prose**

Add this checklist to the bottom of `docs/screenshots.md` before drafting the README:

```markdown
## Documentation acceptance check

- [ ] A first-time owner can follow Quick Start without a router.
- [ ] Bluetooth permission and nearby-device discovery are explained.
- [ ] The README distinguishes optional OpenWrt/wattlined access from BLE.
- [ ] Every image has descriptive alt text and no sensitive identifiers.
- [ ] The companion repository link resolves.
```

- [ ] **Step 2: Verify the checklist is initially unmet**

Run:

```bash
test -f README.md && exit 1 || exit 0
```

Expected: exit 0 because the public README does not yet exist.

- [ ] **Step 3: Draft the BLE-first README**

Create `README.md` with these sections in this order:

```markdown
# Wattline

Wattline is an iPhone, iPad, and Mac companion for compatible power devices.

## Quick Start

1. Install and open Wattline.
2. Choose **Connect a device** and allow Bluetooth access when asked.
3. Turn on the power station and keep it nearby.
4. Choose it under **Nearby devices**.
5. Use the dashboard to view live power and port status.

## Bluetooth is the everyday connection

Wattline connects directly to your power device over Bluetooth Low Energy.
You do not need a router or cloud account to discover, connect to, and use a
nearby device.
```

Continue with screenshots, troubleshooting, optional router access, and a
short development section. Use the exact companion URL from Global
Constraints. State that remote relay deployment still needs hardware
validation.

- [ ] **Step 4: Document reproducible screenshot capture**

Add `docs/screenshots.md` instructions that use a named disposable simulator,
launch the `Wattline` scheme, and save the three images below:

```markdown
docs/images/onboarding.png
docs/images/nearby-devices.png
docs/images/dashboard.png
```

Include the exact capture form:

```bash
xcrun simctl io <SIMULATOR_UDID> screenshot docs/images/<name>.png
```

Explain which app state each image must show and require checking the image
before committing it.

- [ ] **Step 5: Run documentation structure checks**

Run:

```bash
test -f README.md
test -f docs/screenshots.md
rg -n 'Quick Start|Bluetooth is the everyday connection|openwrt-wattline|Troubleshooting' README.md
rg -n 'Documentation acceptance check|simctl io' docs/screenshots.md
```

Expected: every command exits 0.

- [ ] **Step 6: Commit**

```bash
git add README.md docs/screenshots.md
git commit -m "docs: add BLE-first Wattline guide"
```

### Task 2: Capture and wire in real owner-journey screenshots

**Files:**
- Create: `docs/images/onboarding.png`
- Create: `docs/images/nearby-devices.png`
- Create: `docs/images/dashboard.png`
- Modify: `README.md`
- Modify: `docs/screenshots.md`

**Interfaces:**
- Consumes: Task 1 capture instructions and public README sections.
- Produces: three safe, descriptive app captures embedded in the owner journey.

- [ ] **Step 1: Create a disposable iOS simulator and confirm the app builds**

Run:

```bash
xcrun simctl create "Wattline Docs" "iPhone 17 Pro" "com.apple.CoreSimulator.SimRuntime.iOS-26-5"
xcodebuild build -project Wattline/Wattline.xcodeproj -scheme Wattline \
  -destination 'platform=iOS Simulator,name=Wattline Docs' CODE_SIGNING_ALLOWED=NO
```

Expected: the build exits 0. Record the simulator UDID in the capture guide
only while capturing; do not commit it.

- [ ] **Step 2: Capture the onboarding screen**

Boot the simulator, launch the app in its first-run state, inspect the screen,
and capture the visible **Connect a device** onboarding state:

```bash
xcrun simctl io <SIMULATOR_UDID> screenshot docs/images/onboarding.png
```

Expected: no account, router, or device identifier is visible.

- [ ] **Step 3: Capture nearby-device discovery and a connected dashboard**

Use the app’s simulator-safe Demo Mode for the connected state. Capture the
nearby-device empty/discovery state and the connected dashboard as two
separate screenshots:

```bash
xcrun simctl io <SIMULATOR_UDID> screenshot docs/images/nearby-devices.png
xcrun simctl io <SIMULATOR_UDID> screenshot docs/images/dashboard.png
```

Expected: the screenshots demonstrate discovery and the post-connect value
without presenting simulated telemetry as physical measurement.

- [ ] **Step 4: Embed images with owner-oriented alt text**

Place these image references immediately after Quick Start and the BLE section:

```markdown
![Wattline welcome screen with a Connect a device button](docs/images/onboarding.png)
![Wattline Devices screen looking for nearby power devices](docs/images/nearby-devices.png)
![Wattline demo dashboard showing power-device status](docs/images/dashboard.png)
```

Add a one-sentence caption that identifies demo data where relevant.

- [ ] **Step 5: Verify image files and README links**

Run:

```bash
file docs/images/onboarding.png docs/images/nearby-devices.png docs/images/dashboard.png
rg -n 'docs/images/(onboarding|nearby-devices|dashboard)\.png' README.md
```

Expected: each file reports PNG image data and the README contains all three
relative links.

- [ ] **Step 6: Commit**

```bash
git add README.md docs/images docs/screenshots.md
git commit -m "docs: add Wattline app screenshots"
```

### Task 3: Cold-read, link, and publish-readiness review

**Files:**
- Modify: `README.md`
- Modify: `docs/screenshots.md`

**Interfaces:**
- Consumes: completed public guide and screenshot assets.
- Produces: a cold-reader-validated documentation change ready for a PR.

- [ ] **Step 1: Perform the owner cold-read**

Read `README.md` top to bottom while answering these questions in
`docs/screenshots.md` under a new `## Cold-read record` heading:

```markdown
1. Can a first-time owner identify BLE as the default path?
2. Can they reach Nearby devices after granting Bluetooth permission?
3. Do they know what to do when no device appears?
4. Can they tell that OpenWrt/wattlined is optional?
```

Write a one-line evidence-based answer for each question and revise the README
where an answer is not clearly yes.

- [ ] **Step 2: Check external companion link and prohibited overclaims**

Run:

```bash
curl --fail --head --location https://github.com/keithah/openwrt-wattline
rg -n -i 'required router|router required|relay validated|hardware validated' README.md docs/screenshots.md && exit 1 || exit 0
```

Expected: the link command exits 0 and the overclaim scan exits 0.

- [ ] **Step 3: Run final documentation hygiene checks**

Run:

```bash
git diff --check main...HEAD
git status --short
```

Expected: no whitespace errors; only the intended README, guide, and images
are changed.

- [ ] **Step 4: Commit**

```bash
git add README.md docs/screenshots.md
git commit -m "docs: validate Wattline owner guide"
```
