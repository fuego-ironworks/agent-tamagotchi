# Agent Tamagotchi — display capacity v0

Status: display behavior and text-capacity requirements before display
technology selection.

The display is primarily for agent state, long text, task lists, and a
first-class terminal. Resolution alone is not an acceptance criterion. A
candidate must be readable at the intended physical size and fast enough for the
interactions below.

## Text capacity

Measure candidates in readable monospaced cells at the intended viewing
distance, not merely pixels.

### Hard minimum

The normal terminal view must expose at least:

```text
64 columns × 20 rows
```

without horizontal panning.

A display that cannot do this at a comfortable readable cell size is not the
baseline terminal display for this device.

### Target

Prefer enough usable area for:

```text
80 columns × 24 rows
```

while leaving a small persistent status region outside the terminal grid where
practical.

Eighty columns is a useful target because ordinary terminal programs, source
text, logs, and tables frequently assume roughly that width. It is a target,
not permission to make the type uncomfortably small.

### Chat and queue views

The same display should be able to show, without a modal overlay:

- active project/task identity;
- current state such as running, blocked, failed, or completed;
- at least one useful paragraph of response text;
- a visible indication when unseen text exists above or below;
- the current input/dictation state when composing;
- an unambiguous selection domain when Select all is active.

The status area should remain compact enough that it does not turn an otherwise
usable text display into a narrow message strip.

## Refresh behavior

A persistent or reflective display is useful only if it remains practical for
terminal and queue navigation.

A candidate should be tested for these observable behaviors:

- ordinary key echo appears quickly enough that typing does not feel detached
  from the keypress;
- a Page or Half-page press produces a completed readable update without a
  disruptive multi-second flash;
- holding a scroll control can produce repeated updates rather than forcing a
  press-wait-press rhythm;
- partial refresh does not leave enough ghosting to confuse terminal glyphs,
  selection state, or job status;
- returning to a static screen does not require continuous high-power redraw.

For the first prototype, use these as screening targets rather than promises
about a final product:

- visible key echo normally within about 150 ms;
- a page navigation update normally within about 250 ms;
- sustained repeated text navigation of at least 5 readable updates per second.

A display may miss one numeric target and still deserve measurement if the
actual interaction remains good, but a candidate with visibly delayed typing or
multi-second navigation should not be described as suitable for the
first-class terminal requirement.

## Persistence and idle state

When practical, the last useful state should remain visible while the user is
not interacting.

Useful idle content includes:

- active task and state;
- number of blocked/failed/completed-unreviewed items;
- last short status or response excerpt;
- whether a terminal/job is still running;
- network/offline state;
- battery state.

This requirement does not force e-paper. A memory LCD, conventional monochrome
LCD, low-power TFT, or another display may satisfy it with a different power
strategy.

## Monochrome and state encoding

The interface must work correctly in monochrome.

Do not encode running/blocked/failed/completed states by color alone. Use text,
symbols, borders, inversion, or other shape/contrast differences that survive a
monochrome display.

Animations are optional decoration. A stable textual state must exist for every
important condition.

## Terminal acceptance fixture

Before selecting a display technology, render the same fixture on each
candidate:

1. an 80-column source/log line;
2. a 64-column fallback terminal layout;
3. 24 rows of mixed terminal output;
4. inverse/selected text;
5. a rapidly changing command line while typing;
6. Page and Half-page repeated scrolling;
7. a long-running job status adjacent to terminal output;
8. static text left unchanged long enough to expose persistence, burn-in, or
   ghosting behavior;
9. the same content under ordinary room light and a brighter work area.

Record:

- physical active area;
- readable columns and rows;
- chosen cell dimensions;
- measured key-to-visible-update latency;
- full and partial refresh time;
- ghosting after repeated scrolling;
- idle and active power where measurement is available.

## Technology decision boundary

Do not pick a display from pixel count, marketing refresh rate, or persistence
alone.

The component search starts only after a candidate can be evaluated against the
text-capacity and interaction fixture above. E-paper is acceptable only if its
measured refresh and ghosting behavior remain usable for the terminal; a
conventional display is acceptable only if its idle-power behavior remains
reasonable for an always-nearby desk device.
