# Lapis One hardware profile

Reference device for Agent Tamagotchi hardware exploration.

Evidence status: **manufacturer-published specification, not independently verified here**. As of 2026-09-17, Pamir describes Lapis One as a preorder product, with the first shipping batch expected in October 2026. Treat this file as a reference profile, not a physical receipt.

Source: https://www.pamir.ai/

## Physical

- Dimensions: 85 × 85 × 28 mm
- Weight: 227 g
- White housing: painted aluminum
- Black housing: anodized aluminum
- Top shell: PC + ABS plastic
- Physical inputs: power button, rocker switch, fingerprint button

## Compute

- SoC: Rockchip RK3576
- CPU: 4 × Cortex-A72 + 4 × Cortex-A53
- NPU: integrated 6 TOPS accelerator
- Memory: 8 GB LPDDR5

## Display and audio

- Display: Sharp monochrome memory LCD
- Resolution: 240 × 400 px
- Audio DSP: dedicated XMOS device
- Microphones: 2 × MEMS
- Speaker: 1 W mono

The low-power monochrome display and dedicated microphone/speaker path are especially relevant to Agent Tamagotchi because the intended device is a persistent status-and-command surface rather than a general-purpose graphical workstation.

## Battery

- Battery: 3,300 mAh Li-ion
- Manufacturer-stated runtime: roughly 2–4 hours depending on workload
- Pamir describes the battery primarily as continuity/UPS power rather than all-day mobile-computer power.

## Storage

- Internal: 64 GB eMMC
- Expansion: M.2 Key M, 2230
- microSD: advertised support up to 2 TB

## Wireless

- Wi-Fi 6: 802.11a/b/g/n/ac/ax
- Bluetooth 5.4
- NFC

## USB and KVM

Four USB-C ports are advertised with distinct roles.

### USB 1 — OTG

- Power input: USB PD 9 V / 3 A or 5 V / 3 A
- Power output: 5 V / 1 A
- USB 3.2 SuperSpeed
- DisplayPort Alt Mode output up to 4K @ 30 Hz

### USB 2 — Agent KVM

- Power input: USB PD 9 V / 3 A or 5 V / 3 A
- Power output: 5 V / 1 A
- USB-C DisplayPort Alt Mode capture
- Advertised video input up to 2K @ 30 Hz
- HID keyboard and mouse emulation
- On-demand screen capture

### USB 3 and USB 4 — data

- Power output: 5 V / 1 A
- USB 3.2 SuperSpeed
- Advertised 5 Gbit/s shared between the two ports

For Agent Tamagotchi, the KVM path is worth keeping as a separate design question. The core project can be useful as a human-facing agent console without requiring KVM, but KVM could let the device supervise or operate another computer directly.

## GPIO

- 12-pin magnetic GPIO connection
- 5 V and 3.3 V rails
- Exposed Rockchip GPIOs
- Advertised alternate functions include PWM, I2C, UART, and SPI
- No ADC is listed in Pamir's published pinout

The GPIO concept is directly relevant for physical Agent Tamagotchi controls: dedicated submit, dictation, continue, task navigation, and blocker-inspection buttons should not depend on touchscreen UI.

## Sensors and security hardware

- Fingerprint sensor
- IMU
- TPM 2.0 is specified as part of the encrypted-system design

## Operating system profile

Pamir currently specifies:

- Debian 13 (Trixie)
- Linux 6.1.141
- systemd
- read-only root with dm-verity
- signed A/B system updates
- LUKS2 encrypted data, with TPM-backed key handling
- root access
- Nix package manager
- Python SDK for built-in hardware
- Tailscale included

This software stack is descriptive of Lapis One, not a requirement for Agent Tamagotchi.

## Price and availability snapshot

As of 2026-09-17:

- Pamir advertises Lapis One **from $359**.
- The storefront currently shows later preorder batches at higher prices, including a $499 batch.
- Price should therefore be recorded as a time-dependent offer, not a fixed hardware characteristic.

## Agent Tamagotchi takeaways

The useful reference characteristics are:

1. Small square self-contained Linux computer.
2. Always-visible low-power monochrome status display.
3. Physical controls rather than touchscreen-only interaction.
4. Built-in microphones and speaker for voice interaction.
5. Battery sufficient to preserve a running session while moving or unplugging the device.
6. Wi-Fi plus ordinary Linux networking.
7. GPIO for purpose-built controls.
8. Enough local compute and memory to run orchestration, terminal, speech, and interface software even when model inference happens elsewhere.
9. Optional KVM capability for controlling a second computer.
10. Expandable storage rather than dependence on soldered internal flash alone.

## Not yet established for Agent Tamagotchi

This profile does **not** establish that Agent Tamagotchi needs:

- an RK3576 specifically;
- 8 GB RAM;
- a 6 TOPS NPU;
- four USB-C ports;
- KVM hardware;
- TPM 2.0;
- fingerprint authentication;
- an immutable OS;
- Nix;
- Pamir's enclosure dimensions;
- Pamir's display vendor or exact resolution.

Those are candidate reference points to test against the actual interaction requirements.
