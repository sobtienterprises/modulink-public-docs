# Set Up a Basestation

Use this procedure for a supplied Modulink Basestation with its software already
installed. It does not install software on a blank Raspberry Pi.

## Before you start

Have the supplied power unit, Ethernet cable, site network details, and installation
handover available. The handover must contain the Basestation identity, initial
administrator account, certificate information, and installed software version.
For initial Wi-Fi setup, have a compatible monitor, keyboard, and mouse.

Keep the Basestation in a dry, protected location with stable power. Confirm the
power rating on its label. The terminal's DC supply is not the Basestation supply.

## 1. Connect to the site network

Ethernet is preferred where available.

1. Connect the Ethernet cable from the site router or switch to the Basestation.
2. Connect the supplied power unit.
3. Wait for the Basestation to start.
4. Find its address in the router's connected-device list. Match the device identity
   to the installation record.

For Wi-Fi on the Raspberry Pi OS desktop:

1. Connect the monitor, keyboard, and mouse before starting the Basestation.
2. Wait for the desktop. Select the network icon in the taskbar.
3. Select the site Wi-Fi network. Enter its password and connect.
4. Confirm that the desktop shows a network connection.

Use the same local network as the Indi Wi-Fi terminals. Guest Wi-Fi or client
isolation can prevent devices from communicating even when each has internet access.
Give the network owner the [network requirements](../reference/network-and-access.md).

## 2. Record a stable address

Ask the network owner to reserve the Basestation address in DHCP, using its network
adapter MAC address. Record both the hostname and reserved IP address in the
[installation record](../reference/installation-record.md). Do not select an address
by guesswork.

## 3. Open the operator interface

1. Connect a phone or computer to the site network.
2. Open `https://modulink.local` in a browser.
3. If the name does not resolve, use `https://<BASESTATION-IP>` with the address
   obtained from the router. Replace the entire placeholder, including brackets.
4. Confirm that the Modulink sign-in page opens.

Some supplied systems use a self-signed certificate. Before accepting it, check
the address and certificate identity against the handover with the site administrator.
A certificate warning alone does not prove that the device is your Basestation.
If the identity does not match, stop and ask the administrator to check it.

If neither address works, check power, network cables, Wi-Fi association, and
network isolation. A direct IP address does not bypass a disconnected network.

## 4. Sign in and change the temporary password

1. Use the administrator account supplied for this installation.
2. Complete the password-change screen if it appears.
3. Otherwise, open **Settings → Change Password**. Enter the current password,
   the new password, and its confirmation. Select **Change Password**.
4. Store the new password in the site's approved password store.

Do not use a password printed in an old manual. If the supplied account fails,
have the site administrator reset it.

An administrator can reset another user's password through **Users**, the user's
edit control, **New Password**, and **Save Changes**.

## 5. Create individual accounts

1. Open **Users** and select **Create User**.
2. Enter the person's username and initial password. Add email if required.
3. Select the role from the table below.
4. Select **Create User**. Give the credentials to that person through the site's
   approved private channel.
5. Have the person sign in and confirm their access.

| Role | Use |
| --- | --- |
| Admin | Manage users and site configuration. Some initialization steps require this role. |
| Operator | Configure supported instruments and use operating controls. |
| Viewer | Read dashboards and records. |

Follow the validation shown in the current form. The July manual specified at
least three characters for usernames and eight for passwords; site policy can
require more. Do not disable a required password change to avoid its prompt.

## 6. Verify the installation

- [ ] The interface opens from a second device on the site network.
- [ ] The hostname or reserved address is recorded.
- [ ] The temporary administrator password is changed.
- [ ] Each user can sign in with the correct role.
- [ ] The Basestation date, time, and time zone are correct.
- [ ] **Dashboard**, **Devices**, and the purchased application, such as Falcon or
  Irrigation, are available.

An empty dashboard is normal before terminals and application instances are added.
A missing application requires installation or licensing support; adding sensors
will not make that application appear.

Next: [Connect Indi Wi-Fi](connect-indi-wifi.md) or
[Connect a LoRa terminal](connect-lora-terminal.md).
