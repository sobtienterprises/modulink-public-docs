# Configure Instruments and Outputs

Use Instrument Manager to set up installed instruments and supported outputs.

## 1. Select the terminal

Open Instrument Manager. Select the terminal that you installed. Confirm its
product, identity, and hardware profile before you change settings.

## 2. Initialize the configuration

If the terminal has no Core configuration, an administrator selects **Initialize
Core setup**. This creates a configuration draft. It does not send a command to
the terminal.

## 3. Set instrument details

Set the signal type, engineering unit, and supported range for each connected
instrument. Use the instrument manufacturer's data sheet. Do not estimate values
from wire color or a terminal channel name.

## 4. Review and send the configuration

Review the pending configuration. Save it only when the product, instrument, and
output settings are correct. The Basestation records pending and applied
configuration separately.

## 5. Confirm application

Wait for the terminal to report after the configuration is sent. Confirm that
the applied configuration is current and that readings are plausible. A queued
or sent command is not proof of a physical equipment change.

## 6. Test an output safely

Make connected equipment safe before you send an output command. Confirm the
result with an independent field check. Keep required safety interlocks outside
Modulink.

Last reviewed: 2026-09-25.
