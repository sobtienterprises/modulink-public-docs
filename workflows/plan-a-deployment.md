# Plan a Deployment

Plan the system before you order equipment or start field work.

## Installation supplies

- The Basestation, its supplied power unit, and an Ethernet cable.
- Each terminal, its approved power source, and its matching harness or connector drawing.
- The installed sensor's data sheet and any configured analog output endpoints.
- A small flat-blade screwdriver, wire stripper, DC voltmeter, and approved wire connectors.
- A phone or laptop with Wi-Fi for Indi Wi-Fi setup.
- A monitor, keyboard, and mouse if the Basestation needs desktop Wi-Fi setup.
- A loop calibrator when precision verification is required by the commissioning plan.
- Site network information, product/profile mapping, and a private credential handover.

The manual's 24 VDC industrial terminals do not include a supply. Confirm the
packing list for the actual order. Power ratings, mounting hardware, sealing
parts, antennas, and batteries must match the delivered product.

## 1. List each instrument

For each instrument, record the manufacturer, model, output signal, power need,
and installation location. Include a clear photo of its nameplate and terminals.

## 2. Choose the connection

Use Indi Wi-Fi for equipment inside reliable site Wi-Fi coverage. Use Indi LoRa
for line-powered, distributed industrial equipment that sends low data rates.
Use Agri for battery-powered soil monitoring and latching irrigation valves.

## 3. Check power and network access

Record the available DC supply at each terminal location. Record the site network
owner and any required access approval. Plan LoRa coverage before you install
LoRaWAN terminals.

## 4. Make an I/O map

Assign every instrument to a named terminal and channel. Record each control
interface, its safe state, and any independent safety interlock.

## 5. Review the plan

Review the I/O map, network plan, and safety requirements with Modulink before
installation. Do not use a terminal as a substitute for a required safety system.

Last reviewed: 2026-09-25.
