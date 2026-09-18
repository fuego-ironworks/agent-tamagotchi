# Agent Tamagotchi — prototype parts survey — 2026-09-18

Status: prototype candidates only. This is not a final bill of materials and not
a purchase instruction.

The point of this survey is to find readily documented hardware that can exercise
the already-defined interaction and display fixtures. The final device still has
to come in substantially below the cost of a low-cost Android tablet unless it
earns the difference with a clear capability advantage.

Prices and stock below are observations from 2026-09-18 and will change.

## Prototype computer: Raspberry Pi Zero 2 W

The Raspberry Pi Zero 2 W is a useful first prototype computer because it
already supplies:

- a normal Linux userspace suitable for a real terminal;
- microSD storage;
- 2.4 GHz Wi-Fi and an onboard antenna;
- Bluetooth;
- a quad-core 64-bit Arm Cortex-A53 processor;
- 512 MB RAM;
- mini-HDMI;
- a 40-pin GPIO footprint that exposes I2C and I2S-capable pins.

Physical size is about 65 × 30 mm.

This is a prototype fit, not a processor commitment. The final product may use
a different Linux-capable SoC or board.

Observed sources:

- Adafruit Product 5291, Raspberry Pi Zero 2 W:
  https://www.adafruit.com/piz2w
  - observed price: $19.05;
  - observed state: out of stock.
- DigiKey product highlight:
  https://www.digikey.com/en/product-highlight/r/raspberry-pi/raspberry-pi-zero-2-w
  - observed SC1176 price: $15.00;
  - observed immediate quantity: 0.

The important part is the architecture and documented interfaces, not current
stock at either seller.

## Baseline display path: 800 × 480 TFT over HDMI

The 80 × 24 terminal target needs 640 × 384 pixels with an 8 × 16 cell before
allowing any extra status area. An 800 × 480 panel therefore has enough pixel
budget for the target without horizontal panning.

### 5-inch panel

Adafruit Product 1680:

https://www.adafruit.com/product/1680

Observed:

- 800 × 480;
- 5-inch class;
- about 110 × 67 mm screen area;
- no touch layer;
- $27.50;
- in stock.

With an 8 × 16 cell, the 80 × 24 terminal occupies 640 × 384 pixels and leaves
160 horizontal pixels and 96 vertical pixels outside that grid for margins,
status, or a larger font choice.

### 7-inch panel

Adafruit Product 2353:

https://www.adafruit.com/product/2353

Observed:

- 800 × 480;
- 7-inch class;
- $29.95;
- in stock.

It has the same text-cell budget as the 5-inch panel but physically larger
glyphs. Since the requirements allow small-tablet scale, this is worth measuring
against the 5-inch panel rather than assuming the smaller panel is better.

### HDMI decoder

Adafruit Product 2218, TFP401 HDMI/DVI decoder:

https://www.adafruit.com/product/2218

Observed:

- drives the Adafruit 40-pin TTL panels from HDMI/DVI;
- $29.95;
- in stock;
- Adafruit has a complete wiring/tutorial path for the 5-inch and 7-inch
  displays.

For the first prototype this extra decoder cost is defensible because it keeps
the Raspberry Pi GPIO pins free for buttons and I2S audio.

The combined observed display-path prices before cables are:

- 5-inch TFT + TFP401: $57.45;
- 7-inch TFT + TFP401: $59.90.

Those are prototype integration prices, not acceptable final-product display
costs.

## Do not use the cheaper DPI Kippah path for this prototype

Adafruit's DPI Display Kippah can drive the same TFT panels without the HDMI
decoder and is cheaper, but its documented Raspberry Pi interface consumes GPIO
2 through 21 inclusive.

Source:

https://learn.adafruit.com/adafruit-dpi-display-kippah-ttl-tft?view=all

That includes the ordinary I2C pins and the Raspberry Pi I2S pins used by the
microphone path. The initial Tamagotchi prototype requires both a substantial
physical-key interface and a built-in microphone. Saving money on the display
adapter while consuming nearly all of those pins would make the prototype less
representative.

This is a prototype wiring decision only. A final board can drive a display
directly from a suitable SoC without reproducing this conflict.

## Low-power display candidate: SHARP Memory LCD

Adafruit Product 4694:

https://www.adafruit.com/product/4694

Observed:

- 2.7-inch;
- 400 × 240 monochrome;
- reflective / no backlight;
- fast-refresh Memory LCD rather than electrophoretic e-paper;
- $44.95;
- out of stock.

