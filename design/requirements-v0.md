# Agent Tamagotchi — initial requirements

Status: early design requirements, before part selection.

The goal is a dedicated physical interface for supervising and talking to agents. It is not yet a commitment to any particular processor, display technology, development-board family, or operating system.

## Form factor

- Toy-sized, not dongle-sized.
- Roughly phone to small-tablet scale is acceptable.
- It may be somewhat larger than the Lapis One.
- It should be comfortable to leave on a desk and glance at, but still easy to pick up and carry.
- Thinness is not a primary objective if extra thickness improves keys, battery, acoustics, or repairability.

## Primary interface: physical keys

Physical keys are the primary interface. A touchscreen is not required and should not be used as a substitute for important controls.

Desired key feel:

- real moving keys with clearly perceptible travel;
- soft press / soft bottom-out rather than a harsh click;
- enough travel that the press is physically obvious;
- comfortable for repeated use over long sessions;
- large enough and well-spaced enough to use by feel;
- durable enough for very frequent presses.

Do not choose a switch technology yet. Candidate mechanisms can later include silicone-rubber domes, scissor mechanisms, low-profile mechanical switches, or other key structures that meet the feel requirement.

Initial command set to support physically:

- send / submit;
- stop current job;
- continue;
- voice / dictation;
- previous / next task or conversation;
- page up / page down;
- half-page up / half-page down;
- projects / task list;
- back / cancel;
- blocker / explain what needs attention.

The exact layout is intentionally open. The design should distinguish high-frequency controls by shape, position, or feel rather than requiring visual hunting.

## Display

Desired behavior:

- always or nearly always readable at a glance;
- low idle power;
- suitable for text, job state, short responses, menus, and task lists;
- readable in ordinary room light;
- does not need to behave like a full-color tablet display;
- should preserve useful state when the user walks away if the display technology permits that cheaply.

A monochrome, old-school electronic-toy / Tamagotchi-like visual character is acceptable and potentially desirable.

Do not choose display technology yet.

Candidates to compare later:

- memory LCD;
- conventional monochrome LCD;
- low-power TFT;
- fast-refresh e-paper / electrophoretic displays.

E-paper is not assumed to be correct merely because static state persists. Refresh speed, partial-refresh quality, ghosting, cost, power, and practical scrolling behavior need to be compared against other displays.

## Voice input

- Built-in microphone is required for the main design direction.
- Speech-to-text should be supported by the overall system.
- The microphone path should be good enough for ordinary close-range dictation in the way inexpensive phones and tablets already are.
- Do not yet require speech recognition to execute locally on the Tamagotchi. Local, LAN, and cloud transcription should all remain possible architectures.

## Networking

- Wireless networking is required.
- The device needs an internal antenna suitable for ordinary indoor use.
- Wi-Fi is the baseline assumption because the device must communicate with agent services and/or local machines.
- Bluetooth may be useful but is not yet a hard requirement.
- Cellular networking is not currently required.

## Audio output

Open question.

A speaker may be useful for alerts or spoken responses, but is not yet established as required. A simple buzzer or haptic alert may be sufficient for the first version.

## Power

- Battery-powered operation is desirable.
- USB charging is expected.
- It should remain useful as a desk device while plugged in.
- Battery life should be judged against the always-visible-display use case rather than against a general-purpose tablet.

## Compute architecture

Not chosen.

The device does not automatically need to host the large language model or the full agent runtime locally. Its essential job is the human-facing control surface: display state, accept physical commands and dictation, and communicate with agent services.

Any processor choice must therefore be justified by concrete requirements such as display handling, audio capture, networking, encryption, local speech recognition, or offline behavior—not by the fact that Lapis One uses a relatively powerful SoC.

## Economic constraint

A dedicated Agent Tamagotchi should come in significantly below the cost of a full-featured low-cost Android tablet unless it provides a clear capability advantage that justifies the difference.

This constraint should drive part selection only after the interface requirements are stable.

## Design order

1. Establish interaction model and physical controls.
2. Establish display behavior and minimum useful text area.
3. Establish voice/audio requirements.
4. Establish networking and power requirements.
5. Only then shortlist components and prototype platforms.
