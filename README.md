# Usage

## View Device List

```sh
pio device list
```

## Upload Firmware

```sh
pio run -t upload --upload-port /dev/ttyUSB0 # --upload-port from pio device list
```

## Alarm Contact Settings

- **SwitchMode**: 2
- **SwitchTopic**: `<custom_topic>`

## Backlogs

### Garage

Switch 1 (closed): GPIO4 (D2)
Switch 2 (opened): GPIO5 (D1)
Relay 1i: GPIO12 (D6)

Backlog
Module 18;
PowerOnState 0;
Gpio4 9;
Gpio5 10;
Gpio12 29;
PulseTime 7
SwitchMode1 2;
SwitchMode2 2;
SwitchTopic 0;
Rule1 1

Rule1
  ON switch1#boot DO var1 %value% ENDON
  ON switch2#boot DO var2 %value% ENDON
  ON mqtt#Connected DO BACKLOG publish ha/garage/closed "%var1%"; publish ha/garage/opened "%var2%" ENDON
  ON switch1#state DO publish ha/garage/closed "%value%" ENDON
  ON switch2#state DO publish ha/garage/opened "%value%" ENDON
