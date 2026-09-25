# Self-install Readiness: Remaining Gaps

Reviewed 2026-09-25. The detailed industrial manual has been migrated and updated
against the current application source. This does **not** yet establish that an
operator can install every product without assistance.

The checklist below identifies what is still needed to make that claim. Suggested
owners are functions, not assigned people. An item is complete only when its
deliverable is supplied and its acceptance check passes.

## Blocking product and installation information

- [ ] **G1 — Release and profile mapping.** Product/software owner: publish the
  shipping Basestation release, supported firmware, and exact profile for each
  product. Include the labels still shown in the UI. Check: a new installer can
  select the correct product and profile without an engineer interpreting a code.
  Current source still contains engineering labels; the manual predates the Core
  measurement workflow.
- [ ] **G2 — Current Indi LoRa installation drawing.** Hardware owner: supply
  connector and pin numbers, polarity, conductor size, strip length, torque,
  supply/fuse requirements, grounding, AUX limits, and complete current/voltage/
  relay wiring examples. Check: each connection is traceable from the unit label
  to the drawing and verified on delivered hardware. The legacy four-wire harness
  is not a replacement for this drawing.
- [ ] **G3 — Agri field installation chapter.** Hardware/agronomy owner: document
  battery type/orientation, probe and temperature connector maps, Watermark
  preparation, placement/depth, cable routing, latching-solenoid compatibility
  and polarity, sealing, and replacement intervals. Check: install one complete
  station from unopened parts and obtain valid readings at all three depths.
  The cut sheet lists features but is not that procedure.
- [ ] **G4 — Mounting and environmental instructions.** Hardware owner: provide
  mounting dimensions, approved orientation/fasteners, antenna placement,
  clearance, gland/seal instructions, and environmental limits for each product.
  Check: the finished installation maintains the delivered enclosure protection.
  Product photographs and enclosure ratings do not define mounting technique.
- [ ] **G5 — Private installation handover.** Provisioning owner: deliver per-site
  accounts, setup-network credentials, join credentials, certificate identity,
  profile mapping, and recovery access through a private channel. Check: a new
  installer can sign in, join each unit, and recover access without shared defaults.

## Blocking workflow and acceptance evidence

- [ ] **G6 — Current Indi LoRa and Agri radio registration.** Firmware/platform
  owner: confirm the correct application, LoRaWAN version, class, region/sub-band,
  key handling, and operator registration path for each shipping product.
  Check: factory-new units join and deliver a first report using only that procedure.
  The documented legacy Class C profile must not be assumed for Agri.
- [ ] **G7 — Agri application setup.** Irrigation owner: publish steps to create
  the operation/field/block/station, assign probes and valve, enter depths and
  soil/crop settings, choose thresholds, and verify the water workflow. Check:
  a new site reaches a useful irrigation view from an empty database. The current
  page describes operation after setup; the industrial manual does not supply this chapter.
- [ ] **G8 — Sensor calibration and acceptance limits.** Hardware/metrology owner:
  identify board calibration supplied with current Indi Wi-Fi and the approved
  Core mapping/calibration path for each product. Supply numeric tolerances and
  invalid-input criteria. Check: known endpoint and intermediate signals meet
  those limits. Legacy 496/2482 counts do not establish every current input's accuracy.
- [ ] **G9 — Output commissioning and failure behavior.** Hardware/application
  owner: provide approved loads, current/duty limits, test duration, stop/isolation
  method, and expected behavior after radio loss, power loss, and restart.
  Check: physical relay, analog, H-bridge, and latching-valve tests pass on the
  shipping units. Queued commands and firmware state are insufficient evidence.
- [ ] **G10 — Fresh-install rehearsal on shipping software.** Documentation/QA:
  have a person unfamiliar with Modulink follow these pages on an empty site.
  Record every intervention and capture final UI screenshots with secrets removed.
  Include Indi Wi-Fi, current and legacy Indi LoRa, Agri, Falcon, and Irrigation
  where supported. Check: all applicable steps in the installation record pass.
  Current source review is complete; current live-station verification remains
  unavailable because `modulink.local` has not resolved from this workstation.

## Handover and support gaps

- [ ] **G11 — Complete network requirements.** Platform/network owner: publish
  protocols and directions for discovery, time, telemetry, management, updates,
  and optional remote access; state support for hidden SSIDs, enterprise Wi-Fi,
  isolated networks, and offline operation. Check: installation works with the
  stated firewall policy. The manual's four-port table is not a complete policy.
- [ ] **G12 — Backup, restore, update, and replacement procedure.** Platform owner:
  supply a scheduled, off-station backup and a tested full-station recovery plan,
  including the radio database, configuration, licenses, and keys. Document safe
  shutdown/update and terminal replacement. Check: restore onto a spare station
  and verify identities, history, and safe control state. The current application
  database backup alone does not cover the complete station.
- [ ] **G13 — Support and recovery route.** Operations owner: publish the actual
  contact address/number, support hours, required diagnostic bundle, and escalation
  method. Include unreachable Indi Wi-Fi recovery and lost-admin access. Check:
  the operator can raise an actionable request without knowing an engineer personally.
- [ ] **G14 — Illustrated installation pack.** Documentation/hardware owner:
  provide annotated photographs of supplied units, connectors, label locations,
  finished wiring, and UI screens for the named release. Check: each image matches
  shipped hardware and each manual photo placeholder has an actual counterpart.

## Information the site must supply

These are installation-specific, not values that a generic manual should invent:
network credentials and reservation, physical I/O map, sensor output endpoints,
approved alarm thresholds, reading-age limits, process accuracy tolerance, safe
equipment state, operating procedure, and named backup/support owners.

Use the [Installation Record](installation-record.md) to collect them and record
the commissioning result. This checklist can be closed in stages by product;
passing a Falcon industrial installation does not close the Agri installation items.
