# Legacy Sensor Calibration Reference

Use this reference only for a documented legacy input path. Current Core sensor
models, legacy catalog entries, and installed calibrations are separate
records. Changing a catalog entry does not update every installed sensor. Do
not enter raw ADC counts in a field labeled mA or V.

For current sensor setup, use [Configure Sensors and Check Readings](../workflows/configure-sensors.md).

## Legacy screens

| Screen | Use |
| --- | --- |
| **Instrument Manager → Sensors** | Current sensor models and Watermark setup. |
| Device **Sensor Settings**, with **ADC min**, **ADC max**, and **Save All** | Legacy channel calibration. |

## Add a legacy catalog model

Open **Sensor Catalog**. In the current Instrument Manager, select **Sensor
Catalog → Legacy ADC catalog**. On older releases, Sensor Catalog is a separate
navigation page. Select **Add sensor**, enter the model details, and save.

The July manual uses this pressure example:

| Field | Example |
| --- | --- |
| Manufacturer | ifm efector |
| Model | PT5503 |
| Sensor type | pressure |
| Signal type | 4–20 mA |
| ADC min / ADC max | 496 / 2482, only on the documented legacy path |
| Engineering unit | PSI |
| Engineering minimum / maximum | 0 / 360 |

The PT5503 is nominally 0–25 bar. The manual uses the manufacturer's rounded
360 psi figure. Record the chosen unit and range. Verify it against a reference
gauge; do not mix rounded psi values with an exact bar conversion without
accounting for the difference.

The July manual's flow example is the ProSense FTS100-1002:

| Field | Example |
| --- | --- |
| Manufacturer | AutomationDirect (ProSense) |
| Model | FTS100-1002 |
| Sensor type | flow |
| Signal type | 4–20 mA |
| ADC min / ADC max | 496 / 2482, subject to channel verification |
| Engineering unit | ft/s |
| Engineering minimum / maximum | Match the configured analog start and end points |

The manual gives 0–9.85 ft/s as an example. Use that range only if the installed
sensor settings and instructions match. Read **Analog Start Point** and
**Analog End Point** before entering values. The sensor range, configured
analog range, and display range can differ.

Falcon's current permeate and concentrate roles use velocity measurements.
Gallons per minute (gpm) is a volume rate, not a velocity. Converting velocity
to volume flow needs the pipe's actual internal diameter and a defined
calculation. Renaming ft/s as gpm does not convert the reading.

## Bind a legacy model to a channel

For a different 4–20 mA instrument, copy the manufacturer and model from its
label. Select the measurement type, such as pH, temperature, or conductivity.
Enter its actual unit and the values it sends at 4 mA and 20 mA. Check the
transmitter's configured endpoints. A data-sheet default does not prove the
current setting.

1. Open **Devices**, select the terminal, and open **Sensor Settings**.
2. Find channel 0 for the documented CH1 input or channel 1 for CH2.
3. Select the **Sensor Model** for each wired channel.
4. Check the signal, ADC, engineering range, and unit fields.
5. Enter measured channel calibration values when available.
6. Select **Save All**.
7. Check **Live Preview**, then **Live Data**, against the process reference.

If no channels appear, wait for a fresh terminal report and reopen the page. If
only raw data appears, check the device measurement setup before adding catalog
records.

## Two-point calibration for a legacy current input

This is a technician procedure. Follow the wiring drawing. Isolate the process
sensor before connecting a calibrator. Set the calibrator to the correct
source/simulate mode for the circuit. Do not drive a powered loop with another
current source.

1. Connect the calibrator to the input signal and return.
2. Source **4.00 mA**. Wait for a fresh, stable value in **Live Data**.
3. Record the raw count and enter it as that channel's **ADC min**.
4. Source **20.00 mA**. Record the stable raw count as **ADC max**.
5. Select **Save All**.
6. Check both endpoints and a point between them against the expected
   engineering values.
7. Isolate power as required, restore the sensor, and check its process reading.
8. Record the reference equipment, date, endpoints, results, and installer.

On the legacy hardware described in the manual, 496 and 2482 are starting ADC
counts at 4 mA and 20 mA. They are not universal. Rev E specifies these
defaults for the documented Indi Wi-Fi and legacy LoRa boards; a calibrator is
optional for precision verification. Earlier forms used 480 and 2400 on the
applicable legacy path. Compare the process reading with an independent
reference and record whether a precision check was done. Do not adjust
endpoints to hide an unexplained difference.

For a linear 4–20 mA signal, 12 mA is halfway between the configured
engineering endpoints. For a 0–360 psi mapping, it should read about 180 psi.
Use the accuracy tolerance agreed for the instrument and acquisition path.

## Read faults on legacy and current inputs

For current Core inputs, live-zero fault detection is off by default. An
unconnected input can correctly report near 0 mA. Enable live-zero per channel
only for a transmitter that uses a live zero. A reading below 3.9 mA is then
marked as a fault, and the measured current remains visible. Check wiring and
sensor power when a fault appears.

Older ADC-based releases can show **Fault (no loop)** or **Fault / no loop**.
The July manual's approximate 3.5–3.6 mA thresholds apply only to that legacy
interpretation, not to current Core live-zero behavior.

Treat **Fault (over-range)** as invalid until investigated. Do not widen the
engineering range to hide a wiring fault. Stale or rejected readings are not
current process values.

## Acceptance check

- [ ] Each wired input has the correct unit and range, with a sensor model when scaling is needed.
- [ ] The physical input and its software identity are recorded.
- [ ] Endpoints and an intermediate reading meet the agreed tolerance.
- [ ] A fresh process reading agrees with an independent reference.
- [ ] Each input's fault policy matches its intended use; check live-zero when enabled.
- [ ] Application roles use the intended measurements.

Last reviewed: 2026-09-27.
