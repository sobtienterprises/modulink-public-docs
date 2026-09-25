# Set Up the Falcon Cleaning-Skid Dashboard

Falcon monitors reverse-osmosis cleaning skids. Set up terminals and verify their
sensor readings before creating the skid. Sign in as an Operator or Admin.

Complete the site's [asset-group setup](../reference/technician-commissioning.md)
before expecting application telemetry. The manual's browser procedure is available
under **Asset Groups**.

## 1. Prepare a role map

Record the terminal and installed measurement for each role. Feed measurements
apply to the whole skid. Vessel measurements apply to one vessel.

| Location | Role | Required measurement kind |
| --- | --- | --- |
| Feed | Temperature | Temperature |
| Feed | pH | pH |
| Feed | Conductivity | Conductivity |
| Each vessel | Inlet pressure | Gauge pressure |
| Each vessel | Outlet pressure | Gauge pressure |
| Each vessel | Permeate velocity | Velocity |
| Each vessel | Concentrate velocity | Velocity |

Confirm the physical location of the outlet-pressure sensor against the skid
drawing. Differential pressure depends on the actual pair of measurement points.
Use [Set Up Sensors](configure-sensors.md) before assigning these roles.

## 2. Create the skid

1. Open **Falcon** at `/falcon`.
2. Open **New skid**, or use the setup screen shown when no skid exists.
3. In **Skid settings**, enter **Name**.
4. Enter **Overpressure limit (psi)** and **Overtemperature limit (°C)** from
   the approved operating procedure.
5. Select **Create skid**.
6. Confirm the message asking you to select and save measurements below.

Current software saves skid settings and measurement assignments separately.
Creating a skid does not complete its sensor setup. On an existing skid, use
**Configure** and **Save settings** to change its name or limits.

## 3. Assign feed measurements

1. In **Wireless measurements → Feed water**, find each required role.
2. Choose **Measurement** by its sensor name, terminal identity, and unit.
3. Set **Maximum reading age (seconds)** to the approved freshness limit.
4. Set **Combine readings from** using the guidance below.
5. Review whether estimated values or uncertain timing are permitted by the site procedure.

The list filters by measurement kind. If a sensor is missing, check its setup,
measurement type, and registration. Do not choose an unrelated sensor to fill a blank.

## 4. Add vessels

1. Select **Add vessel**.
2. Enter **Vessel label** and optional **Bank**.
3. Assign inlet pressure, outlet pressure, permeate velocity, and concentrate velocity.
4. Repeat for each vessel. The current form allows up to 32 vessels.
5. Select **Save measurements**.

The older manual described 48 vessels and a single save operation. Those
instructions do not match the current source.

## 5. Choose how readings are combined

| Option | Use |
| --- | --- |
| The same wireless report | Inputs that arrive together in the same report. |
| The closest earlier reading | Inputs from separate reports or terminals. |
| The same report, otherwise an earlier reading | Prefer one report, with a bounded earlier-reading fallback. |

For either earlier-reading option, set **Maximum gap between readings (seconds)**.
Choose the limit from reporting intervals and the maximum acceptable difference
in measurement times. A long limit can combine process conditions from different
times; a short limit can leave results unavailable.

The form initially uses a 60-second reading age and a 10-second gap when an
earlier-reading option is selected. These are form defaults, not a recommendation
for every installation. Record the approved choices.

## 6. Verify the dashboard

1. Return to the Falcon live page and select the skid.
2. Check that feed temperature, conductivity, and pH correspond to the installed sensors.
3. Check each vessel's pressures and velocities against the role map.
4. Confirm differential pressure is consistent with the two pressure readings.
5. Open a vessel detail view and check new readings and history.
6. Record any missing, stale, or rejected measurement before accepting the setup.

If a value is empty, check the source measurement, role assignment, freshness
limit, and time-combination policy. Current Falcon uses registered measurements;
adding an old raw-channel binding is not a substitute.

## Existing installations with the older binding form

The July manual's form has **Device EUI**, **Ch**, and **Sensor** fields. For the
documented 4–20 mA harness, use channel **0** for CH1 and **1** for CH2. That form
could pre-fill **16**, which is a voltage channel. Check every row before saving.

Older Falcon telemetry routing also requires a site asset group. See the
[technician commissioning reference](../reference/technician-commissioning.md).
On current software, a **Review the previous channel assignments** message means
you must select registered measurements and save the new setup. Previous cycle
records retain their original interpretation.

Active or pending cycles can prevent changes to settings and assignments. Finish
or resolve the cycle using the operating procedure before editing the setup.

Next: [Operate Falcon](operate-falcon.md).
