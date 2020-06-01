# Usage

## View Device List

```sh
pio device list
```

## Upload Firmware

```sh
pio run -t upload --upload-port /dev/ttyUSB0 # --upload-port from pio device list
```

## Backlogs

### Garage

**Switch 1 (closed)**: GPIO4 (D2)
**Switch 2 (opened)**: GPIO5 (D1)
**Relay 1i**: GPIO12 (D6)

```
Backlog
  Module 18;
  PowerOnState 0;
  Gpio4 9;
  Gpio5 10;
  Gpio12 29;
  PulseTime 7;
  SwitchMode1 2;
  SwitchMode2 2;
  SwitchTopic 0;
  Rule1 1
```

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
