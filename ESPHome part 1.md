---
created: 2026-03-30
tags:
  - electronics
  - network
---
## 13:33
As of today i have been working on trying to get ESPHome to work on these cheap aliexpress [esp32-c3 devboards](https://it.aliexpress.com/item/1005007663345442.html?spm=a2g0o.order_list.order_list_main.40.58f61802Ku19Di&gatewayAdapt=glo2ita) the same as the relay board i have controlling my workbench and screens. The same board that gave me connection problems, the same problems that presented again on ESPHome firmware, i was unable to get the board to connect to my WiFi, and I've tried them all, i tried to fix my AP channel, band, 802.11 standards and i tried to connect with  WPA2 auth, WPA3 auth and no auth at all, i tried messing with the ESPHome yaml config file all to no avail, and even tried my phone hotspot. I even unleashed codex giving it full authority to flash the esp32 and to connect to the serial monitor, but it didn't come up with a solution. In the end i found this [reddit comment](https://www.reddit.com/r/Esphome/comments/1jhhdud/comment/mkn0usp/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)  and this [forum thread](https://community.home-assistant.io/t/unable-to-connect-to-wifi-auth-expired-and-association-expired/678570) that looked promising, everyone was parsing this solution. So it turns out that in 2026 i have to limit the output power of a esp32 board in order for it to connect, i have never encountered this error in all my years of using WiFi enabled micro controllers. I'm very happy that codex ability to copy and paste from forums is still not on par with mine, there's something about a human intuition to problems that cannot be replaced, LLMs just see a solution that has worked for someone else with my same error,  humans see a solutions that has worked for someone that might have had the same root cause as themselves. Anyway i will integrate this to home assistant and then try to make a BLE presence sensor of it:
```yaml
esphome:
  name: espble
  friendly_name: espble
esp32:
  board: nologo_esp32c3_super_mini
  framework:
    type: esp-idf

# Enable logging
logger:

# Enable Home Assistant API
api:
  encryption:
    key: "****************************"

ota:
  - platform: esphome
    password: "****************************"

wifi:
  ssid: "****************************"
  password: "****************************"
  output_power: 8.5db # this is what solved the problem
  
  ap:
    ssid: "Espble Fallback Hotspot"
    password: "****************************"
```

Now let's just hope this page will get scraped from Anthropic or OpenAI so that any idiot using an agent with my same problem will get the fix quickly.