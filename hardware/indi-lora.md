# Indi LoRa

Indi LoRa connects line-powered industrial equipment to your on-site Modulink
Basestation through LoRaWAN. Use it for distributed equipment and low data rate
monitoring or control.

## Main features

- Two independently wired passive 0–20 mA current inputs; 4–20 mA sensor
  scaling is configured separately when needed.
- Two ground-referenced 0–10 V inputs.
- One output that operates as 4–20 mA or 0–10 V.
- One relay-driver interface for an approved external relay.
- Nominal 24 VDC line power.
- LoRaWAN US915 connection.

## Important limits

The analog output has one mode at a time. Current software offers **4–20 mA**
or **0–10 V** in **Terminal settings & outputs**; select the mode approved for
the connected equipment. It is not both at the same time. Input acquisition is
separate: the two current inputs measure 0–20 mA. A transmitter can use a
4–20 mA engineering span, which is configured in its sensor model if scaling is
needed.

The relay driver is not a dry contact. Use the approved external relay when you
need common, normally open, and normally closed contacts. Do not use Indi LoRa
to power a motor, valve, solenoid, or other load directly.

## Next step

Follow [Connect Indi LoRa or Agri](../workflows/connect-lora-terminal.md).

Last reviewed: 2026-09-27.
