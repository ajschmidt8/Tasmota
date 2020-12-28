# Usage

## View Device List

```sh
pio device list
```

## Build & Upload Firmware

```sh
pio run -e tasmota -t upload --upload-port /dev/ttyUSB0 # --upload-port from pio device list
```

## Backlogs

### Garage

**Switch 1 (closed)**: GPIO4 (D2)

**Switch 2 (opened)**: GPIO5 (D1)

**Relay 1i**: GPIO12 (D6)

```
Rule1
  ON switch1#boot DO var1 %value% ENDON
  ON switch2#boot DO var2 %value% ENDON
  ON mqtt#connected DO BACKLOG event SetClosed=%var1%; event SetOpened=%var2% ENDON
  ON switch1#state DO event SetClosed=%value% ENDON
  ON switch2#state DO event SetOpened=%value% ENDON
  ON event#SetClosed DO publish2 ha/garage/closed %value% ENDON
  ON event#SetOpened DO publish2 ha/garage/opened %value% ENDON
```

```
Backlog
  Module 18;
  PowerOnState 0;
  Gpio4 160;
  Gpio5 161;
  Gpio12 256;
  PulseTime 7;
  SwitchMode1 2;
  SwitchMode2 2;
  SwitchTopic 0;
  Rule1 1;
  Gpio2 288;
  LedPower 1;
  LedState 7
```
