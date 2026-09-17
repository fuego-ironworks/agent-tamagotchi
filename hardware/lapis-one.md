# Lapis One research profile

Reference device for Agent Tamagotchi hardware exploration.

Evidence status: **manufacturer-published specifications and public documentation unless otherwise marked**. This is not a physical-device receipt. Keep claims about the shipped product separate from estimates, interpretations, and Agent Tamagotchi design choices.

Primary sources:

- https://www.pamir.ai/
- https://docs.pamir.ai/

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

The RK3576 is a general-purpose ARM64 SoC, not merely a display controller. It gives Lapis enough computer to run Debian, persistent agent processes, shells, MCP servers, compilers, local services, peripheral I/O, KVM capture/control, and potentially smaller local inference workloads.

The current Lapis pitch should not be read as "the large language model runs entirely on this chip." Pamir documentation discusses third-party model providers and API credentials. The product is better understood as a local agent host that can call remote models while keeping tools, state, credentials, and peripheral control on the Lapis itself.

Pamir's earlier Distiller material documented local llama.cpp use with a quantized Qwen2.5 3B model, plus local speech recognition and speech synthesis. That establishes that local small-model use exists in the product lineage; it does not by itself establish the exact production Lapis One software image.

## Display and audio

- Display: Sharp monochrome memory LCD
- Resolution: 240 × 400 px
- Audio DSP: dedicated XMOS device
- Microphones: 2 × MEMS
- Speaker: 1 W mono

The display is attractive as a reference for an always-visible, low-power status surface. The audio path shows that voice interaction can be built directly into the device, but it does not establish that Agent Tamagotchi needs an expensive SoC for speech-to-text. Cheap Android phones already demonstrate that useful voice transcription can exist in a finished device far below Lapis pricing.

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

## USB and Agent KVM

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

The KVM is easier to understand as **video capture plus USB keyboard/mouse emulation**, not merely as a conventional desktop KVM switch.

Conceptually:

```text
controlled computer  -- screen/video -->  Lapis
controlled computer  <-- USB HID ------  Lapis
```

An agent running on Lapis can inspect screenshots, decide where to click or what to type, then emit ordinary HID events back to the controlled machine. The target computer need not run the agent runtime itself.

A concrete use case is a machine where software installation is unavailable or undesirable: a locked-down work computer, a Windows/macOS-only GUI application, firmware/installer screens, recovery environments, or other systems whose practical interface is a display plus keyboard and mouse. This does **not** establish that Pamir designed the product specifically to evade corporate security policies; it only establishes the technical capability and an obvious class of use cases.

For software-development tasks with APIs, shells, files, or GitHub access, direct machine interfaces are generally more precise than screenshot-driven KVM control. KVM is best treated as a bridge for otherwise closed/manual interfaces.

### USB 3 and USB 4 — data

- Power output: 5 V / 1 A
- USB 3.2 SuperSpeed
- Advertised 5 Gbit/s shared between the two ports

## GPIO

- 12-pin magnetic GPIO connection
- 5 V and 3.3 V rails
- Exposed Rockchip GPIOs
- Advertised alternate functions include PWM, I2C, UART, and SPI
- No ADC is listed in Pamir's published pinout

For Agent Tamagotchi, GPIO is directly relevant to dedicated controls such as submit, dictate, continue, task navigation, stop/cancel, and blocker inspection.

## Sensors and security hardware

- Fingerprint sensor
- IMU
- TPM 2.0 specified as part of the encrypted-system design
- LUKS2 encrypted data with TPM-backed key handling is described by Pamir

This hardware makes Lapis suitable for keeping local credentials and secrets more securely than ordinary plaintext files. API keys, SSH keys, and cryptocurrency wallet material are possible examples of secrets a user could choose to keep there. Do not describe Lapis as a dedicated cryptocurrency hardware wallet without separate evidence: the architecture and threat model are different from a purpose-built Ledger/Trezor-style device.

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
- Later preorder batches have been shown at higher prices, including $499.
- Treat price as a time-dependent offer rather than a fixed hardware characteristic.

