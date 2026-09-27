# Register and Commission a Terminal

Registration identifies the terminal. Provisioning assigns its hardware profile
and site information. Core setup makes the terminal's supported measurements
and outputs available; Core channel bindings put selected sources on the
dashboard. These are separate steps, and an entry in **Devices** does not by
itself mean commissioning is complete.

## Before you start

Sign in as an Operator or Admin. Have the approved product/profile mapping from
the installation handover. Use a 12-character MAC address for Indi Wi-Fi and a
16-character DevEUI for LoRa terminals. Remove separators from the MAC address
and use lowercase hexadecimal characters.

For a LoRa terminal, complete [radio registration](connect-lora-terminal.md) as well.
Adding a Modulink record does not establish a LoRaWAN join.

## Path A: Add the terminal before its first report

1. Open **Provisioning** at `/provisioning`.
2. Expand **Add Device**.
3. Select the **Device Type** that matches the terminal's transport and hardware.
4. Enter its MAC address or DevEUI from the label.
5. Select the approved **Hardware Profile** for that exact product.
6. Enter a useful **Device name** and optional **Customer ID**.
7. Select **Add Device**.

Some installed releases still show engineering labels in product/profile lists.
Use the supplied product-to-profile mapping. Do not choose a profile because its
name is similar. Missing or ambiguous profiles are a commissioning stop point.

## Path B: Use an unrecognized terminal report

1. Open **Provisioning**.
2. Find the terminal in **Unrecognized Devices** by its exact label identity.
3. Select **Provision** in its row.
4. Review the hardware profile and site fields described below.
5. Select **Provision Device**.

## Add or edit the site information

1. Find the terminal under **Provisioned Devices** and select **Edit**.
2. Check **Device name**, **Customer ID**, **Site Name**, and **Notes**.
3. Set the map location to the physical installation point.
4. Check **Profile** against the handover.
5. Keep delivery fields, such as **F-Port** and **Confirmed downlink**, at their
   approved values. They are not sensor calibration settings.
6. Select **Provision Device**.

The current source pre-fills saved site fields. Earlier releases did not. Review
every field before saving; do not assume a blank field means there is no saved value.

## Set up the terminal's Core sources

1. Open **Devices**, select the terminal, and open **Sensor Settings**.
2. Select **Set up sensor inputs** when offered. Core registers the supported
   inputs and diagnostics for the identified product. Confirm the displayed
   terminal name and identity match the physical unit before continuing.
3. Review the streams shown for this terminal. Use [Set Up Sensors](configure-sensors.md)
   for sensor models, derived measurements, and optional input policies.

Setup creates Core sources; it does not put every source on the dashboard. For
Agri, first configure the Watermark models so Core has the three derived
soil-tension streams; see [Set Up Agri Irrigation](set-up-agri-irrigation.md).
Then register each supported source in **Core → Channels → Add channel**:

1. Choose **Measurement** and select a **Core stream** for every supported
   physical measurement and diagnostic stream. Give it a useful dashboard name
   if the supplied label needs context, then select **Save binding**.
2. Choose **Actuator** and select a **Core endpoint** for each supported output
   listed for the terminal. Save each endpoint as its own channel, including
   endpoints not currently enabled for operation.
3. Reconcile your entries against the terminal's supported channel list in the
   product guide and the installation handover. Avoid duplicates: each available
   stream or endpoint can be bound once.

An output endpoint is a command destination. A relay, valve, or analog-output
state shadow is a separate reported source; register both when supported. Adding
an endpoint to Core does not send a command or authorize operation.

Use this checklist to reconcile the supported sources. The sensor setup and the
connected hardware determine which sources are available; do not create a source
that is absent from the terminal or select a lookalike from another terminal.

| Product | Register as **Measurement** | Register as **Actuator** |
| --- | --- | --- |
| Indi LoRa | Two 0–20 mA current inputs (Core electrical unit A), two 0–10 V inputs (V), relay state (boolean), and analog-output setpoint shadow (structured). | Relay endpoint and analog-output endpoint. |
| Agri | Three Watermark resistance readings (Ohm), DS18B20 temperature (°C), valve latch state (boolean), last coil-pulse current (A), battery voltage (V), reservoir-rail voltage (V), and three derived Watermark soil-tension readings (Pa; display unit may be selected in Irrigation). | Valve endpoint. |

For a current transmitter that represents a 4–20 mA engineering span, keep the
native current measurement and transmitter scaling distinct. Live-zero fault
detection is an optional policy on each current input, disabled by default; when
enabled, a measured value below 3.9 mA is flagged while the actual current stays
available. Do not confuse a sensor's 4–20 mA engineering span with the input's
0–20 mA measurement range.

## Verify the result

1. Open **Devices** and find the terminal.
2. Confirm identity, profile, firmware version, last-seen time, and provisioning state.
3. Open **Live Data**. Wait for at least two reports to confirm that time advances.
4. Open **Telemetry History** and confirm fresh measurements appear. In **Core**,
   confirm every supported stream and endpoint has its intended dashboard binding.
5. Record the result in the [installation record](../reference/installation-record.md).

For the manual's two-current-input harness, physical CH1 is software channel 0
and CH2 is channel 1. Do not apply this harness map to other connectors or products.

If a configuration is queued or sent, wait for terminal feedback. A delivery
message is not proof that the terminal applied the settings or that equipment moved.

## Finish commissioning

1. [Map sensors and verify readings](configure-sensors.md).
2. [Configure terminal settings and outputs](configure-instruments.md), if used.
3. Configure the application: [Falcon](set-up-falcon.md) or [Agri Irrigation](set-up-agri-irrigation.md).
4. Complete the [site acceptance checklist](../reference/installation-record.md).
