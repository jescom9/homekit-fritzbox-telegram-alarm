# HomeKit + FRITZ!Box + Telegram Alarm

A small, open-source starter for a **self-monitored home alarm**: compatible sensors feed Home Assistant and Alarmo, Apple Home controls the alarm, and Telegram delivers an alert when it triggers.

**Status:** configuration templates and a setup guide. YAML syntax has been checked; this has not been tested on your alarm hardware. Your existing alarm model and the billing period of your $60 subscription are still unknown.

```text
Door / motion sensors → Home Assistant + Alarmo → HomeKit Bridge → Apple Home
                                  │
                                  └→ Telegram alert
FRITZ!Box → optional presence reminder
```

## What is included

- A HomeKit bridge exposing the Alarmo security-system tile.
- A Telegram alert on the `triggered` state and a separate alarm-unavailable alert.
- An optional, disabled FRITZ!Box presence reminder.
- [Setup instructions](docs/setup.md), [hardware acceptance checks](docs/testing.md), [repository research](docs/repositories.md), and a [short video script](docs/video-script.md).

Alarmo supplies the alarm state machine and sensor rules. This repository supplies configuration around it; it does not contain a replacement alarm firmware or a sensor driver.

## What you need

An always-on Home Assistant host, compatible door/motion sensors, Alarmo, an iPhone, and a HomePod or supported Apple TV home hub for control and Home notifications away from home. Telegram alerts require internet access. A FRITZ!Box is optional. A local siren is optional and must be configured separately.

Existing proprietary sensors may need replacement. Sensors paired only with Apple Home are not automatically available to Home Assistant; confirm an integration, Matter sharing, or a deliberate re-pairing path first.

## Start here

1. [Check compatibility and install the integrations](docs/setup.md).
2. Configure your sensors and alarm modes in Alarmo.
3. Copy the example secret values into your **local** Home Assistant `secrets.yaml` and replace them.
4. Merge the configuration snippet and install the package as described in the guide.
5. Pair the generated bridge with Apple Home and complete the acceptance checks.

Keep your current service until you have decided that self-monitoring meets your needs and tested the full setup. This starter provides no monitoring operator, emergency dispatch, cellular backup, or guaranteed delivery. Power/internet outages and device failures need separate planning.

## The $60 comparison

If the subscription is **$60/month**, that is **$720/year** before replacement costs. If it is **$60/year**, annual savings start at $60. Subtract hardware, electricity, and any services you choose; no subscription savings have been verified for your household.

HomeKit camera recording, if added later, has separate hardware and service requirements and is outside this starter.

## Upstream projects

[Alarmo](https://github.com/nielsfaber/alarmo) documents Apple HomeKit operation. [Home Assistant HomeKit Bridge](https://www.home-assistant.io/integrations/homekit/) provides the Apple Home connection. [Telegram bot](https://www.home-assistant.io/integrations/telegram_bot/) supplies the notifier. [FRITZ!Box Tools](https://www.home-assistant.io/integrations/fritz/) supplies optional router presence.

For an existing Homebridge installation, [homebridge-fritz-platform](https://github.com/seydx/homebridge-fritz-platform) is a particularly close FRITZ!Box + Telegram + HomeKit match. See [the comparison](docs/repositories.md) before choosing a stack.

## Contributing and license

Contributions with hardware model, software versions, reproduction steps, and sanitized configuration are welcome. Do not attach tokens, PINs, pairing codes, chat IDs, or household presence logs.

Original material in this repository is [MIT licensed](LICENSE). Linked upstream projects retain their own licenses. No upstream source code is vendored here.
