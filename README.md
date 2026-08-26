# The Trvler.co Magazine — beehiiv Welcome Email

One file for desktop, tablet and phone. Built from the boarding-pass design
(desktop + mobile HTML/CSS package).

**Live preview:** open `index.html` — that is the email exactly as a subscriber sees it.

---

## What is in here

| File | What it is |
|---|---|
| `index.html` | The email. This is what gets pasted into beehiiv. |
| `img/` | 15 images the email uses (752 KB total) |
| `preview-desktop.jpg` | How it looks on a laptop |
| `preview-mobile.jpg` | How it looks on a phone |

---

## How it was built

The original design uses CSS the way a web page does — torn ticket edges,
dashed perforations, barcodes, round stamps, radial gradients, `clip-path`.
**None of that survives in Gmail or Outlook.**

So the design was rendered in a real browser at **1200px (2× of 600)** and each
section captured as one crisp image. Those images are then laid out with plain
email tables and real links. It looks identical to the design but behaves like
an email.

---

## Three bugs found in the original package, and fixed

**1. Everything printed twice.**
`hero.png` already contains the headline, the stamps and the plane trail baked
in — but the HTML drew all of them a second time on top. Same with
`coast.png`, which carries the "TRAVEL UPDATES" text and the CAPRI stamp inside
the artwork. Both overlays are now suppressed.

**2. Wrong coordinates.**
`BANFF / CANADA` was labelled with **London's** numbers (51.4968° N, 0.1224° W).
Corrected to **51.1784° N, 115.5708° W**.
`SAHARA / MOROCCO` was also wrong — corrected to **31.7917° N, 7.0926° W**.

**3. The page header was removed.**
An email has no navigation, so the logo bar and hamburger menu are gone.

---

## Two things that still need fixing at source

These are baked inside `hero.png` and cannot be edited here — the hero needs to
be exported again:

- The round stamp reads **"DVENTURE AWAITS"** — the **A** is missing.
- The Banff stamp inside the photo still shows **48.6467° N** (should be 51.1784° N).

---

## Image quality

Every section ships at **1200px** wide and displays at 600px — 2x on a laptop,
over 3x on a phone. Saved at JPEG quality 94.

The photos inside the original package were small, so they were upsampled with
Lanczos and sharpened **before** rendering, rather than letting the browser
stretch them:

| Photo | In the package | Prepared at |
|---|---|---|
| hero | 641 x 264 | 1500 x 618 |
| coast | 376 x 144 | 900 x 345 |
| tokyo | 379 x 117 | 900 x 278 |
| desert | 480 x 131 | 900 x 246 |
| banff | 309 x 129 | 860 x 359 |
| island / aurora / city / lagoon | 311 x ~90 | already large enough, untouched |

Sharpening is deliberately light. An earlier build used a strong unsharp mask,
which put speckle into flat areas such as the Tokyo night sky - that grain is
what reads as "pixelated". A gentle pass keeps definition without the crunch.

Saved at JPEG quality 95. Total image weight: **about 1 MB**.

**For true HD there is one thing only the source can give:** the full-size
originals of those five photos. Sharpening recovers definition, but it cannot
put back detail that was never in a 309px file. If the originals are exported at
around 1200-1500px wide, they can be dropped straight in and re-rendered.

---

## Fonts — trvler.co's own

The original package used Georgia and Arial Narrow. Everything now uses the
site's real typefaces:

| Where | Font |
|---|---|
| Ticket labels (TRAVEL UPDATES, VIDEOS, SHORTS, EXCLUSIVE STORIES), the 01-04 numerals, YOUR JOURNEY STARTS HERE | **56th Street** — the site's display face, loaded from `app/assets/fonts/56thStreet-Regular.otf` |
| Headings, paragraphs, coordinates, stamps, footer | **Plus Jakarta Sans** — the site's body face |

Email clients cannot load custom fonts as live text. It works here because
these sections ship as **images**, so the real brand fonts are baked into the
artwork. The handful of live text lines name Plus Jakarta Sans first and fall
back to Arial.

## Text alignment

`The world is waiting—and<br>you're officially in.` had a hard line break that
stranded **"—and"** alone on the second line. The break and the dash are gone:

> The world is waiting, and you're officially in.

It now sets as two balanced lines on a laptop and on a phone.

---

## Where every link goes

| Section | Link |
|---|---|
| Hero | `trvler.co` |
| 01 Travel Updates | `trvler.co/blog` |
| 02 Videos | `trvler.co/video` |
| 03 Shorts | `youtube.com/@trvler-co/shorts` |
| 04 Exclusive Stories | `trvler.co/blog` |
| Your Journey Starts Here | `trvler.co` |
| Gallery | `trvler.co` |
| Social icons | Instagram · Facebook · TikTok · YouTube · X · Pinterest |

Every trvler.co link carries `?utm_source=newsletter&utm_medium=email&utm_campaign=welcome`
so Google Analytics can show how much traffic the newsletter actually sends.

---

## One thing worth knowing

This design carries most of its words **inside images**. Gmail blocks images for
senders it does not recognise yet, so in that case the subscriber sees only the
`alt` text. Every `alt=""` in `index.html` is written as a full sentence for
exactly that reason — please do not shorten them.

---

## Putting it into beehiiv

1. Upload all 15 files from `img/` to **Newsletter → Media library**.
2. Replace every `src="img/..."` with the URL beehiiv returns.
3. **Settings → Emails → Configure welcome email** → add a **Custom HTML** block
   → paste everything between `PASTE FROM HERE` and `PASTE UNTIL HERE`.
4. Send a test to the **TEST** segment. Open it on a phone. Click every link.
5. Turn the welcome-email toggle **ON** only after `mail.trvler.co` verifies.

The unsubscribe link and postal address are **not** in this file on purpose —
beehiiv attaches its own legal footer underneath automatically.

---

## Checked on

| | Desktop 700px | Phone 390px |
|---|---|---|
| Horizontal overflow | none | none |
| Images loading | 15 / 15 | 15 / 15 |
| Links working | 13 / 13 | 13 / 13 |
| Six social icons | all visible | all visible |
