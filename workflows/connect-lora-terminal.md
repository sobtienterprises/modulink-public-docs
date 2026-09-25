# Connect a LoRa Terminal

Use this page for Indi LoRa, Indi LoRa (Legacy), or Agri. Radio registration and
Modulink provisioning are separate steps. Have the 16-character DevEUI, the
approved network profile, and the unit's join credentials from the handover.

## 1. Confirm radio and power requirements

Check that the gateway is installed, powered, and receiving on the site's
approved frequency plan. The documented US deployment uses US915. Use the
network profile supplied for the exact product and firmware.

Indi LoRa uses line power. Agri uses four C cells. The legacy manual's industrial
unit uses 24 VDC. Do not apply one product's power or wiring instructions to another.

## 2. Register the radio identity

The current Provisioning page has a LoRa registration panel with **Device ID**,
**AppKey**, and **Name**, followed by **Register Terminal**. That panel was built
for legacy LoRa registration. Use it only when the supplied profile mapping
confirms support for your unit.

1. Open **Provisioning** and expand the LoRa registration panel.
2. Enter the DevEUI from the unit, without spaces.
3. Enter the key supplied for that unit. Leave the field blank only if the site
   administrator confirms that the configured site default is correct.
4. Enter a useful name and select **Register Terminal**.
5. Record **Terminal registered** or **Already registered**. Check an existing
   entry before changing it.

If the panel does not support the delivered product, a technician must use the
ChirpStack console and its supplied profile. The exact current Indi LoRa and
Agri profile values still require a released installation reference; see
[Self-install Gaps](../reference/self-install-gaps.md).

## Technician path: ChirpStack registration

1. Open `http://modulink.local:8080` on the trusted site network.
2. Sign in using the site ChirpStack account. Change a temporary password if prompted.
3. Open **Tenant → Applications** and the application named in the handover.
   The July legacy installation uses **Modulink Terminal**.
4. Select **Add device**. Enter a name and the exact **Device EUI**.
5. Select the product's approved **Device profile** and select **Submit**.
6. Open **OTAA keys**. Enter the supplied **Application key** and submit.
7. Apply terminal power and open **LoRaWAN frames**.
8. Confirm a join sequence and a subsequent uplink from that DevEUI.

Do not create a replacement application merely because the expected application
is missing. The telemetry integration depends on the configured application.
Do not copy a key or radio profile from a different terminal.

### Legacy profile reference only

The July manual specifies the following for its Indi LoRa (Legacy) installation:

| Setting | Documented value |
| --- | --- |
| Region | US915, sub-band 2 |
| LoRaWAN MAC version | 1.0.3 |
| Regional parameters | A |
| Activation | OTAA |
| Device class | Class C |
| ADR algorithm | Default |
| Codec | None |
| Expected uplink interval | 3600 seconds |

The expected uplink interval is a network inactivity threshold, not a command
to report hourly. The manual describes a 15-second initial report interval and
profile-controlled reporting afterward. Confirm the installed profile's interval.
Do not apply this legacy table to Agri or current Indi LoRa.

## 3. Provision in Modulink

1. Open **Provisioning** on the Basestation.
2. Match the terminal by DevEUI under **Unrecognized Devices**, or use its pre-added record.
3. Select **Provision** and choose the approved product hardware profile.
4. Enter the site name, map position, and installation notes.
5. Select **Provision Device** and wait for terminal feedback.

If the industrial legacy profile is missing, stop. The old manual's fixed-ID
SQL insertion is not a general repair procedure for a current database. Have
the technician use the [Rev E browser profile procedure](../reference/technician-commissioning.md)
when it applies, or obtain the correct profile for the installed release.

## 4. Verify reception

1. Open **Devices**, then the terminal and **Live Data**.
2. Check at least two reports with advancing timestamps.
3. Open **Telemetry History** and confirm the expected channels.
4. Record the profile, firmware, report interval, and first-report time.

Rev E says indicator colors vary by hardware and describes join retries about
every 15 seconds. Use network frames and fresh telemetry as proof of reception.
If no report appears after two minutes, check power, DevEUI, key, profile,
gateway reception, and application selection. Do not infer join success from an LED.

Next: [Set Up Sensors](configure-sensors.md) and complete the
[commissioning checks](commission-a-terminal.md).
