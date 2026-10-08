# Relevant open-source repositories

Research checked 8 October 2026. These are feature matches, not a hardware compatibility certification. Upstream projects have separate licenses and release schedules.

| Repository | Relevant role | Fit for this project |
| --- | --- | --- |
| [seydx/homebridge-fritz-platform](https://github.com/seydx/homebridge-fritz-platform) | FRITZ!Box devices in HomeKit, Wi-Fi presence, and Telegram notifications including alarm notifications | Closest single repository to the requested combination. Useful if you already use Homebridge; confirm your router and installed Homebridge version. |
| [homebridge/homebridge](https://github.com/homebridge/homebridge) | Bridge platform for third-party HomeKit accessories | Alternative platform; requires appropriate plugins and alarm rules. |
| [home-assistant/core](https://github.com/home-assistant/core) | Automation platform with FRITZ!Box Tools, Telegram bot, and HomeKit Bridge integrations | Foundation used by this starter. |
| [nielsfaber/alarmo](https://github.com/nielsfaber/alarmo) | Alarm modes, codes, sensor rules, and delays for Home Assistant | Alarm logic used by this starter; upstream documents HomeKit control. |
| [kbr/fritzconnection](https://github.com/kbr/fritzconnection) | Python access to FRITZ!Box TR-064/AHA interfaces | Building block for a custom router integration; unnecessary to install separately for this starter. |
| [python-telegram-bot/python-telegram-bot](https://github.com/python-telegram-bot/python-telegram-bot) | Python Telegram Bot API library | Building block for a custom bot; this starter uses Home Assistant's integration instead. |

The recommended architecture here is an engineering choice: keep alarm logic in Alarmo and export its security-system entity to Apple Home. FRITZ!Box has an optional presence role; it does not become a door sensor or monitored alarm by installing a repository.

Official integration references: [FRITZ!Box Tools](https://www.home-assistant.io/integrations/fritz/), [Telegram bot](https://www.home-assistant.io/integrations/telegram_bot/), [HomeKit Bridge](https://www.home-assistant.io/integrations/homekit/).
