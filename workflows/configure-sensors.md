# Set Up Sensors and Verify Readings

Read native current and voltage directly when electrical units are all you need.
Use a sensor model to convert a signal to an engineering measurement such as
pressure. A mapping connects that model to the physical input; creating a catalog
entry alone does not connect the sensor to a dashboard.

## Before you start

Have the instrument data sheet, wiring map, actual output settings, and an
independent reference. Record the terminal identity and input for each instrument.
Confirm that fresh reports arrive before changing calibration.

## Current Core setup

Open **Devices**, select the terminal, and open **Sensor Settings**. Select
**Set up sensor inputs** when offered. Agri registers its three native
Watermark resistance inputs, DS18B20 temperature input, battery, and terminal
diagnostics. Indi LoRa registers its two current inputs, two voltage inputs,
and output-state streams. Confirm the displayed terminal identity before
continuing.

The setup is based on the identified terminal. Do not add a replacement sensor
or channel just because a reading is absent; first check the selected device,
port, and latest report.

For every supported source, use **Core → Channels → Add channel** to select a
**Measurement** and its **Core stream**, then **Save binding**. Use **Actuator**
and a **Core endpoint** for output command destinations. Register reported state
shadows separately from their endpoints. This creates the dashboard channel;
sensor models and scaling are configured separately below.

## Map an analog transmitter to engineering units

For supported current or voltage inputs, open **Devices → Sensor Settings** and
expand **Map sensors to inputs**. Select the stream's matching **Sensor model**,
confirm its measurement range and electrical signal range, and select **Save
sensor mapping**. A model can provide the signal endpoints directly; a generic
measurement model may ask for **Signal minimum** and **Signal maximum** in mA or
V. Enter the transmitter's configured endpoints, not an assumed data-sheet
default. A current transmitter must use a current input; a voltage transmitter
must use a voltage input. The message after saving distinguishes a saved mapping
from one that Core has made effective.

Native Indi LoRa current inputs measure 0–20 mA. A sensor model can map a
transmitter's 4–20 mA electrical span to its engineering units without changing
the raw electrical reading. Optional per-channel **live-zero fault detection**
is disabled by default. When enabled for a 4–20 mA transmitter, Core flags a
measured value below 3.9 mA as a fault and retains the actual measured current.

For Agri, follow [Set Up Agri Irrigation](set-up-agri-irrigation.md) to configure
each Watermark model and its temperature compensation before registering the
derived soil-tension streams in Core.

## Legacy channel calibration

| Screen | Use |
| --- | --- |
| **Instrument Manager → Sensors** | Current sensor models and Watermark setup. |
| Device **Sensor Settings**, with **ADC min**, **ADC max**, and **Save All** | Legacy channel calibration from the July manual. |

Do not enter legacy raw ADC counts into a field labeled mA or V. Current Core
models, legacy catalog entries, and installed calibrations are separate records.
Changing a catalog entry does not automatically upgrade every installed sensor.

## Legacy catalog: pressure example

Open the legacy **Sensor Catalog**. In the current Instrument Manager this is
under **Sensor Catalog → Legacy ADC catalog**. On older releases it is a separate
navigation page. Select **Add sensor**, fill in the model, and save.

The July manual uses this PT5503 example:

| Field | Manual example |
| --- | --- |
| Manufacturer | ifm efector |
| Model | PT5503 |
| Sensor type | pressure |
| Signal type | 4-20mA |
| ADC min / ADC max | 496 / 2482, only for the documented legacy acquisition path |
| Engineering unit | PSI |
| Engineering minimum / maximum | 0 / 360 |

The sensor is nominally 0–25 bar. The manual uses the manufacturer's rounded
360 psi figure. Record the chosen unit and range, and verify against a reference
gauge. Do not mix a rounded psi range with an exact bar conversion unnoticed.

## Legacy catalog: flow example

Create a separate entry for the ProSense FTS100-1002:

| Field | Manual example |
| --- | --- |
| Manufacturer | AutomationDirect (ProSense) |
| Model | FTS100-1002 |
| Sensor type | flow |
| Signal type | 4-20mA |
| ADC min / ADC max | 496 / 2482, subject to channel verification |
| Engineering unit | ft/s |
| Engineering minimum / maximum | Match the actual analog start and end points |

