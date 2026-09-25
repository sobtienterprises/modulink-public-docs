# Register and Commission a Terminal

Registration identifies the terminal. Provisioning assigns its hardware profile
and site information. Sensor mapping and application setup follow these steps.
An entry in **Devices** does not by itself mean the installation is complete.

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

## Verify the result

1. Open **Devices** and find the terminal.
2. Confirm identity, profile, firmware version, last-seen time, and provisioning state.
3. Open **Live Data**. Wait for at least two reports to confirm that time advances.
4. Open **Telemetry History** and confirm the expected physical channels appear.
5. Record the result in the [installation record](../reference/installation-record.md).

For the manual's two-current-input harness, physical CH1 is software channel 0
and CH2 is channel 1. Do not apply this harness map to other connectors or products.

If a configuration is queued or sent, wait for terminal feedback. A delivery
message is not proof that the terminal applied the settings or that equipment moved.

## Finish commissioning

1. [Map and verify every sensor](configure-sensors.md).
2. [Configure supported outputs](configure-instruments.md), if used.
3. Configure the application: [Falcon](set-up-falcon.md) or Irrigation.
4. Complete the [site acceptance checklist](../reference/installation-record.md).
