# Connect Indi Wi-Fi

Complete Basestation setup first. This procedure uses the supplied terminal's
Wi-Fi setup portal. Record the terminal name and 12-character MAC address from
its label. The terminal name identifies its setup network; the MAC identifies
its record in Modulink.

## 1. Prepare power and credentials

Have a phone or laptop, the site Wi-Fi name and password, and the terminal's
setup-network credentials from the installation handover. Confirm coverage at
the intended mounting point.

Connect the supply specified on the unit. The July manual's industrial harness
uses 24 VDC, red positive and black return. Apply that wiring only to the matching
harness; see [Field Wiring](../reference/safety-and-wiring.md).

## 2. Join the terminal's setup network

1. Apply power and wait for the terminal to start.
2. Open Wi-Fi settings on the phone or laptop.
3. Select the network whose name matches the terminal in front of you.
4. Enter the setup-network password supplied for that unit.
5. Stay connected if the phone reports that this network has no internet access.

A new terminal opens its setup network. A terminal with saved settings first
tries its saved network. Allow 60 seconds without a connection before expecting
setup mode. If it already reaches the saved network, setup mode may not appear.
Check **Devices** and **Provisioning** before attempting a reset.

## 3. Open the setup page

The **Modulink Wi-Fi Setup** page usually opens automatically. If it does not,
open `http://192.168.4.1` while connected to the terminal's setup network.
Confirm the terminal name at the top of the page.

## 4. Save the site network

1. Select the site network from the list.
2. Enter its Wi-Fi password. The manual's portal accepts 8–63 characters.
3. Select **Connect device to this network**.
4. Wait while the terminal stores the settings and attempts the connection.

For a hidden network, expand **Advanced (hidden SSID / static IP)** and enter its
name. Use static address, prefix, gateway, and DNS fields only with values supplied
by the network owner. Only one person should configure a terminal at a time.

The setup network can close during the connection attempt. Its disappearance
alone does not confirm communication with the Basestation.

## 5. Check the result

1. Reconnect the phone or laptop to the site network.
2. Open the Basestation and check **Provisioning** for the terminal's MAC address.
3. Complete [Register and Commission a Terminal](commission-a-terminal.md).
4. Open **Devices**, select the terminal, and check **Live Data** for fresh reports.

If the setup network returns, rejoin it and read **Last failure**:

| Result | Check | Next action |
| --- | --- | --- |
| `rejected` | Password spelling, case, and extra spaces | Enter the correct password and submit again. |
| `absent` | Router power, range, supported band, and hidden network name | Select **Rescan**, or enter the hidden network name. |
| `dhcp_fail` | The router did not give the terminal an address | Ask the network owner to check DHCP capacity and policy. |

**Retry stored network now** retries without a new password entry. The portal
shows connection progress. The manual documents automatic retries every 30 seconds
for general failures and every five minutes after password rejection. Wait for
the result before submitting again; the portal limits repeated submissions.

## 6. Repeat for the remaining terminals

You can register all MAC addresses in advance, then set up Wi-Fi one terminal at
a time. For each unit, record the site, physical location, assigned profile, and
time of its first report. Match the setup network to the label each time.

## Previously connected terminal

If the terminal connects to an old network, use its existing reachable address
and have a technician follow the [network reset procedure](../reference/support-and-troubleshooting.md).
The manual documents no operator reset button for that hardware. An unreachable
terminal requires a recovery path from support.

## Acceptance check

- [ ] Correct terminal label and setup network matched.
- [ ] Site Wi-Fi connection completed.
- [ ] Terminal registered with its own MAC and correct profile.
- [ ] Site name and physical location saved.
- [ ] Fresh readings visible in **Devices → Live Data**.

Next: [Set Up Sensors](configure-sensors.md).
