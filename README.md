# home-assistant-blueprints

A collection of Home Assistant automation blueprints.

## Blueprints

### Presence-Activated Entity Controller
**`presence_activated_entity_controller.yaml`**

Turn entities on when presence is detected and off after a configurable inactivity period. This is the recommended starting point for most motion/occupancy automations — it's simpler and more reliable than the generic activity blueprint below.

- Trigger: one or more `binary_sensor` entities (motion, occupancy, or door device class)
- Optional: illuminance threshold, time windows, and blocking entities for both turn-on and turn-off
- Scenes are supported as turn-off targets — they are activated rather than turned off
- Verifies all sensors are still inactive after the wait period before turning off

---

### Generic Area Activity and Inactivity Automation
**`activity_and_inactivity_trigger.yaml`**

A more flexible variant that accepts area, device, or entity targets — not just individual binary sensors. Useful when you want to drive automations from an entire area's motion sensors rather than listing them individually.

- Trigger: entity target (binary sensors, lights, fans) or area target
- Supports illuminance cutoff, time windows, and blocking entities for both turn-on and turn-off
- Turn-off wait time is driven by an `input_number` helper (allows dynamic adjustment from the UI)
- Scenes and scripts in the turn-off target are activated rather than turned off

---

### Motion + Illuminance Activated Entity
**`motion_illuminance_activated_entity.yaml`**

The original single-sensor blueprint. Takes one motion sensor and one target entity. Less flexible than the newer blueprints but simpler to configure.

- Trigger: single motion sensor
- Target: single entity (light, switch, scene, or script)
- Optional: illuminance check, time window, turn-on and turn-off blocking entities, separate turn-off entity
- Turn-off wait is driven by an `input_number` helper

---

### Generic Zigbee Button Handler
**`zigbee_button_handler.yaml`**

Map button press events from zigbee2mqtt devices to arbitrary actions. Uses the zigbee2mqtt `event` entity (experimental HA integration).

- Trigger: one or more MQTT `event` entities
- Supports: single, double, triple, hold, and release press types
- Each press type maps to a configurable action sequence

---

### Z-Wave GE/Enbrighten Switch Double-Tap
**`zwave_js_ge_switch_event_handler.yaml`**

Respond to double-tap up/down events from GE and Enbrighten Z-Wave switches via the Z-Wave JS integration. Handles both Basic command class events and Central Scene `KeyPressed2x` events so it works across switch firmware variants.

- Trigger: Z-Wave JS value notification events from a selected Enbrighten device
- Actions: separate sequences for double-tap-on and double-tap-off

## Installation

Import any blueprint directly into Home Assistant via **Settings → Automations → Blueprints → Import Blueprint** and paste the raw URL:

```
https://raw.githubusercontent.com/jlaska/hass-blueprints/main/<filename>.yaml
```