The July manual gives 0–9.85 ft/s as an example. Use it only if the installed
sensor's configuration and instructions permit and match those endpoints.
Read the sensor's Analog Start Point and Analog End Point before entering values.
The available range, configured analog range, and display range can differ.

Falcon's current permeate and concentrate roles select velocity measurements.
Gallons per minute is a volume rate, not velocity. A pipe-area conversion needs
the actual internal diameter and a defined conversion. Renaming ft/s as gpm does
not perform that conversion.

## Bind a legacy model to a channel

For other 4–20 mA instruments, use the same catalog procedure. Copy manufacturer
and model from the label. Select the measurement type, such as pH, temperature,
or conductivity. Enter its actual unit and the values transmitted at 4 and 20 mA.
Check configurable transmitter endpoints at the instrument itself. A data-sheet
default does not prove the current setting.

1. Open **Devices**, then the terminal and **Sensor Settings**.
2. Find channel 0 for the documented CH1 input or channel 1 for CH2.
3. Select the **Sensor Model** for each wired channel.
4. Review the copied signal, ADC, engineering-range, and unit fields.
5. Enter measured per-channel calibration values where available.
6. Select **Save All**.
7. Check **Live Preview** and then **Live Data** against the process reference.

If the page shows no channels, wait for a fresh terminal report and reopen it.
If only raw data is available, confirm the device's measurement setup before
creating additional catalog records.

## Two-point calibration for the legacy current-input path

This is a technician procedure. Isolate the process sensor before substituting
a calibrator. Make sure the calibrator's source/simulate mode matches the circuit.
Do not drive a powered loop with another current source.

1. Connect the calibrator to the input signal and return using the wiring drawing.
2. Source **4.00 mA**. Wait for a fresh, stable reading in **Live Data**.
3. Record the raw count and enter it as that channel's **ADC min**.
4. Source **20.00 mA**. Record the stable raw count as **ADC max**.
5. Select **Save All**.
6. Check both endpoints and an intermediate point against the expected engineering values.
7. Isolate power as required, restore the sensor, and verify the process reading.
8. Record reference equipment, date, endpoints, results, and installer.

For the legacy hardware described in the manual, 496 and 2482 are starting
counts at 4 mA and 20 mA. They are not universal constants for all Modulink inputs.
Rev E specifies these defaults for the documented Indi Wi-Fi and legacy LoRa
boards, with a calibrator optional for precision verification. Earlier forms used
480 / 2400; correct those only on the applicable legacy path. Compare the process
reading with an independent reference and record whether a precision check was
performed. Do not adjust endpoints merely to make an unexplained discrepancy disappear.

For a linear 4–20 mA example, 12 mA is halfway between the configured engineering
endpoints. A 0–360 psi mapping should therefore read about 180 psi. Apply the
accuracy tolerance agreed for the actual instrument and acquisition chain.

## Recognize invalid readings

For current Core inputs, live-zero is disabled by default. An unconnected
input may correctly report near 0 mA. Enable live-zero per channel when using a
transmitter that requires a live zero; the fault threshold is below 3.9 mA and
the measured current remains visible. Check wiring and sensor power when a
fault is reported.

Older ADC-based releases can display **Fault (no loop)** or **Fault / no loop**.
The July manual's approximate 3.5–3.6 mA thresholds apply only to that legacy
interpretation, not to the current Core live-zero policy.

Treat **Fault (over-range)** as invalid until investigated. Do not widen the
engineering range to hide a wiring fault. Stale or rejected measurements also
must not be treated as current process values.

## Acceptance check

- [ ] Every wired input has the correct unit and range, plus a sensor model when engineering scaling is needed.
- [ ] Physical input and software identity are recorded.
- [ ] Endpoints and an intermediate reading meet the agreed tolerance.
- [ ] A fresh process reading agrees with the independent reference.
- [ ] Each input's fault policy matches its intended use; check live-zero when enabled.
- [ ] Application roles use the intended measurements.

Next: [Set Up Falcon](set-up-falcon.md) or [Set Up Agri Irrigation](set-up-agri-irrigation.md).

Last reviewed: 2026-09-27.
