# Set Up Agri Irrigation

Use this workflow after the Agri terminal is registered and its Core sources
are available. It creates or resumes a monitoring station and maps its readings.
It does not open the valve or start automatic control.

## 1. Set up the terminal's native sources

Follow [Register and Commission a Terminal](commission-a-terminal.md) and use
**Devices → Sensor Settings → Set up sensor inputs**. The three native
Watermark inputs report resistance. The DS18B20 is a temperature reading.
Battery, reservoir-rail, and coil-pulse-current streams are diagnostics, not
soil sensors.

If no eligible Agri terminal appears in setup, check **Devices** for a fresh
report and a matching Agri profile and firmware identification. Use the visible
terminal details to confirm which unit is ready, then retry setup. Do not enter
an internal device identifier or create a substitute channel to work around a
missing terminal.

## 2. Configure Watermark sensors and compensation

In **Instrument Manager → Sensors**, select the terminal and open **Watermark
sensors**. Configure WM1, WM2, and WM3 together. Each Watermark resistance input
is a separate soil-tension sensor. When exactly one temperature stream from the
same terminal is available, the form preselects it; verify the choice. Assign
the same terminal's DS18B20 as the temperature-compensation input when it is
available. This compensation choice is separate from whether the physical
DS18B20 is installed in air or soil.

Select **Save Watermark sensors** after reviewing the three inputs. When saved,
the page shows compact summaries for each sensor with an **Edit Watermark
sensors** link. If the form shows no unique candidate, select the correct
temperature stream yourself or use the model reference only when appropriate.

If no compensation input is selected, the built-in WATERMARK 200SS model uses
its 24 °C reference and marks the resulting reading as estimated. Review the
reading quality before using it to guide irrigation. New Irrigation inputs
accept estimated measurements by default; review that choice for the site and
preserve an existing explicit opt-out.

No separate mandatory calibration step is required to begin setup. Where the
installed sensor model offers calibration or correction, use measured values
and the site acceptance limits. Do not invent correction values or treat a
model's range as proof of field accuracy.

## 3. Register all Agri sources in Core

The Watermark setup creates three derived soil-tension streams in addition to
the native resistance streams. In **Core → Channels**, register every source
and the valve endpoint using the Agri checklist in [Register and Commission a
Terminal](commission-a-terminal.md). Do this before choosing station inputs;
the seven inputs in the simple setup are the three derived tensions, one
temperature role, and three diagnostics.

## 4. Create or resume a monitoring station

1. Open **Irrigation setup**.
2. Under **Set up an Agri station**, choose the Agri terminal and enter a station
   name.
3. For **Temperature sensor measures**, choose **Air temperature** or **Soil
   temperature** to match where the DS18B20 is physically installed.
4. Choose the installed valve wiring, normally open or normally closed, from the
   approved installation record.
5. Review the seven listed Agri inputs and each suggested Core measurement.
   Resolve any missing or ambiguous source in Devices/Core before continuing.
6. Select **Save reviewed station**. Confirm the success message and open the
   station.

New stations start in monitoring mode. Farm and field information can be added
later through **Advanced farm setup**. Do not guess probe depths, crop values,
soil settings, or irrigation thresholds; obtain these from the site plan.

If a station already exists for this terminal, choose **Review and resume
station** before changing setup. Compare its saved inputs, temperature role,
and valve wiring with the installation. Preserve an existing measurement policy
unless an authorized operator intentionally changes it.

After saving, **Measurement inputs** and **Station settings** show compact
summaries. Use **Edit inputs** to change measurement assignments, or **Edit name and
location**, **Edit valve setting**, and **Change zone** for station details.
Successful saves return to the summary; **Cancel** leaves saved settings intact.
You do not need to repeat setup on each visit.

## 5. Review readings and control state

Open the station and check that the three soil-tension readings, temperature,
diagnostics, and timestamps are current. Confirm whether the temperature is
reported as air or soil according to its physical placement. A valid software
reading is not independent sensor calibration or a field placement check.

Agri's minimum reporting interval is 15 seconds. A saved or queued interval is
not proof the terminal has applied it; confirm fresh reports and their
timestamps against the requested supported interval. Do not use a shorter
requested interval as an acceptance target.

Before any valve operation, confirm the site's authorization, compatible
latching valve, water supply, and independent means of checking valve and flow
state. A valve command or reported state alone does not prove that water is
flowing. For operating instructions, see [Operate Irrigation](operate-irrigation.md).

For installation limits and acceptance evidence still required, see
[Self-install Readiness](../reference/self-install-gaps.md) and the
[Installation Record](../reference/installation-record.md).

Last reviewed: 2026-09-27.
