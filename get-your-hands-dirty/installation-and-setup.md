# Installation and setup

This article explains how to install the HomeSphere Hub and perform the initial
setup.

## Requirements

| Item         |             Minimum |           Recommended |
| ------------ | ------------------: | --------------------: |
| Hub hardware |   HomeSphere Hub v1 |     HomeSphere Hub v2 |
| Wi‑Fi        |             2.4 GHz | Dual-band (2.4/5 GHz) |
| Mobile app   | iOS 14 / Android 10 |                Latest |

## Quick install (5–10 minutes)

1. Unbox the hub and plug it into power.
2. Connect the hub to your router using an Ethernet cable (recommended) or
   Wi‑Fi.
3. On your phone, install the HomeSphere app and create an account.
4. Follow the in-app pairing flow.

## CLI for advanced users

If you need to configure the hub on the local network, you can use the developer
CLI.

```bash
# discover hubs on the LAN
homesphere-cli discover --timeout 5

# claim a hub using a local token
homesphere-cli claim --token ABCDE-12345
```

## Notes

- Use Ethernet when possible to avoid flaky device discovery.
- If the hub doesn't appear in the app, check firewall rules on your router.

![hub-setup](../assets/hub-setup.png "Hub setup diagram")

For device setup instructions see `devices.md`.
