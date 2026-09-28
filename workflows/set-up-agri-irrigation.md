# Set Up Agri Irrigation

Use this workflow to prepare an Agri station for monitoring. It does not open a
valve or start automatic control.

## Steps

1. **Set up the Agri inputs.** Open **Devices**, select the Agri terminal, open
   **Sensor Settings**, and select **Set up sensor inputs**. The terminal
   provides three Watermark resistance inputs, one DS18B20 temperature input,
   and diagnostic streams such as battery, reservoir-rail, and coil-pulse
   current. If no Agri terminal is offered, check its visible profile,
   firmware, and latest report in **Devices**, then try again.

2. **Select the Watermark and temperature inputs.** Open **Devices**, select
   the Agri terminal, and open **Sensor Settings**. If the Watermark settings
   are already saved, select **Edit Watermark sensors**.
   Configure WM1, WM2, and WM3 as separate soil-tension sensors. When exactly
   one temperature stream from this terminal is available, the form selects
   it. Check that it is the DS18B20, or select that stream yourself. It
   compensates all three Watermarks. This setting does not change where the
   DS18B20 is physically installed. If there is no unique candidate, select
   the correct stream yourself or use the model reference when appropriate.

   ![The new Watermark setup form already has DS18B20 temperature selected for WM1 and WM2.](../assets/screenshots/agri-watermark-default-ds18b20.png)

   <a href="https://sobtienterprises.github.io/modulink-public-docs/assets/screenshots/agri-watermark-default-ds18b20.png" target="_blank" rel="noopener">Open full-size image</a>

   *The form selects the onboard DS18B20 when it is the only temperature input on that terminal. Check all three rows, then save. The next image shows the lower part of the form.*

   ![The lower part of Sensor Settings shows the DS18B20 selected for WM2 and WM3.](../assets/screenshots/agri-watermark-compensation-lower.png)

   <a href="https://sobtienterprises.github.io/modulink-public-docs/assets/screenshots/agri-watermark-compensation-lower.png" target="_blank" rel="noopener">Open full-size image</a>

3. **Save and check the sensor setup.** Select **Save Watermark sensors**.
   The form closes and the page shows a summary for WM1, WM2, and WM3, with
   their temperature compensation settings. Use **Edit Watermark sensors**
   only when you want to change those settings.

   ![Saved Watermark summary shows WM1, WM2, and WM3 configured with DS18B20 temperature compensation.](../assets/screenshots/agri-watermark-saved-summary.png)

   <a href="https://sobtienterprises.github.io/modulink-public-docs/assets/screenshots/agri-watermark-saved-summary.png" target="_blank" rel="noopener">Open full-size image</a>

4. **Review estimated readings and corrections.** Without a compensation
   input, the built-in WATERMARK 200SS model uses its 24 °C reference and marks
   the derived reading as estimated. New Irrigation inputs accept estimated
   readings by default. Review that choice for the site and preserve an
   existing explicit opt-out. No separate calibration is required to begin
   setup. Correction starts at zero. Keep zero correction unless measured
   values and the site's acceptance limits support a change. If the installed
   model offers calibration, use measured values and those limits.

5. **Register the Agri sources in Core.** Open **Core → Channels** and use the
   Agri checklist in [Register and Commission a Terminal](commission-a-terminal.md).
   Register every supported source, the three derived soil-tension streams,
   and the valve endpoint before choosing station inputs. The simple station
   setup uses seven measurement inputs: three derived tensions, one
   temperature role, and three diagnostics.

6. **Review and save the station.** Open **Irrigation setup**. Under **Set up
   an Agri station**, select the terminal and enter a station name. Set
   **Temperature sensor measures** to **Air temperature** or **Soil
   temperature** to match the DS18B20's physical location. Select the normally
   open or normally closed valve type from the approved installation record.
   Review the seven inputs and suggested Core measurements, then select **Save
   reviewed station**. The station list shows **Station inputs saved**. Select
   the station name to open it. If the
   terminal already has a station, select **Review and resume station** and
   check its saved settings before changing them.

7. **Check the saved settings.** A new station starts in monitoring mode.
   **Measurement inputs** and **Station settings** show summaries. Use **Edit
   inputs**, **Edit name and location**, **Edit valve setting**, or **Change
   zone** to make a change. **Cancel** leaves saved settings intact. Farm and
   field details can be added later in **Advanced farm setup**; get probe
   depths, crop values, soil settings, and irrigation thresholds from the site
   plan instead of guessing. You do not need to repeat setup on each visit.

8. **Check readings.** In the station, check the three soil-tension readings,
   temperature, diagnostics, timestamps, and reading quality. Confirm that the
   temperature role matches the DS18B20's physical location. Agri's minimum
   reporting interval is 15 seconds; confirm fresh reports and timestamps
   before relying on a requested interval.

For valve operation, follow the site's approved procedure and use a compatible
latching valve. A command or reported valve state alone does not prove that
water is flowing. See [Operate Irrigation](operate-irrigation.md).

For installation limits, see
[Self-install Readiness](../reference/self-install-gaps.md) and the
[Installation Record](../reference/installation-record.md).

Last reviewed: 2026-09-28.
