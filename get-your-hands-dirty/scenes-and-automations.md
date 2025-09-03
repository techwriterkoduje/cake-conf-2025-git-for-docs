# Scenes and automations

Scenes are static presets. Automations are event-driven.

## Scene example

Name: "Evening"

- Living Room Light: 50% brightness
- Thermostat: 21°C
- Front Door: locked

## Automation building blocks

- Triggers (time, sensor, location)
- Conditions (only if away, only at night)
- Actions (set state, notify, run scene)

### Sample automation: Motion-triggered hallway light

```yaml
trigger:
  type: motion
  sensor: hallway-motion-1
condition:
  - type: time
    after: "18:00"
action:
  - device: hallway-light-1
    action: turn_on
    params: { brightness: 70 }
```

## Best practices

- Prefer explicit time-based conditions when automations affect safety.
- Keep automations small and test each step.

> Note: test automations in a safe mode (simulation) before deploying to real
> devices.
