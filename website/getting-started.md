# Getting started with HomeSphere

Welcome — this short guide helps a new user set up HomeSphere and perform the
first basic tasks. Use this page for quick Git exercises (small edits, branch
merges) or as the first page in a printed quick-start.

## What you'll do

- Unbox and power the hub
- Connect the hub to your network
- Create an account and pair one device
- Run a sample scene

## Quick start (5–15 minutes)

1. Plug in the HomeSphere Hub and power it on.
2. Connect the hub to your router (Ethernet preferred). See
   `installation-and-setup.md` for full details.
3. Install the HomeSphere mobile app and create an account.
4. In the app, choose Add → Hub and follow the pairing flow.
5. Add a device (e.g., Living Room Light) and try a built-in scene: Evening.

### Minimal CLI flow (advanced)

Use the CLI only if you prefer the terminal or need to script setup:

```powershell
# discover hubs on the LAN (PowerShell)
homesphere-cli discover --timeout 5

# claim a hub with a one-time token (example)
homesphere-cli claim --token "OT-12345-EXAMPLE"
```

## Quick checklist

- [ ] Hub plugged in
- [ ] Hub connected to network
- [ ] Account created
- [ ] One device paired
- [ ] Scene executed

## Troubleshooting hints

- If the hub does not appear in the app, try rebooting your router and hub.
- Confirm your phone and hub are on the same local network for discovery.
- For device-specific pairing advice, see `devices.md` and `troubleshooting.md`.

![hub-setup-placeholder](../assets/hub-setup.png "Hub setup illustration")

This quick-start assumes a home network with DHCP enabled and no restrictive
client isolation on the Wi‑Fi network.[^1]

[^1]:
    If your network uses client isolation, temporarily disable it during setup,
    or use an Ethernet connection.
