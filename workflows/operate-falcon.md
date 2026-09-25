# Operate Falcon

Complete [Falcon setup](set-up-falcon.md) and the site's commissioning checks first.
Falcon displays process data and records cleaning. Its session controls do not
operate the site's valves or pumps.

## Start-of-shift checks

1. Open **Falcon** and select the correct skid.
2. Check the count of reporting vessels and the time of the latest readings.
3. Review feed temperature, pH, and conductivity.
4. Review each vessel's differential pressure and permeate velocity.
5. Open **Alerts** at `/alerts`. Review severity, time, and affected device.
6. Investigate missing signals or unexpected readings before starting work.

Use the vessel detail view to inspect trends and compare pressure, flow, and
other available measurements. Check units before comparing values. A blank or
**no signal** indication is not a zero reading.

## Record a manual vessel session

On installations that show per-vessel **Start / Stop** controls:

1. Follow the site procedure to prepare the equipment.
2. Select **Start** on the correct vessel card. Confirm that its timer starts.
3. Perform the cleaning steps using the site's physical controls and procedure.
4. Select **Stop** on that vessel card when finished.
5. Select **Confirm stop** when prompted.
6. Confirm **Session logged** and review the elapsed time.

These buttons record a session. They do not prove that cleaning occurred and do
not open or close valves. A vessel session is distinct from a full skid cycle.

## Record a full cleaning cycle

Current Falcon also provides a cycle panel:

1. Enter **Operator** and optional **Job ref**.
2. Set **Duration (minutes)** within the displayed maximum.
3. Select **Record configured measurements** if this run needs measurement records.
   Save the measurement assignments first.
4. Select **Start cycle** and check the resulting active cycle.
5. Enter **Action** (`Clean`, `Soak`, `Flush`, or `Rinse`), **Chemistry** (`High pH`,
   `Low pH`, or `Neutral`), and **Temp** (`High` or `Ambient`). Select **Start stage**.
6. Select **Stop stage** when the phase finishes. Use **Add a note** and **Add note**
   for changes, alarms, and observations. Repeat for the remaining stages.
7. Select **End cycle**, choose **Complete** or **Abandoned**, then confirm with
   **Complete cycle** or **Abandon cycle**. Stop the final stage first when its
   final readings are required.
8. Review the saved record before handover.

If the result of starting a cycle is uncertain, use **Retry original request**
when offered. Check for an active cycle before attempting a new one. Do not create
duplicate records to work around a slow response.

Integration details and the older cycle API are in the
[Falcon API reference](../reference/falcon-api.md). An API route's existence does
not prove that its workflow matches the installed operator screen.

## Respond to an alarm

Overpressure and overtemperature warnings depend on configured limits and valid
readings. Read the affected vessel, measured value, and limit. Follow the site's
response procedure. A banner does not stop physical equipment.

The July manual describes banners clearing when the reading returns below the
limit and cycle notes retaining alarm information. Confirm the installed release's
alarm and recording behavior during commissioning. Do not use the banner as an
independent safety interlock.

## Interpret the cleaning advisory

The **looks done** advisory uses differential-pressure and concentrate-velocity
trends during a cleaning stage. A flat trend after a minimum duration can produce
an advisory. It does not establish membrane cleanliness or authorize an automatic stop.

Review the process readings and the site's cleaning criteria before ending work.
Advisory settings are available under **Configure → Cleaning advisory thresholds**
on current software. Record any changes and use values approved for the process.

## End-of-shift handover

Record the skid, job, operator, cycle/session identifiers, times, stages, and
unexpected conditions. Confirm the physical equipment state separately from the
recording state. Tell the next operator about unresolved sensor or communication faults.
