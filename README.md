# Motion-activated Light (Enhanced)

A Home Assistant blueprint that turns lights on when motion is detected and off after a configurable delay — with proper restart behaviour if motion is detected again before the timer expires.

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fpetarivanov-msft%2FMotion-activated-Light-enhanced-%2Fblob%2Fmain%2Fmotion_light_enhanced.yaml)

## What it does

- Turns on a light when motion is detected
- Waits for motion to clear, then starts a countdown
- Turns the light off when the countdown finishes
- If motion is detected again during the countdown, it restarts (no flickering)
- Also handles the case where motion clears before the automation is in wait mode

## Installation

**Option A — one-click import** (requires Home Assistant 2021.3+):  
Click the badge above.

**Option B — manual:**

1. Download `motion_light_enhanced.yaml`
2. Copy it to `config/blueprints/automation/` (create the folder if it doesn't exist)
3. In Home Assistant: **Settings → Automations → Blueprints → Reload**
4. Create a new automation and select *Motion-activated Light (Enhanced)*

## Inputs

| Input | Required | Default | Description |
|---|---|---|---|
| Motion Sensor | Yes | — | A `binary_sensor` with device class `motion` or `occupancy` |
| Light | Yes | — | The light or light group to control |
| Wait time | No | 120s | How long to keep the light on after motion stops |

## Example automation

```yaml
alias: Hallway light on motion
use_blueprint:
  path: homeassistant/motion_light_enhanced.yaml
  input:
    motion_entity: binary_sensor.hallway_motion
    light_target:
      entity_id: light.hallway
    no_motion_wait: 60
```

## How it differs from the built-in blueprint

The official HA motion light blueprint only triggers on motion start. This one also triggers on motion clear, which means it correctly handles lights that were already on and catches edge cases where the automation missed the initial trigger.

## License

MIT — see [LICENSE](LICENSE)