This part remains interesting as evidence about the desired old-school,
persistent/low-idle-power visual character, but it is not a baseline terminal
display.

At 400 pixels wide:

- a 6-pixel-wide cell yields only 66 columns;
- an 80-column layout would require a 5-pixel-wide cell;
- on the 58.8 mm active width, a 6-pixel cell is under 0.9 mm wide.

That is useful for a status-display experiment, not enough evidence to call it
comfortable for the first-class terminal requirement.

The candidate should be revisited only if a larger, similarly fast Memory LCD
or another reflective display satisfies the actual text fixture.

## Physical-key feel prototype: silicone elastomer keypad

Adafruit Product 1611:

https://www.adafruit.com/product/1611

DigiKey listing:

https://www.digikey.com/en/products/detail/adafruit-industries-llc/1611/5823361

Observed:

- silicone elastomer 4 × 4 keypad;
- 60 × 60 mm;
- $4.95;
- Adafruit in stock;
- DigiKey listed 355 in stock at $4.95.

The rubber keypad is a useful cheap test of the required soft press and travel.
It is not the final layout:

- one 4 × 4 pad has only 16 positions while the requirements define 17 actions;
- the v0 layout deliberately uses directional rockers for Task, Page, Half-page,
  and Clipboard;
- a flat 4 × 4 matrix does not prove those rockers can be identified by touch.

Two pads would cost $9.90 at the observed unit price and are enough to prototype
all action semantics while the final tactile geometry is still being designed.

Do not buy the full Feather-based NeoTrellis kit merely to obtain a keypad. The
main computer is not a Feather, and that would pay for an unrelated compute
board.

## Microphone: SPH0645LM4H I2S breakout

Adafruit Product 3421:

https://www.adafruit.com/product/3421

DigiKey listing:

https://www.digikey.com/en/products/detail/adafruit-industries-llc/3421/6691114

Adafruit Raspberry Pi wiring guide:

https://learn.adafruit.com/adafruit-i2s-mems-microphone-breakout/raspberry-pi-wiring-test

Observed:

- digital I2S microphone;
- roughly 50 Hz–15 kHz audio range;
- $6.95;
- DigiKey listed roughly 2,400 in stock;
- Adafruit's guide explicitly covers Raspberry Pi OS Bookworm and Bullseye,
  including 32-bit and 64-bit Lite releases.

This is a strong prototype microphone because it directly tests the intended
built-in dictation path and has a current Raspberry Pi tutorial. It does not
commit the final product to this exact microphone.

## Antenna and networking

No separate antenna part is needed for the first prototype because the Pi Zero
2 W already has 2.4 GHz Wi-Fi, Bluetooth, and an onboard antenna.

The physical enclosure still has to be tested for RF effects. A built-in radio
does not establish acceptable range after the board is placed behind a display,
battery, wiring, and enclosure material.

## Battery and charging: intentionally not selected yet

Do not select the battery/boost/charger from a tutorial BOM before measuring the
actual prototype.

The display choice changes the load substantially, and the Pi Zero 2 W vendor
recommendation allows for a 5 V, 2.5 A supply. The old Adafruit portable-display
projects using a 1 A boost converter are useful references but are not enough to
establish margin for this complete device.

First measure:

- Pi idle current;
- Pi current during Wi-Fi traffic;
- display current at usable brightness;
- microphone + keypad interface current;
- boot peak;
- worst observed combined load.

Then size the battery, charger, boost/buck path, connector, and thermal margin.

## First prototype stack worth physically testing

A behavior prototype can therefore be assembled around:

- Raspberry Pi Zero 2 W or an equivalent Linux-capable Zero-format board;
- 5-inch or 7-inch 800 × 480 TFT;
- TFP401 HDMI decoder;
- one or two silicone elastomer keypads for action/feel testing;
- SPH0645LM4H I2S microphone;
- temporary bench power rather than a prematurely selected battery circuit.

This stack intentionally overpays for modular boards. Its purpose is to test:

- 80 × 24 terminal readability at 5 versus 7 inches;
- key layout and soft-key feel;
- direct terminal navigation;
- queue controls;
- copy/paste/select behavior;
- microphone/dictation plumbing;
- Wi-Fi behavior;
- actual power draw.

Only after those measurements should the design collapse the prototype into a
cheaper dedicated PCB, direct display interface, final keypad geometry, and
battery system.
