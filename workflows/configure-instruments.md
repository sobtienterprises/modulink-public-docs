# Configure Terminal Settings and Outputs

This procedure changes terminal reporting and supported output settings.
Use [Set Up Sensors](configure-sensors.md) for sensor models and calibration.

## 1. Open the terminal controls

1. Sign in as an Operator or Admin.
2. Open **Instrument Manager → Actuators**.
3. Select the terminal by its identity and profile.
4. Read **Terminal settings & outputs**. Confirm that it is the intended device.

If setup is missing, an administrator can use **Initialize Core setup** for
supported hardware. Confirm the actual product first. Initialization creates a
draft; it does not prove which configuration the hardware currently uses and
does not itself send an output command.

## 2. Set reporting and output modes

1. Set **Reporting interval (seconds)** to the value approved for this installation.
2. For current Indi LoRa, select **Enable relay** and **Enable analog output** only
   for installed, approved interfaces.
3. Select **Analog output mode**: **0–10 V** or **4–20 mA**. Match the receiving input.
4. Review the settings and select **Save settings**.
5. Wait for the result. The UI can report **Settings saved and queued for the terminal**.

Saving here queues a configuration for delivery. Pending configuration, last-sent
configuration, and hardware-reported state are different. A queued result is
not proof of application. If a request times out, select **Refresh** and inspect
the current state before trying again.

## 3. Test a supported output

Only test after the wiring, load rating, and safe test procedure are approved.
Tell the person at the equipment which output you intend to operate.

| Control shown | Action |
| --- | --- |
| Relay or binary H-bridge | Select **On** or **Off**. |
| Valve | Select **Open** or **Close**. |
| Analog output | Enter the setpoint in the displayed V or mA units, then **Set output**. |
| Analog disable | Select **Disable output**. A disabled output differs from its minimum setpoint. |
| Drive or PWM | Use the displayed duty range and **Set output**; **Stop** requests zero drive. |

1. Check that no unsaved settings remain.
2. Confirm the output name, displayed unit, and permitted range.
3. Send one command and follow its displayed command number and delivery status.
4. Wait for a fresh **Reported** state and timestamp.
5. Have the person at the equipment verify the physical result.
6. Return the equipment to its agreed safe state and record the result.

The command status and the reported output answer different questions:

| Command status | Meaning |
| --- | --- |
| Queued or accepted by the network | Delivery is progressing; terminal application is not yet confirmed. |
| Device reports applied | The terminal acknowledged application. Verify the fresh reported output and physical result separately. |
| Duplicate ignored | This receipt does not establish whether an earlier attempt applied the command. Application remains unconfirmed. |
| Busy or rejected | The terminal did not accept this attempt. Review the result before deciding whether to retry. |
| Delivery unconfirmed or status unavailable | The outcome is unknown. Inspect the reported state before sending another command. |

The page follows the command number returned by that submission. Reloading the
same browser session retains that reference; checking its status does not send
another output command. A late acknowledgment can still update an unconfirmed
result.

**Last reported**, **Unknown**, or **No state reported yet** does not establish
the current physical state. Wireless failure can prevent a stop command from
arriving. Use the site's independent isolation or stop procedure when required.

## If controls are unavailable

Check account role, completed initialization, saved settings, and the selected
product profile. Disabled outputs can be unavailable in the saved configuration.
If the UI reports that settings changed, refresh and review before sending a command.
Do not enable an unfamiliar output simply to make a button available.

For an R7 ordinary finite control run with reported intent and retry behavior,
see [Use the Industrial Demonstrator](use-benchtop.md). Its estimated-measurement
choice is separate from the Irrigation input defaults.
