# Agent Tamagotchi — initial requirements

Status: early design requirements, before part selection.

The goal is a dedicated physical interface for supervising and talking to agents. It is not yet a commitment to any particular processor, display technology, development-board family, or operating system.

## Form factor

- Toy-sized, not dongle-sized.
- Roughly phone to small-tablet scale is acceptable.
- It may be somewhat larger than the Lapis One.
- It should be comfortable to leave on a desk and glance at, but still easy to pick up and carry.
- Thinness is not a primary objective if extra thickness improves keys, battery, acoustics, durability, or repairability.
- It should work as something kept nearby and picked up briefly to inspect jobs, continue work, stop something, or confirm that merges and other actions completed.

## Handling and enclosure

The device should tolerate casual, imperfect handling better than an ordinary glass-front tablet.

Desired handling characteristics:

- usable with wet or dirty hands for the important controls;
- grippy rather than slippery;
- some rubber or rubber-like exterior surfaces, bumpers, overmolding, or equivalent treatment are desirable candidates;
- resistant to minor drops, desk impacts, and being tossed into a bag;
- important buttons should remain easy to identify and press without precise fingertip placement;
- the enclosure should not depend on a pristine capacitive touchscreen for core operation;
- exact ingress-protection or drop-test targets are not yet specified.

The intent is closer to a small durable field controller or electronic toy than to a thin premium phone.

## Primary interface: physical keys

Physical keys are the primary interface for frequent control actions. A touchscreen is not required for those controls and should not be used as a substitute for them.

The device does **not** need a full physical QWERTY keyboard. An Android-Go-like on-screen keyboard is acceptable for arbitrary text entry. The physical keyboard area should instead be optimized for commands that are used repeatedly while supervising agents or using a terminal.

Desired key feel:

- real moving keys with clearly perceptible travel;
- soft press / soft bottom-out rather than a harsh click;
- enough travel that the press is physically obvious;
- comfortable for repeated use over long sessions;
- large enough and well-spaced enough to use by feel;
- usable when fingers are wet or dirty;
- tolerant of imprecise presses rather than demanding touchscreen-like accuracy;
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
- blocker / explain what needs attention;
- terminal;
- select all visible / active text;
- copy;
- paste.

The exact layout is intentionally open. The design should distinguish high-frequency controls by shape, position, or feel rather than requiring visual hunting.

## Terminal and text manipulation

Terminal access is a first-class use case, not a hidden developer feature. A Termux-like terminal or equivalent shell view should be directly accessible from the device interface.

The physical controls should make common terminal and text operations cheap even when arbitrary typing uses the on-screen keyboard. In particular:

- direct terminal key or equally immediate terminal access;
- page and half-page movement through terminal/chat output;
- select all text in the active text region or screen where that operation is meaningful;
- copy selected text;
- paste clipboard contents;
- preserve ordinary software selection when finer-grained selection is needed;
- do not require a touchscreen gesture for the common clipboard operations.

The exact semantics of “select all text on the screen” need to be defined per view. In a terminal it may mean the visible scrollback region or active selection domain; in chat it may mean the currently displayed response or editable input. The interface should avoid destructive ambiguity.

## Display

Desired behavior:

- always or nearly always readable at a glance;
- low idle power;
- suitable for text, job state, short responses, menus, task lists, and terminal output;
- readable in ordinary room light;
- does not need to behave like a full-color tablet display;
- should preserve useful state when the user walks away if the display technology permits that cheaply;
- should refresh quickly enough that terminal scrolling and text selection remain usable.

A monochrome, old-school electronic-toy / Tamagotchi-like visual character is acceptable and potentially desirable.

Do not choose display technology yet.

Candidates to compare later:

- memory LCD;
- conventional monochrome LCD;
- low-power TFT;
- fast-refresh e-paper / electrophoretic displays.

E-paper is not assumed to be correct merely because static state persists. Refresh speed, partial-refresh quality, ghosting, cost, power, and practical scrolling behavior need to be compared against other displays. Terminal use makes refresh behavior a stronger requirement than it would be for a status-only device.

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

The device does not automatically need to host the large language model or the full agent runtime locally. Its essential job is the human-facing control surface: display state, accept physical commands and dictation, provide terminal/text interaction, and communicate with agent services.

Any processor choice must therefore be justified by concrete requirements such as display handling, terminal rendering, audio capture, networking, encryption, local speech recognition, or offline behavior—not by the fact that Lapis One uses a relatively powerful SoC.

## Economic constraint

A dedicated Agent Tamagotchi should come in significantly below the cost of a full-featured low-cost Android tablet unless it provides a clear capability advantage that justifies the difference.

This constraint should drive part selection only after the interface requirements are stable.

## Design order

1. Establish interaction model and physical controls.
2. Establish display behavior and minimum useful text area, including terminal use.
3. Establish voice/audio requirements.
4. Establish networking and power requirements.
5. Only then shortlist components and prototype platforms.
