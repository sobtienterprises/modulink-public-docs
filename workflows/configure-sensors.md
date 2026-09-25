# Set Up Sensors and Verify Readings

A sensor model defines how to interpret a signal. A mapping assigns that model
to one physical input. Application assignments then use the resulting measurement.
Complete each step; a catalog entry alone does not connect a sensor to a dashboard.

## Before you start

Have the instrument data sheet, wiring map, actual output settings, and an
independent reference. Record the terminal identity and input for each instrument.
Confirm that fresh reports arrive before changing calibration.

## 1. Choose the setup path shown on your Basestation

| Screen | Use |
| --- | --- |
| **Instrument Manager → Sensors → Map sensors to inputs** | Current Core sensor mappings. Use electrical units such as mA or V. |
| Device **Sensor Settings**, with **ADC min**, **ADC max**, and **Save All** | Legacy channel calibration from the July manual. |

Do not enter legacy raw ADC counts into a field labeled mA or V. Current Core
models, legacy catalog entries, and installed calibrations are separate records.
Changing a catalog entry does not automatically upgrade every installed sensor.

## 2. Current sensor mapping

1. Open **Instrument Manager → Sensors**.
2. Select the terminal by name and identity.
3. If **Set up sensor inputs** is shown, complete the approved product setup.
   Some initialization operations require an Admin account.
4. Under **Map sensors to inputs**, find the physical current or voltage input.
5. Select **Sensor model**. Check its measurement range and unit.
6. Check the electrical signal range. For a compatible generic model, enter
   **Signal minimum** and **Signal maximum** in the displayed mA or V units.
7. Select **Save sensor mapping**.
8. Wait for a new reading and compare it with the independent reference.

A current-output sensor must use a current input. A voltage-output sensor must
use a voltage input. If the model needs several inputs or additional calibration,
use its advanced setup with a technician.

For Indi Wi-Fi, current measurements can require board ADC calibration before
physical measurements are available. Do not supply guessed board calibration.
For Agri, configure the three Watermark probes together in Instrument Manager;
the legacy 4–20 mA procedure below does not apply to soil probes.

## 3. Legacy catalog: pressure example

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

## 4. Legacy catalog: flow example

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

## 5. Bind a legacy model to a channel

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

## 6. Two-point calibration for the legacy current-input path

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

## 7. Recognize invalid readings

**Fault (no loop)** or **Fault / no loop** indicates an invalid low signal, not
zero pressure or zero flow. Check loose wiring, sensor power, and sensor fault
status. The manual gives approximate thresholds near 3.5–3.6 mA; the exact
threshold depends on the product and active interpretation.

Treat **Fault (over-range)** as invalid until investigated. Do not widen the
engineering range to hide a wiring fault. Stale or rejected measurements also
must not be treated as current process values.

## Acceptance check

- [ ] Every wired input has the correct model, signal range, and unit.
- [ ] Physical input and software identity are recorded.
- [ ] Endpoints and an intermediate reading meet the agreed tolerance.
- [ ] A fresh process reading agrees with the independent reference.
- [ ] Invalid or disconnected inputs are identified as faults.
- [ ] Application roles use the intended measurements.

Next: [Set Up Falcon](set-up-falcon.md), or the Irrigation setup for the site.
