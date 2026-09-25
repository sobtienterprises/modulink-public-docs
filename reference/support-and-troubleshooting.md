# Support and Troubleshooting

Use this page when a terminal does not report or a reading is not correct.

## Basestation does not open

Check that the Basestation has power and a site-network connection. Use a computer
on the same site network. If `https://modulink.local` does not open, ask the site
network owner for the Basestation address.

## Terminal does not report

Check terminal power. Check the terminal identity and product profile. For Indi
Wi-Fi, check site Wi-Fi coverage and the saved network settings. For Indi LoRa
or Agri, check LoRaWAN coverage and registration.

## Reading is not correct

Check the field wiring and the instrument data sheet. Check the configured signal
type, unit, and range. Do not change scaling values until you confirm the
instrument model and wiring.

## Output does not give the expected result

Make the equipment safe. Check the output configuration and the terminal report.
Use an independent field check to confirm the equipment state. Do not bypass an
independent safety interlock.

## Wi-Fi setup network is missing

Check the specified supply at the terminal. Allow 60 seconds without connectivity
for the documented portal to appear. A terminal that reaches its saved Wi-Fi
network does not need setup mode; look in **Devices** or **Provisioning** first.
Match the network name to the terminal's own label.

For `rejected`, `absent`, or `dhcp_fail`, use the
[Wi-Fi result table](../workflows/connect-indi-wifi.md). A DHCP error requires a
network-address check, not repeated password changes.

## Technician: return Indi Wi-Fi to setup mode

Use this only for the documented Linux network-manager installation. The terminal
must be reachable, and the technician must have its approved SSH access. Confirm
the target identity and arrange a maintenance window before changing its network.

On that terminal, run:

```sh
sudo /opt/modulink-netman/modulink-netman --factory-reset
```

This erases saved Wi-Fi settings and can disconnect the SSH session. It does not
remove the Basestation provisioning record. Rejoin the unit's setup network and
repeat [Connect Indi Wi-Fi](../workflows/connect-indi-wifi.md).

The manual provides no physical recovery-button procedure for that hardware.
If the terminal cannot be reached on any known network, contact support for the
approved recovery method. Do not erase the Basestation to recover one terminal.

## LoRa joins but no Modulink data appears

Check the exact DevEUI, the assigned radio profile, and fresh uplink frames.
Confirm the device belongs to the configured Modulink application in ChirpStack.
A join-accept alone is insufficient; verify a subsequent uplink and its receipt
in **Devices → Live Data**. Check the unit's key against its private handover.

## Falcon is blank while Devices has readings

Check the site's asset-group membership and application availability. On current
Falcon, check registered measurement assignments, type, freshness, and time policy.
On the older raw-channel form, check that CH1 uses channel 0 and CH2 uses channel 1,
and that each channel has a saved sensor model. Do not leave a current-input row
on voltage channel 16.

## Reading is consistently offset

Check sensor output endpoints, unit, physical input, and saved calibration path.
Use the [sensor verification procedure](../workflows/configure-sensors.md).
Do not apply legacy ADC counts to current Core electrical-unit fields.

## Contact support

Provide the product name, terminal identity, site, time, observed condition,
connected equipment model, and any alert text. Do not send passwords or device
keys.

Last reviewed: 2026-09-25.
