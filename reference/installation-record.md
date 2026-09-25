# Installation Record and Acceptance Checklist

Copy this record for each site. Store credentials separately. Record an actual
result for each test; do not mark a test passed because configuration was saved.

## Site record

| Item | Record |
| --- | --- |
| Site, installer, installation date | |
| Site operator and support contact | |
| Basestation identity and supplied power unit | |
| Software release and enabled applications | |
| Hostname, reserved IP, network owner | |
| Certificate identity verified by | |
| Backup owner, schedule, private storage location | |
| Most recent successful restore test | |

## One row per terminal

| Product and label identity | Physical location | Firmware and hardware profile | Supply | Report interval | First fresh report |
| --- | --- | --- | --- | --- | --- |
| | | | | | |

## One row per instrument

| Terminal/input | Sensor model | Signal span | Engineering span and unit | Application role | Reference and tolerance | Measured result |
| --- | --- | --- | --- | --- | --- | --- |
| | | | | | | |

Record calibration endpoint counts separately where the legacy ADC path uses them.
For current sensor mappings, retain the installed model/calibration revision.

## Acceptance sequence

- [ ] Confirm the packing list, product identities, power ratings, and installation drawings.
- [ ] Mount and seal equipment according to supplied instructions.
- [ ] Verify field wiring, isolation, polarity, and supply voltage.
- [ ] Open the Basestation from the operator's normal workstation.
- [ ] Verify individual accounts, roles, and changed temporary credentials.
- [ ] Confirm time and hostname/direct-IP access.
- [ ] Verify every terminal's identity, profile, and at least two fresh reports.
- [ ] Verify every sensor at endpoints and an intermediate reference value where applicable.
- [ ] Confirm fault indication for an invalid input using the approved test method.
- [ ] Confirm application assignments against the physical instrument map.
- [ ] Confirm dashboard units, freshness rules, trends, and history.
- [ ] Test approved outputs with a person at the equipment; record physical results.
- [ ] Verify the physical safe state after testing.
- [ ] Run a sample recording workflow and confirm the saved record.
- [ ] Verify the agreed alert response with a controlled test that does not expose equipment to unsafe conditions.
- [ ] Record results of the approved power/network interruption and recovery test.
- [ ] Confirm backups and a successful isolated restore with the responsible technician.
- [ ] Give the operator drawings, credentials, recovery instructions, and support details.

## Handover decision

Record each failed or unperformed test, its impact, responsible person, and required
action. List restrictions on operation. The installer and site operator should
review the record together before accepting the system.

Use [Self-install Gaps](self-install-gaps.md) to distinguish missing product
instructions from site-specific information that the installer must supply.
