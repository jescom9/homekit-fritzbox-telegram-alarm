# Hardware acceptance checks

**Repository verification:** the YAML templates were parsed with Home Assistant tags recognized. That checks file syntax only. Home Assistant configuration validation and all hardware checks below must be completed on your actual installation; no live home or router was accessed during repository creation.

Record your Home Assistant and Alarmo versions, router and sensor models, test date, and observed results locally. Do not publish household identifiers or logs.

| Check | Expected observation | Status at creation |
| --- | --- | --- |
| Home Assistant configuration validation | Check passes; startup logs contain no errors for the installed package | Not run |
| Telegram test action | Correct recipient receives one test message | Not run |
| Disarmed sensor event | Opening a door changes the sensor state but does not trigger Alarmo | Not run |
| Arm Away and wait for exit delay | Alarmo reaches `armed_away`; Apple Home agrees | Not run |
| Entry and trigger | An enrolled door follows the configured entry delay, then Alarmo reaches `triggered`; Telegram alert arrives | Not run |
| Disarm from Apple Home | Alarmo reaches `disarmed` using the configured bridge code | Not run |
| Open sensor when arming | Behavior matches your configured policy; verify the actual Alarmo state if Home is stuck arming | Not run |
| Home/Night sensor policy | Interior motion and perimeter sensors behave as intended for each mode | Not run |
| Local siren, if fitted | Siren sounds on trigger and stops on disarm/reset | Not run |
| Sensor unavailable | Alarmo reports the missing sensor and follows your chosen unavailable-sensor policy | Not run |
| Phone on cellular data | Remote Apple Home control and enabled notifications work through the home hub | Not run |
| Internet disconnected | Confirm local alarm/siren behavior and document that Telegram delivery is unavailable; do not assume queued delivery | Not run |
| Router or alarm host restart | Confirm recovered alarm state, sensor connectivity, bridge operation, and alert delivery | Not run |
| Power loss | Confirm your backup arrangements or record the loss of protection | Not run |
| FRITZ reminder, if enabled | A tracked phone away for ten minutes gets a reminder only while the alarm is disarmed; alarm state remains unchanged | Not run |

The package's two-minute unavailable alert needs Home Assistant and Telegram connectivity to keep running. It cannot report a dead Home Assistant host, router, or complete power outage. State-trigger timers also restart after Home Assistant reloads/restarts.

Do a supervised test with everyone in the household informed. Run the setup alongside the current alarm service long enough to identify missed events and false alarms before deciding whether to cancel that service.
