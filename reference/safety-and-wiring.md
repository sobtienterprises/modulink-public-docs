# Safety and Field Wiring

## Scope of these wiring examples

These examples come from the July industrial installation manual. They apply to
the four-conductor, 22 AWG harness supplied with the documented Indi Wi-Fi and
Indi LoRa (Legacy) installations. Confirm the harness against the unit's wiring
drawing before use. They are not a pinout for the current Indi LoRa or Agri.

The current Indi LoRa uses passive current inputs, voltage inputs, an analog
output, and an external relay driver. Agri uses soil probes and a latching valve.
Their connector maps must be supplied with the installation; do not infer them
from the color table below. See the [remaining installation gaps](self-install-gaps.md).

## Prepare the work

Have a DC voltmeter, the specified supply, a wire stripper, a small flat-blade
screwdriver, and connectors approved for the conductor type and size. Have the
sensor data sheet and the site's wiring drawing beside the equipment.

1. Isolate terminal and sensor power. Verify absence of voltage with a meter.
2. Confirm the power rating, polarity, signal type, and connector pin numbers.
3. Make the connected equipment safe before working on output wiring.
4. Keep loose conductors insulated. Do not connect mains AC to a terminal DC input.
5. Follow the connector maker's strip-length and tightening instructions.

The manual suggests about 7 mm of stripped conductor for its screw connection.
Use that only if it matches the fitted connector's specification. It is not a
universal strip length or torque specification.

## Industrial harness map

| Harness conductor | Function | Software channel |
| --- | --- | --- |
| Red | +24 VDC supply | — |
| Black | Supply return / GND | — |
| White | CH1, current sink input | 0 |
| Blue | CH2, current sink input | 1 |

The blue wire in the Modulink harness is an input. The blue wire in an M12 sensor
cordset can be a supply return. These are different cables. Label both ends.

## Connect terminal power

1. With the supply off, connect harness red to +24 VDC.
2. Connect harness black to supply return, 0 V.
3. Inspect the connections for exposed strands and correct polarity.
4. Complete sensor wiring with power still isolated.
5. Check the supply voltage and polarity before connecting power to the terminal.
6. Apply power and check for normal operation.

The current Indi Wi-Fi product information also describes 12 VDC operation.
These 24 VDC sensor examples do not establish compatibility at 12 VDC. In
particular, the flow sensor below requires 18–30 VDC.

## Example: ifm PT5503 pressure on CH1

This is a two-wire, loop-powered 4–20 mA sensor. The manual uses a 0–360 psi
engineering range. Confirm the supplied sensor's range and connector drawing.

| Sensor pin | Typical cordset color | Connect to |
| --- | --- | --- |
| 1, L+ | Brown | Harness red, +24 VDC |
| 2, OUT | White | Harness white, CH1 |
| 3 | Blue | Insulate separately; unused in this example |
| 4 | Black | Insulate separately; unused in this example |

The loop runs from supply positive, through the sensor, into CH1, and back through
the terminal to supply return. This two-wire sensor has no separate ground lead.
Do not substitute a pin-1/pin-3 sensor connection for the pin-1/pin-2 connection.

Check the [ifm PT5503 product information](https://www.ifm.com/gb/en/product/PT5503)
and the data sheet delivered with the actual unit.

## Example: ProSense FTS100-1002 flow on CH2

This sensor has separate power and two analog outputs. The manual uses OUT2 for
flow. The terminal and sensor share a supply return.

| Sensor pin | Typical cordset color | Connect to |
| --- | --- | --- |
| 1, L+ | Brown | Harness red, +24 VDC |
| 2, OUT2 | White | Harness blue, CH2 |
| 3, L− | Blue | Harness black, GND |
| 4, OUT1 | Black | Insulate, or connect to a separately assigned current input for temperature |

With power isolated, connect supply, return, and OUT2 as shown. Insulate unused
leads separately. Apply power and allow the sensor to start before checking data.
The manual allows 10 seconds for startup.

Confirm the output function, medium, display unit, and analog start/end settings
at the sensor. Do not assume a displayed volumetric rate has the same scaling as
a velocity signal. The [AutomationDirect product page](https://www.automationdirect.com/adc/shopping/catalog/process_control_-a-_measurement/flow_sensors/thermal_flow_sensors/fts100-1002)
links the installation instructions for this exact model. Its supply is 18–30 VDC.

## Externally powered sensor or loop

The terminal current input measures a signal; it does not provide loop power.
For the documented common-return harness:

1. Isolate both supplies.
2. Confirm that the sensor output is compatible with a passive current input.
3. Connect its signal to CH1 or CH2.
4. Connect the required loop return to the input's GND connection, as shown in the
   approved installation drawing.
5. Confirm reference and isolation requirements before joining separate supply returns.

Do not add a second receiver in parallel with an existing current-loop receiver.
Have the installer review existing PLC or panel connections before changing the loop.

## Outputs

Indi LoRa's relay driver is not a dry contact. Use an approved external relay.
Its analog output selects one mode: 4–20 mA or 0–10 V. It does not power the load.
Indi Wi-Fi's H-bridge and Agri's latching-valve output require compatible loads.

Do not connect an output without its product-specific drawing, current limits,
and approved load specification. A software state does not prove a valve moved,
a contact switched, or a motor stopped. Keep required interlocks independent.

## Wiring acceptance

- [ ] Product and harness match the drawing.
- [ ] Voltage and polarity measured before connection.
- [ ] Sensor pin functions checked against its data sheet.
- [ ] Each input labeled with the terminal identity and physical channel.
- [ ] Unused conductors insulated; cables secured and enclosure sealed as specified.
- [ ] Every reading verified using [sensor setup and calibration](../workflows/configure-sensors.md).
