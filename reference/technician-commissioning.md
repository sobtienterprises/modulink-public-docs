# Technician Commissioning Reference

Use these procedures only when the installed release and commissioning plan
require them. Ordinary operators should complete the linked browser procedures.

## Legacy Falcon asset groups

Rev E of the manual uses a site asset group of type `skid` to route terminal
telemetry to Falcon. Group membership and measurement assignments serve different
purposes. Complete both when required by the installed application.

Before changing groups, confirm that every terminal is registered or has reported
at least once. Have an Operator or Admin account. Inspect existing groups first.
Current software supports shared membership and dispatches an uplink once per
skill. The chapter draft's warning about duplicate dispatch was corrected in Rev E.

### Browser procedure

1. Open **Asset Groups** at `/asset-groups`.
2. Select **Create Group**.
3. Enter **Group name**, select group type `skid`, and add optional **Customer ID**.
4. Select **Create** and open the new group card.
5. Open **Members** and select **Add Device**.
6. Select the terminal by its label identity. Keep role `sensor` for the documented setup.
7. Select **Add Device** and repeat for each site terminal.
8. Check the member list and recent **Last Seen** times.

One group per site is the usual manual setup. Add a terminal to another group
only when it serves that group too. For a terminal added by mistake, review the
effect before removing its membership; that group will stop receiving its telemetry.

The commands below are an alternative for technicians who script site setup.

### Authenticate

Use the site's trusted TLS certificate. The examples use `--cacert` with a
certificate file verified by the site administrator. If the certificate is
already trusted by the operating system, omit that option.

Prepare a private `login.json` file with the supplied username and password.
Do not commit that file or paste credentials into a shared terminal log.

```json
{"username":"<SITE-USERNAME>","password":"<SITE-PASSWORD>"}
```

```sh
curl --fail-with-body --cacert /path/to/site-ca.pem \
  https://modulink.local/api/v1/auth/login \
  -H 'Content-Type: application/json' --data-binary @login.json
```

Keep the returned `access_token` private. Use it in place of `<TOKEN>` below.
Examples are templates; replace the complete placeholders before use.

### Inspect and create the site group

```sh
curl --fail-with-body --cacert /path/to/site-ca.pem \
  'https://modulink.local/api/v1/asset-groups?group_type=skid' \
  -H 'Authorization: Bearer <TOKEN>'
```

Inspect existing groups and members. Reuse the correct site group. If none exists,
create one with a descriptive site name:

```sh
curl --fail-with-body --cacert /path/to/site-ca.pem \
  https://modulink.local/api/v1/asset-groups \
  -H 'Authorization: Bearer <TOKEN>' -H 'Content-Type: application/json' \
  --data '{"group_name":"Site cleaning skids","group_type":"skid"}'
```

Record the returned `group_id`. For each intended terminal, add its exact identity:

```sh
curl --fail-with-body --cacert /path/to/site-ca.pem \
  'https://modulink.local/api/v1/asset-groups/<GROUP-ID>/members' \
  -H 'Authorization: Bearer <TOKEN>' -H 'Content-Type: application/json' \
  --data '{"dev_eui":"<TERMINAL-ID>","role":"sensor"}'
```

If adding a member reports that the device does not exist, return to provisioning.
Do not invent a second identity. After adding members, check fresh terminal data
and the Falcon dashboard. Keep the group membership record with the site handover.

## Create the legacy industrial hardware profile

Rev E replaces the older chapter's SQL insertion with the **Hardware Profiles**
page. Use this recipe only for the manual's Indi LoRa (Legacy) industrial hardware
and approved firmware. Current Indi LoRa and Agri require their own profiles.

1. Open **Hardware Profiles** at `/hardware-profiles` and inspect existing IDs.
2. Select **Create Profile**.
3. Set **Profile ID** to the approved unused industrial ID. The manual uses **4**;
   confirm that it is free and correct for this installation. Do not use **1**,
   which selects the legacy soil-sensor mode.
4. Set **Profile Name** to **Indi LoRa (Legacy) Industrial** and describe its two
   current inputs. Existing installations may retain the older profile label.
5. Set **Sample Period (seconds)** to **60** for the manual's configuration.
6. Enable **4-20mA CH0** and **4-20mA CH1**. Leave **VoltADC0–3** disabled.
7. Use **Instantaneous** sample mode and **1x** oversampling on both inputs.
8. For the manual's approved valve installation only, enable **H-Bridge**, label it
   **Valve**, and select **Valve (Hunter PGV)**. The manual sets **Max On Time (ms)**
   to **1000**, but documents a fixed **600 ms** firmware pulse limit. Confirm load
   compatibility independently; the stored value does not establish actual timing.
9. Leave **PWM0–3** disabled with zero duty limits.
10. Review all settings and select **Create Profile**.
11. Reload **Provisioning**, select the profile for the matching terminal, and
    verify its report and configuration feedback.

For that configuration, expect current inputs 0 and 1 and the enabled valve state
channel. The valve state is not a sensor reading. Labels such as **Pressure Sensor**
or **Flowmeter** are captions; configure measurement scaling separately.

### Export and import profiles

Use **Export** on **Hardware Profiles** to download the profile JSON. Before using
**Import** on another station, compare every ID and name with that station's profiles.
The manual specifies that matching IDs are overwritten and conflicting names on
different IDs are refused. Importing all profiles can affect terminals already
using those IDs. Retain an export of the destination and review the affected
devices before importing. Verify the result and device feedback afterward.

### Older SQL procedure

The earlier chapter draft inserts a fixed database profile ID for industrial
legacy units. It assumes three existing factory profiles and uses the database
ID as a firmware mode selector. Those assumptions are specific to that release.

Do not run that insertion against a current station without a reviewed migration.
An existing ID can mean a different profile. Supply support with the terminal
identity, product, firmware, current profile list, and software version. Request
the approved industrial profile and its application procedure.

The older industrial configuration enables the two current inputs and disables
unused voltage inputs. The manual also describes valve settings whose requested
pulse duration was not honored by that firmware. Do not infer an output's physical
timing from a stored configuration field.

After the approved profile is installed, reload **Provisioning**, select it for
the matching terminal, and verify configuration feedback and expected input channels.
No database edits are needed for normal operator commissioning.

## Backup and recovery handover

Have the installer provide a tested backup and recovery procedure for the delivered
release. Retain application data, the radio-network database, site configuration,
licenses, and certificate/key material in private storage.

The current source has a technician application-database backup playbook. It does
not by itself back up the complete station, install an automatic backup schedule,
or prove a successful restore. A compressed archive passing an integrity check
does not prove that a replacement Basestation can restore the site.

Before handover, record who runs backups, where an off-station copy is kept, the
schedule, retention, and the date of a successful isolated restore. Do not restore
onto an operating station as a routine documentation check.
