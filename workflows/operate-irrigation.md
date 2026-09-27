# Operate Irrigation

Use this workflow after completing [Agri Irrigation setup](set-up-agri-irrigation.md)
and confirming the site's valve procedure.

## 1. Check the station

Open **Irrigation** and select the station. Review the latest soil-tension
readings, the temperature role, battery and terminal diagnostics, alerts, and
reported valve state. Check timestamps and quality before relying on a reading.
Inspect the field when readings are unexpected or a sensor fault is shown.

## 2. Open the valve

Use **Manual override** only when an operator is authorized and the approved
field procedure is ready. Enter an approved value in **Open for (minutes)** when
using a finite run, then select **Open valve**. Do not infer water flow from the
command or the valve state alone.

## 3. Confirm and close

Wait for a fresh reported valve state and verify the physical result when the
operation requires it. Select **Close valve** when closure is needed, then wait
for fresh closed-state feedback. A browser closing is not a closure procedure.
The Basestation must remain powered and the radio link must deliver the command;
use the site's independent closure procedure if communication fails.

## 4. Review the record

Review station history and alerts after the operation. Record any unexpected
valve state, missing report, or safety condition before starting another run.

Last reviewed: 2026-09-27.