## Cost research

### Bad first estimate to avoid

Do **not** price the RK3576 subsystem by substituting a complete $200+ development board for the raw compute electronics. That badly overstates product BOM because a development board already includes its own PCB, connectors, regulators, vendor margin, distribution margin, and unrelated interfaces.

### More realistic low-volume picture

A complete RK3576 single-board computer with 8 GB LPDDR5 can retail far below the price of a development kit, showing that the actual RK3576 + memory subsystem cannot sensibly be modeled as a $200+ component block.

A rough one-off/low-volume decomposition discussed during research was:

| subsystem | rough range |
| --- | ---: |
| RK3576 + 8 GB board-level compute electronics | $45–70 |
| 64 GB eMMC | $8–15 |
| Sharp memory LCD | $19–29 |
| audio DSP + two microphones + speaker | $15–25 |
| battery + charging/power | $10–20 |
| NFC + TPM + IMU + fingerprint | $12–25 |
| USB/KVM circuitry | $20–40 |
| connectors/passives/miscellaneous | $10–20 |
| PCB allocation | $8–20 |
| enclosure/mechanical parts | $15–30 |

This is an **engineering estimate**, not Pamir's BOM and not a quotation. It suggests something on the order of roughly $160–275 for low-volume finished hardware before assembly labor, certification, failures, tooling, software development, support, packaging, fulfillment, and margin. Higher production volume should reduce component cost.

The main conclusion is not that Lapis costs a particular amount to manufacture; it is that the earlier ~$430 electronics estimate was invalid because it used a retail development board as a component proxy.

## What the compute appears to be for

The high-end-for-a-chat-terminal hardware makes sense if Lapis is treated as **the agent's own computer**, rather than merely a screen for ChatGPT.

Likely workloads include:

1. Persistent Debian agent processes and shells.
2. Local tools, compilers, MCP servers, package managers, files, and services.
3. USB, storage, GPIO, networking, and other peripheral control.
4. Capturing another computer's display and emitting keyboard/mouse actions through Agent KVM.
5. Local speech recognition/synthesis and perhaps smaller local models.
6. Secure local storage of credentials and other agent state.
7. Remote calls to larger hosted models when needed.

That is a much broader role than Agent Tamagotchi's current human-facing supervision concept.

## Agent Tamagotchi contrast

Lapis should remain a **reference design**, not the default architecture.

Agent Tamagotchi's present design question is different: provide a dedicated human control surface for supervising long-running agent/chat work. The useful capabilities discussed so far include:

- persistent status display;
- hardware submit;
- hardware stop/cancel;
- hardware continue;
- previous/next task or conversation;
- page/half-page navigation;
- pull up projects/task list;
- blocker/problem inspection;
- voice dictation where economical;
- clear waiting/working/failed/finished state.

A cheap Android phone/tablet already proves that display, battery, microphone, networking, speech-to-text, and enough user-interface compute can exist in a roughly $70–100 finished device. Therefore a standalone Tamagotchi should come in **significantly below a full-featured cheap Android tablet** unless it offers a capability the tablet genuinely cannot.

The `tablet-keyboard` branch explores the complementary path: keep the cheap Android device and add a purpose-built physical command keyboard/control surface rather than replacing the whole computer.

## Not established for Agent Tamagotchi

This research does **not** establish that Agent Tamagotchi needs:

- RK3576 specifically;
- 8 GB RAM;
- a 6 TOPS NPU;
- four USB-C ports;
- Agent KVM hardware;
- TPM 2.0;
- fingerprint authentication;
- NFC;
- M.2 storage;
- an immutable OS;
- Nix;
- Pamir's enclosure dimensions;
- Pamir's display vendor or exact resolution.

Those remain optional reference points to test against the actual interaction requirements.
