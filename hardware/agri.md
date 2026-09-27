# Agri

Agri is a battery-powered LoRaWAN terminal for soil monitoring and irrigation
control. It reports to the on-site Modulink Basestation.

## Main features

- Three IRROMETER Watermark 200-SS resistance inputs interpreted as soil tension.
- One DS18B20 temperature input. Its installation role depends on where the
  sensor is physically placed; soil temperature and air temperature are distinct.
- One latching-valve drive.
- Four C-cell battery power.
- LoRaWAN US915 connection.

## Use Agri when

- You need readings from the root zone.
- Field power is not available at every terminal location.
- You need to operate one compatible latching irrigation valve.

## Important limits

The valve drive is for one compatible latching valve. It is not proof that the
physical valve moved. Use independent field checks and safety controls where
they are required.

The DS18B20 reading can also be assigned as a Watermark temperature-compensation
input when available. Compensation is a separate use of the temperature reading;
it does not change the sensor's physical installation role.

## Next step

Follow [Connect Indi LoRa or Agri](../workflows/connect-lora-terminal.md), then
[Set Up Agri Irrigation](../workflows/set-up-agri-irrigation.md).

Last reviewed: 2026-09-27.
