# Network and Access Reference

## Addresses used during installation

| Address | Purpose | Where the client must be |
| --- | --- | --- |
| `https://modulink.local` | Operator interface | Basestation's site network |
| `https://<BASESTATION-IP>` | Direct-address fallback | Network with a route to the Basestation |
| `http://192.168.4.1` | Indi Wi-Fi setup portal | Connected to that terminal's setup Wi-Fi |
| `http://modulink.local:8080` | ChirpStack technician console | Trusted site network |

The setup portal address is not the Basestation address. Reconnect the phone to
the site network after configuring the terminal.

## Site network preparation

1. Record the site network owner and the approved Wi-Fi network.
2. Confirm coverage at each Indi Wi-Fi installation point.
3. Confirm that client isolation does not block terminals from the Basestation.
4. Reserve the Basestation address in DHCP and record it.
5. Verify access from an operator workstation on the intended network segment.
6. Agree on remote access separately; the local hostname is not a public remote-access address.

## Ports described in the installation manual

| Port | Protocol/service | Intended use |
| --- | --- | --- |
| 443 | HTTPS | Operator interface and API |
| 80 | HTTP | Redirect to HTTPS |
| 8080 | HTTP, ChirpStack | Technician network management |
| 1883 | MQTT | Terminal telemetry to the Basestation |

This is the manual's service list, not a complete firewall policy for every
release. DNS, DHCP, time synchronization, discovery, updates, and optional remote
access need a release-specific network plan. Do not expose the management or
telemetry ports to the internet as a setup shortcut.

## Credentials in the handover

Keep the administrator account, user accounts, ChirpStack account, Wi-Fi setup
credentials, LoRa join credentials, and ERP key in the approved private store.
They serve different purposes. An operator token cannot replace a radio key.

The July manual printed shared defaults. Public documentation intentionally uses
placeholders. Each installation still needs a complete private credential handover
and recovery contact before an operator can install it alone.

## Time

The manual describes the Basestation as the site time source. Confirm its date,
time zone, and network time status before accepting data. Compare a fresh report's
time with the workstation. Record unexplained offsets or unknown timing quality.
Do not assume that being online proves a synchronized clock.
