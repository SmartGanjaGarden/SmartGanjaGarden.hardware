# SmartGanjaGarden.hardware

<details open>
  <summary>Nuki SmartLock 4.0 Pro</summary>
  
  ### Nuki SmartLock 4.0 Pro
  ![SmartLock](https://github.com/SmartGanjaGarden/SmartGanjaGarden.hardware/blob/main/src/images/nuki-smart-lock-40-pro.jpg "Nuki Smart Lock 4.0 Pro")

  <details>
  <summary>MQTT API 1.4</summary>
  <br>  
  #LockActions

  |ID|smartlock|opener|
  |------|------|------|
  |1|unlock|activate rto|
  |2|lock|deactivate rto|
  |3|unlatch|electric strike actuation|
  |4|lock ‘n’ go|activate continuous mode|
  |5|lock ‘n’ go with unlatch|deactivate continuous mode|
  |6|full lock||
  |80|fob (without action)|fob (without action)
  |90|button (without action)|button (without action)|

  #Simple Lock Actions

  Possible outcome of a simple lock action (mapping handled in the firmware of the device):

  |action|smartlock/knob|smartlock/handle|opener|
  |------|------|------|------|
  |lock|lock|lock|deactivate rto and cm|
  |unlock|unlatch|unlock|open|

  #Lock States

  |ID|smartlock|opener|
  |------|------|------|
  |0|uncalibrated|untrained|
  |1|locked|online|
  |2|unlocking|-|
  |3|unlocked|rto active|
  |4|locking|-|
  |5|unlatched|open|
  |6|unlocked (lock ‘n’ go)|-|
  |7|unlatching|opening|
  |253|-|boot run|
  |254|motor blocked|-|
  |255|undefined|undefined|

  #Doorsensor States

  |ID|name|
  |------|------|
  |1|deactivated|
  |2|door closed|
  |3|door opened|
  |4|door state unknown|
  |5|calibrating|
  |16|Uncalibrated|
  |240|Tampered|
  |255|Unknown|

  #Trigger

  |ID|name|
  |------|------|
  |0|system / bluetooth command|
  |1|(reserved)|
  |2|button|
  |3|automatic (e.g. time control)|
  |6|auto lock|
  |171|HomeKit|
  |172|MQTT|

  #Device Type

  |ID|name|
  |------|------|
  |0|Smart Lock|
  |2|Opener|
  |3|Smart Door|
  |4|Smart Lock 3.0 (Pro)|

  #Modes

  |mode|smartlock|opener|Description|
  |------|------|------|------|
  |2|door mode|door mode|Operation mode after complete setup|
  |3|-|continuous mode|Ring to Open permanently active|

  #Published Topics for Device States

  The following topic structure is available per device and updated whenever an update to a device state occurs. In addition the “last updated” timestamp is changed with every update. The retain flag is activated with all topics and QOS = 0 is used.

  |Topic|Description|Example|
  |------|------|------|
  |deviceType|Nuki device type (see Device Types)|4|
  |name|Name of the device|Home door|
  |firmware|Current firmware version of the device|3.2.0|
  |mode|ID of the lock mode (see Modes)|2|
  |state|ID of the lock state (see Lock States)|1|
  |batteryCritical|Flag indicating if the batteries of the Nuki device are at critical level|true|
  |batteryChargeState|Value representing the current charge status in %|18|
  |batteryCharging|Flag indicating if the batteries of the Nuki device are charging at the moment|false|
  |keypadBatteryCritical|Flag indicating if the batteries of the paired Nuki Keypad are at critical level|false|
  |doorsensorState|ID of the door sensor state|2|
  |doorsensorBatteryCritical|Flag indicating if the batteries of the paired Nuki Door Sensor are at critical level|false|
  |ringactionTimestamp|Timestamp of the last ring-action. Only for Nuki Opener.|2018-10-03T06:49:00+00:00|
  |serverConnected|Connection state to the Nuki server.|true|
  |timestamp|Timestamp of the retrieval of the last update|2018-10-03T06:49:00+00:00|
  |connected|Indicates if the device is currently connected to the MQTT server or not. Uses “false” as the last will message, which will be set by the mqtt server automatically if the device disconnects.|true|

  #Published and Subscribed Topics for Device Control

  The following topic structure allows to send commands to the device via a topic to which the device subscribes. For all messages QOS = 2 is used. The retain flag is not set.

  If “Allow locking” is disabled during provisioning, the device does not subscribe to the lockAction, lock and unlock topics.

  |Topic|Description|Example|
  |------|------|------|
  |lockAction|ID of the desired Lock Action. Only actions 1-6 are supported.|1|
  |lock|Set to “true” to execute the simple lock action “lock”|true|
  |unlock|Set to “true” to execute the simple lock action “unlock”|true|
  |commandResponse|The Nuki device publishes to this topic the return code of the last command it executed: <br>0 = Success<br>1-255 = Error code as described in the BLE API.<br>Note: Nuki devices can only process one command at a time. If several commands are sent in parallel the commandResponses might overlap.|0|
  |lockActionEvent|The Nuki device publishes to this topic a comma separated list whenever a lock action is about to be executed:<br>● LockAction<br>● Trigger<br>● Auth-ID: Auth-ID of the user<br>● Code-ID: ID of the Keypad code, 0 = unknown<br>● Auto- Unlock (0 or 1) or number of button presses (only button & fob actions) or Keypad source (0 = back key, 1 = code, 2 = fingerprint)<br>● Only lock actions that are attempted to be executed are reported. E.g. unsuccessful Keypad code entries or lock commands outside of a time window are not published.<br><br><br><br><br><br><br><br>| Unlatch via Keypad with Auth-ID 54321 from Code-ID 12345:<br>3,0,54321,12345,1<br><br>Auto-Unlock via App from Auth-ID 54322:<br>1,0,54322,0,1<br><br>Lock’n Go via Button:<br>4,2,0,0,0<br><br>Button configured to “no action on double click” and pressed twice:<br>90,2,0,0,2<br><br>Fob with auth-id 54322 configured to “unlatch” on triple click and pressed 3x:<br>3,3,54322,0,3|
</details>
</details>

---

<details open>
  <summary>Phoscon Conbee II Universal Zigbee Gateway</summary>
  
  ### Phoscon Conbee II Universal Zigbee Gateway
  ![RadiatorThermostat](https://github.com/SmartGanjaGarden/SmartGanjaGarden.hardware/blob/main/src/images/Phoscon_Conbee_2.png "Phoscon Conbee II Universal Zigbee Gateway")
  
  <details>
  <summary>Documentation</summary>
    <a target="_blank" rel="noopener noreferrer" href="https://phoscon.de/de/conbee2/">Phoscon Documentation</a>
</details>
</details>

---

<details open>
  <summary>Radiator Thermostat GS361A-H04/NX4911</summary>
  
  ### Radiator Thermostat GS361A-H04/NX4911
  ![RadiatorThermostat](https://github.com/SmartGanjaGarden/SmartGanjaGarden.hardware/blob/main/src/images/GS361A-H04.png "Radiator Thermostat GS361A-H04/NX4911")
  
  <details>
  <summary>Documentation</summary>
    <a target="_blank" rel="noopener noreferrer" href="https://www.pearl.de/pdocs/NX4911_11_180747.pdf">Pearl Manual</a><br>
    <a target="_blank" rel="noopener noreferrer" href="https://www.pearl.de/pdocs/NX4911_11_189446.pdf">Pearl Quickstart</a><br>
    <a target="_blank" rel="noopener noreferrer" href="https://www.zigbee2mqtt.io/devices/GS361A-H04.html">Zigbee2MQTT</a>
</details>
</details>

---

<details open>
  <summary>Shelly Button gen1</summary>
  
  ### Shelly Button gen1
  ![Button](https://github.com/SmartGanjaGarden/SmartGanjaGarden.hardware/blob/main/src/images/shelly_button_gen1.png "Shelly Button gen1")
  
  <details>
  <summary>Documentation</summary>
    <a href="https://kb.shelly.cloud/knowledge-base/shelly-button-1">Shelly Knowledge Base</a>
</details>
</details>

---

<details open>
  <summary>Shelly Door/Window gen1</summary>
  
  ### Shelly Door/Window gen1
  ![Door_Window](https://github.com/SmartGanjaGarden/SmartGanjaGarden.hardware/blob/main/src/images/shelly_door_window_gen1.png "Shelly Door/Window gen1")
  
  <details>
  <summary>Documentation</summary>
    <a href="https://kb.shelly.cloud/knowledge-base/shelly-door-window-2">Shelly Knowledge Base</a>
</details>
</details>

---

<details open>
  <summary>Shelly Plug S gen1</summary>
  
  ### Shelly Plug S gen1
  ![SmartPlug](https://github.com/SmartGanjaGarden/SmartGanjaGarden.hardware/blob/main/src/images/shelly_plug_s_gen1.png "Shelly Plug S gen1")
  
  <details>
  <summary>Documentation</summary>
    <a href="https://kb.shelly.cloud/knowledge-base/shelly-plug-s">Shelly Knowledge Base</a>
</details>
</details>

---

<details open>
  <summary>Shelly Plus Plug S gen2</summary>
  
  ### Shelly Plus Plug S gen2
  ![SmartPlug](https://github.com/SmartGanjaGarden/SmartGanjaGarden.hardware/blob/main/src/images/shelly_plug_s_gen2.png "Shelly Plug S gen2")
  
  <details>
  <summary>Documentation</summary>
    <a href="https://kb.shelly.cloud/knowledge-base/shelly-plus-plug-s-v2">Shelly Knowledge Base</a>
</details>
</details>

---

<details open>
  <summary>Sonoff SNZB-02D</summary>
  
  ### Sonoff SNZB-02D
  ![Hygrometer](https://github.com/SmartGanjaGarden/SmartGanjaGarden.hardware/blob/main/src/images/SNZB-02D.png "Sonoff SNZB-02D")
  
  <details>
  <summary>Documentation</summary>
    <a href="https://sonoff.tech/product-document/gateway-and-sensors-doc/snzb-02d-doc">Sonoff Product Documents</a>
</details>
</details>

---

<details open>
  <summary>Sonoff SNZB-02P</summary>
  
  ### Sonoff SNZB-02P
  ![Hygrometer](https://github.com/SmartGanjaGarden/SmartGanjaGarden.hardware/blob/main/src/images/SNZB-02P.png "Sonoff SNZB-02P")
  
  <details>
  <summary>Documentation</summary>
    <a href="https://sonoff.tech/product-document/gateway-and-sensors-doc/snzb-02p-doc">Sonoff Product Documents</a>
</details>
</details>

---
