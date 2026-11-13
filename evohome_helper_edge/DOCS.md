# Evohome Helper

Adds presence detection to a Honeywell Evohome installation: the heating is turned down
when no-one is home, and kept warm for when people arrive.

## How it works

Every interval the app reads who is home from Home Assistant and the state of the
thermostat from Evohome, and decides which mode the thermostat should be in:

- **Someone is home**: the thermostat follows its schedule.
- **No-one is home**: the thermostat is switched to the away mode, once everyone has
  been gone for the away delay.
- **No-one is home, but the schedule expects people**: for a while after the schedule
  raises a setpoint (waking up, coming home), the thermostat keeps following its
  schedule so the home is warm on arrival. This only applies to a home in daily use,
  not to one that has been empty for longer, such as during a holiday.
- **Warm outside**: with auto-eco enabled, the economy mode is used instead of the
  normal schedule when the outside temperature is close to the scheduled setpoints.

Someone arriving at an empty home is acted on right away, without waiting for the next
interval.

Manual changes on the thermostat, such as a mode or a zone override set by hand, are
left alone until they are cleared. If presence cannot be determined, for example while
Home Assistant is starting, the thermostat is left unchanged.

## Configuration

### Evohome

| Option | Description |
| --- | --- |
| `username` | The e-mail address of the Evohome account. |
| `password` | The password of the Evohome account. |
| `location_name` | The name of the location, exactly as shown in the Evohome app. |
| `away_mode` | The mode to switch to when no-one is home: `away`, `eco` (economy) or `custom`. |

### Presence

| Option | Default | Description |
| --- | --- | --- |
| `entities` | | Entities that report `home` when someone is home, such as `person.*` or `device_tracker.*`. At least one is needed. |
| `last_home_grace_time` | `86400` | Seconds after the last person left during which the home counts as being in daily use. Only a home in daily use is pre-heated. |
| `heating_schedule_grace_time` | `1800` | Seconds to keep heating after the schedule raises a setpoint, even if no-one is home yet. |
| `away_delay` | `300` | Seconds to wait after the last person left before switching to the away mode. `0` switches right away. |

### Auto-eco

| Option | Default | Description |
| --- | --- | --- |
| `enabled` | `true` | Use the economy mode when it is warm enough outside. |
| `weather_entity` | | The weather entity that provides the outside temperature, such as `weather.home`. Without it auto-eco does nothing. |
| `outside_temp_threshold` | `18.0` | Economy mode is never used while it is colder outside than this (°C). |
| `inside_temp_diff` | `1.0` | Economy mode is used when the outside temperature is within this many degrees of the highest scheduled setpoint, or above it. |

### Interval

`interval` (default `180`) is the number of seconds between checks of the thermostat.
The Evohome service limits how often it can be called, so keep this at a few minutes.
