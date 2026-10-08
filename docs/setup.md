# Setup

## 1. Check your hardware

Record your alarm model, sensor models, Home Assistant version, and subscription billing period. Confirm that sensors can report open/closed or motion states to Home Assistant independently of the subscription. Do not assume that an existing proprietary alarm or an Apple Home accessory can be reused.

Install Home Assistant on an always-on host using its [official installation guide](https://www.home-assistant.io/installation/). Add sensors through their supported integrations and verify their states before continuing. Configure a local siren separately if you want an audible alarm.

## 2. Install Alarmo

Follow [Alarmo's installation instructions](https://github.com/nielsfaber/alarmo#installation). Configure Away/Home/Night modes as needed, assign sensors, set entry/exit delays, and create a user code for disarming. Confirm the resulting entity ID; the templates assume `alarm_control_panel.alarmo`. Change every reference if yours differs.

If using a siren, configure Alarmo actions for triggering and stopping it, then test both. Review unavailable-sensor handling in Alarmo. The repository's unavailable alert watches the alarm entity, not each individual sensor.

## 3. Set up Telegram

Use [Home Assistant's Telegram bot guide](https://www.home-assistant.io/integrations/telegram_bot/) to create a bot through the verified BotFather account, start a conversation with your bot, and configure the integration in **Settings → Devices & services**. Choose **Broadcast** for outgoing alerts and add your intended chat ID as an allowed chat. No inbound router port is needed for this mode.

Find the chat's `notify` entity in the integration. In **Developer Tools → Actions**, send a test using `notify.send_message` with that entity and a plain message. Put the entity ID in the local secret described below. Store the bot token through the integration setup, never in this repository.

## 4. Install the templates

Use a Home Assistant file editor or your usual configuration access. Back up the files you edit.

1. Merge the two entries from `home-assistant/secrets.example.yaml` into your existing `/config/secrets.yaml`. Replace the placeholders. The code must match your Alarmo user code.
2. Merge `home-assistant/configuration.example.yaml` into `/config/configuration.yaml`, using the existing `homeassistant:` block if present. If packages are already enabled, keep that arrangement.
3. Copy `home-assistant/packages/home_alarm.yaml` into the configured packages folder. Replace the Alarmo ID if necessary. If port `21064` is already used by another bridge, choose an unused port.
4. Run Home Assistant's configuration check using **Developer Tools → YAML → Check configuration** where available, or your installation's supported check procedure. Fix errors before restarting.
5. Restart Home Assistant and inspect its logs for integration or automation errors.

The [package loader](https://www.home-assistant.io/docs/configuration/packages/) groups the bridge and automations into one file. Keep existing configuration; these files are snippets, not a complete Home Assistant installation.

## 5. Pair Apple Home

Find the bridge pairing notification in Home Assistant and scan its QR code using **Add Accessory** in Apple Home. The alarm should appear as a security system. Avoid exposing the same alarm on a second existing bridge.

The bridge stores the Alarmo code and supplies it for Apple Home operations; Home members who can control this accessory can therefore operate it. Configure your household access accordingly. [HomeKit Bridge](https://www.home-assistant.io/integrations/homekit/) documents this code configuration.

For remote control, configure a [HomePod or Apple TV home hub](https://support.apple.com/en-ie/102557). Enable supported alarm notifications under **Status and Notifications**, where available, and test them on each intended device using [Apple's notification guide](https://support.apple.com/en-gb/105042). Telegram is a separate alert path.

HomeKit does not display all Alarmo modes or entry-delay details. If Apple Home appears stuck arming, inspect Alarmo for a failed arming attempt before assuming that the home is protected. See [Alarmo's HomeKit limitations](https://github.com/nielsfaber/alarmo#apple-homekit).

## 6. Optional FRITZ!Box presence

Follow [FRITZ!Box Tools](https://www.home-assistant.io/integrations/fritz/) to add the router. Enable the documented TR-064 and UPnP status settings on the local network and use a dedicated router account. Identify your phone's device-tracker entity.

Replace the phone placeholder in `home-assistant/optional/fritz_presence_reminder.yaml`, then copy it into the packages folder. Check configuration, restart, and enable the automation manually. It starts disabled on every restart.

The reminder detects one phone appearing away. Wi-Fi sleep, network faults, private-address changes, guests, and people without tracked phones make router presence unsuitable as the sole basis for arming or disarming. The example sends a reminder; it never changes the alarm state.

## 7. Test before switching

Complete [the acceptance checks](testing.md). Hardware costs and subscription terms determine whether this makes sense for your home. Decide separately whether you need professional monitoring or backup connectivity.

To remove this starter, unpair **Home Alarm Bridge** in Apple Home, remove only the package files installed by this guide, remove their unused local secrets, check configuration, and restart. Keep other Home Assistant packages and integrations intact.
