# Agent Tamagotchi — physical control layout v0

Status: interaction layout only. This does not select switches, keycaps, a PCB,
processor, enclosure, or display.

The requirements define 17 frequent physical actions. The first layout keeps the
important actions direct while using paired rockers for naturally paired
navigation and clipboard operations.

## Control inventory

Dedicated keys:

- **Send**
- **Stop**
- **Continue**
- **Voice**
- **Projects**
- **Back**
- **Blocker**
- **Terminal**
- **Select all**

Two-way rockers:

- **Task** — previous / next task or conversation
- **Page** — page up / page down
- **Half page** — half-page up / half-page down
- **Clipboard** — copy / paste

That gives all 17 required actions with 13 physical controls. No required action
depends on a touchscreen gesture.

## Physical grouping

The enclosure should make the groups identifiable by position and feel, not by
color.

### Primary action cluster

Keep these under the dominant thumb or equally easy to reach:

```text
[ Voice ]   [ Continue ]

[ Blocker ] [ Send     ]   [ Stop ]
```

- **Stop** must be physically distinct from Send and Continue. It should not be
  easy to hit accidentally, but it must not require a chord, menu, or long
  press.
- **Send** should be one of the largest ordinary keys.
- **Continue** is intentionally separate from Send. It means continue the active
  work item; it does not submit whatever happens to be in the text editor.
- **Blocker** goes directly to the reason a work item needs attention.

### Navigation edge

A vertical edge cluster keeps reading/navigation possible without moving a hand
over the display:

```text
[ Task       ↑ / ↓ ]
[ Page       ↑ / ↓ ]
[ Half page  ↑ / ↓ ]
```

The two directions of each rocker must be distinguishable by touch. Holding a
scroll direction may repeat, but a single press always means one discrete
movement.

### Utility row

```text
[ Back ] [ Projects ] [ Terminal ] [ Select all ] [ Copy / Paste ]
```

The clipboard rocker uses one direction for Copy and the opposite direction for
Paste. Copy and Paste must have different tactile directions; they should not
share a timing-dependent short/long-press distinction.

## Semantics

### Send

Submit the current composed input to the active work item.

If there is no composed input, Send does nothing destructive. The interface
should make the inactive state visible rather than inventing content to send.

After a successful submit, the normal queue behavior may advance to the next
item needing attention.

### Stop

Request cancellation of the active job immediately.

A local button press and a remote cancellation are distinct facts. If the
remote service has only acknowledged a stop request but the job is still
running, the display must not show the job as stopped.

### Continue

Send the explicit continuation action for the active work item. It is not an
alias for Send and does not consume unsent editor text.

### Voice

Start or stop dictation for the current input field. Dictation populates text;
it does not automatically press Send. This keeps transcription errors reviewable
before submission.

### Task rocker

Move between work items without changing their queue status. Previous and next
refer to the locally visible ordering.

### Page and half-page rockers

Move through the active output/terminal view. They should preserve the current
selection where the view can do so without ambiguity.

### Projects

Open the locally inspectable project/task list. It is navigation, not a request
for a model to choose a project.

### Back

Return to the previous view or cancel the current local navigation state. It
must not silently cancel a running remote job; Stop owns that meaning.

### Blocker

Open the first concrete reason the active item needs attention: a failed check,
missing decision, permission request, unresolved conflict, or other retained
blocking evidence.

If no concrete blocker exists, say so. Do not manufacture a model explanation
merely because the key was pressed.

### Terminal

Open the terminal directly and preserve its working directory, process/session
identity, scroll position, and current selection where practical.

### Select all

Select the active view's defined text domain. The selected domain must be
visible before a destructive follow-up action.

Initial domains:

- terminal: current selectable scrollback/output domain;
- chat/output: current response or explicitly focused text region;
- editor: complete current input.

A view with no unambiguous text domain should reject Select all rather than
guess.

### Clipboard rocker

Copy uses the current selection. Paste inserts clipboard text into the active
editable input; it does not execute terminal text or submit chat text
automatically.

## Tactile requirements

- Stop, Send, and Voice must be identifiable without looking.
- Paired rockers must reveal direction by geometry or travel.
- Core actions must remain usable with wet or dirty fingers.
- Do not rely on capacitive sensing for these controls.
- Do not rely on color as the only distinction.
- Accidental Stop and accidental Send should require different physical errors;
  they should not be adjacent identical keys with no tactile boundary.

## First interaction acceptance fixture

A prototype layout is acceptable only if a user can, without touching the
display:

1. move to the next queued work item;
2. read one full page and then half a page;
3. open the blocker for that item;
4. return to the work item;
5. dictate text and review it;
6. send it;
7. advance to another item;
8. open the terminal;
9. page through output;
10. select, copy, and paste text without executing the paste;
11. request Stop on a running item;
12. distinguish “stop requested” from “stopped.”

This fixture is about interaction. It does not establish switch durability,
ingress resistance, battery life, display suitability, or network reliability.
