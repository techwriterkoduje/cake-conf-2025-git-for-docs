# Devices

Document types for devices include sensor, actuator, and hybrid. This article
shows how to write device docs and includes examples.

## Device overview

- Name: Living Room Light
- Type: Actuator (light)
- Model: LS100
- Protocols: Zigbee, Wi‑Fi (fallback)

## Example device spec

```yaml
id: lr-light-01
name: "Living Room Light"
type: light
capabilities:
  - on_off
  - brightness
  - color_temperature
```

## How to write usage docs

1. Brief description of the device and typical placement.
2. Power and network requirements.
3. Step-by-step pairing and firmware update instructions.
4. Example automation snippets.

### Example automation (JSON)

```json
{
  "trigger": { "type": "sunset" },
  "actions": [
    {
      "device_id": "lr-light-01",
      "action": "turn_on",
      "params": { "brightness": 80 }
    }
  ]
}
```

## Device compatibility table

| Model | Zigbee | Z‑Wave | Wi‑Fi |
| ----: | :----: | :----: | :---: |
| LS100 |   ✓    |        |   ✓   |
| LS200 |   ✓    |   ✓    |       |

For contributor tips, see `style-guide.md`.
