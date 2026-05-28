# New Section Archetypes — Design Spec v1

**Author:** Cole (Lead Visual Identity Designer)
**Date:** 2026-05-27
**For:** Ethan Glines's personal website (`index.html`)
**Design system:** Warm Editorial (locked) — cream `#F7F3EC`, ink `#1A1A1A`, warm amber `#C8742A`, forest `#3E5C50`, neutral `#8A8278`
**Typography:** Fraunces (display) / Inter (body) / JetBrains Mono (accents)
**Signature moves to echo:** hand-drawn SVG underlines, pulsing accent dot, hairline section rules, eyebrow + section-rule combo, mono micro-labels, magnetic CTAs, subtle Y-translate card hover

---

## Updated Page Flow (with new sections inserted)

| # | Section | Status | Anchor |
|---|---------|--------|--------|
| 1 | Header (fixed) | Existing | — |
| 2 | Hero | Existing | `#top` |
| 3 | **NEW — Elevator Pitch Module** | **D** | `#pitch` |
| 4 | Bio / Operator Intro | Existing | `#about` |
| 5 | Stat Strip (count-up) | Existing | — |
| 6 | **NEW — Case Study Cards (replaces "Selected Work")** | **A** | `#work` |
| 7 | Experience Timeline | Existing | `#timeline` |
| 8 | **NEW — Blog & Reflection Card Grid** | **B** | `#field-notes` |
| 9 | Capabilities Strip | Existing | `#capabilities` |
| 10 | **NEW — Certifications Badge Strip** | **C** | `#credentials` |
| 11 | Resume | Existing | `#resume` |
| 12 | (Testimonials — currently hidden, will return) | Existing | — |
| 13 | Contact | Existing | `#contact` |
| 14 | Footer | Existing | — |

**Nav update required:** Add `Pitch` (or fold into hero CTA), `Field Notes` to primary nav. Recommend final nav: `Pitch · Work · Field Notes · Capabilities · Contact`.

---

## A. Case Study Cards (Inline Expanded) — Replaces "Selected Work"

### Decision: Replace, don't append

The existing "Selected Work" section already holds Blue Luna and Travel With Glines as project cards with role meta + outcomes + media. Reed's case study drafts are richer versions of the same content (Blue Luna + SyTech) with deeper strategic narrative. **Recommendation:** the case study format BECOMES the new "Selected Work" treatment. Travel With Glines stays as a project card style (it's an experience, not a strategic case study), but Blue Luna and SyTech upgrade to the full case study format. Net: section becomes a hybrid — two case study blocks first (Blue Luna, SyTech), then the Travel With Glines card retained below.

### A.1 Layout — Full-width, two-column interior

Full-width section. Each case study is a single `<article class="case-study">` block stacked vertically (not side-by-side). Interior uses a two-column grid: **left column** (40%) holds the meta + pull quote; **right column** (60%) holds Challenge / What I did / Outcome blocks. Mobile collapses to single column.

```
┌─ CASE STUDY ─────────────────────────────────────────────────┐
│  ┌──────────────────┐  ┌────────────────────────────────────┐│
│  │ 01 / SYTECH      │  │ THE CHALLENGE                       ││
│  │ ━━━━             │  │ [2-3 sentences]                     ││
│  │ Records          │  │                                     ││
│  │ Management       │  │ WHAT I DID                          ││
│  │ Firm Rebrand     │  │ — bullet                            ││
│  │                  │  │ — bullet                            ││
│  │ Role · Year ·    │  │ — bullet                            ││
│  │ Industry         │  │ — bullet                            ││
│  │                  │  │                                     ││
│  │ ┌──────────────┐ │  │ THE OUTCOME                         ││
│  │ │ " pull quote │ │  │ [2-3 sentences]                     ││
│  │ │   in serif   │ │  │                                     ││
│  │ │   italic   " │ │  │ [View live →]                       ││
│  │ └──────────────┘ │  │                                     ││
│  └──────────────────┘  └────────────────────────────────────┘│
└──────────────────────────────────────────────────────────────┘
```

### A.2 Structure

```html
<section class="case-studies" id="work">
  <div class="wrap">
    <div class="section-head">
      <span class="section-rule"></span>
      <p class="eyebrow">Selected Work</p>
      <h2>Two case studies. One operator playbook.</h2>
    </div>

    <article class="case-study">
      <div class="case-study-grid">
        <aside class="case-study-meta">
          <p class="case-study-index">01</p>
          <h3 class="case-study-title">SyTech</h3>
          <p class="case-study-subtitle">Records Management Firm Rebrand &amp; Multipage Site</p>
          <div class="case-study-meta-strip">
            <span><strong>Role</strong> · Lead Strategist, Copywriter, Builder</span>
            <span><strong>Year</strong> · 2026</span>
            <span><strong>Industry</strong> · Public Sector Tech</span>
          </div>
          <blockquote class="case-study-quote">
            <p>A two-minute pitch is a confession that you don't know your own value yet.</p>
          </blockquote>
        </aside>

        <div class="case-study-body">
          <div class="case-study-block">
            <p class="case-study-label">The challenge</p>
            <p>SyTech had 25 years of work and 800 million records...</p>
          </div>
          <div class="case-study-block">
            <p class="case-study-label">What I did</p>
            <ul class="case-study-list">
              <li>Compressed the two-minute pitch...</li>
              <li>Rebuilt the messaging architecture...</li>
              <li>Wrote, designed, and shipped a twelve-page site...</li>
              <li>Held the line on data sovereignty...</li>
            </ul>
          </div>
          <div class="case-study-block">
            <p class="case-study-label">The outcome</p>
            <p>Site is live in production...</p>
          </div>
          <a href="https://ethan-glines.github.io/SyTech-Website/" class="case-study-cta magnetic" target="_blank" rel="noopener">
            View SyTech live <span aria-hidden="true">→</span>
          </a>
        </div>
      </div>
    </article>

    <article class="case-study">…Blue Luna case study…</article>

    <!-- Travel With Glines retained as legacy project-card pattern below -->
    <article class="project-card">…existing TWG card…</article>
  </div>
</section>
```

### A.3 CSS specs

- **Section padding:** existing `--section-pad` clamp
- **Grid:** `grid-template-columns: minmax(0, 0.7fr) minmax(0, 1fr); gap: clamp(2rem, 5vw, 4.5rem);` Mobile (<880px): single column, `gap: 2rem`.
- **Case study background:** `var(--surface)` (white), `border-radius: 14px`, `border: 1px solid var(--hairline)`, `padding: clamp(2rem, 4vw, 3.5rem)`
- **Index number (`01`, `02`):** Fraunces, `clamp(2.75rem, 4vw, 3.5rem)`, ink color, opsz 96, opacity 0.18 — sits as a quiet editorial chapter mark above the title.
- **Title:** Fraunces, 2.25-3rem, opsz 72, weight 500
- **Subtitle:** Fraunces italic, 1.125-1.25rem, weight 400, neutral color
- **Meta strip:** mono, 0.72rem, neutral, stacked vertically on left column with `gap: 0.5rem`; `strong` is ink
- **Pull quote:** Fraunces italic, opsz 72, SOFT 100, weight 400, 1.25-1.5rem, ink color. Left border 2px solid `var(--accent)`, padding-left 1.25rem. Lives at the bottom of the left column.
- **Block label ("The challenge", "What I did", "The outcome"):** mono, 0.72rem, uppercase, letter-spacing 0.12em, accent color (`var(--accent)`), margin-bottom 0.75rem
- **Block paragraph:** Inter, 1rem-1.0625rem, line-height 1.7, ink color, max-width 60ch
- **Bullet list (`.case-study-list`):** custom marker — use the same orange dash bullet from existing `.project-outcomes::before` (6px × 2px amber bar at top: 0.65rem)
- **Block spacing:** `gap: 2rem` between blocks
- **CTA:** reuse `.project-cta` styling — amber link with arrow, `gap` widens on hover

### A.4 Behavior

- **Scroll reveal:** existing `.reveal` pattern. The meta column reveals first (no delay); body column reveals with `data-delay="1"`.
- **Hover:** Subtle border color shift `border-color: rgba(200, 116, 42, 0.35)` over 350ms. No Y-translate (the card is too large to lift gracefully — translate would create awkward shadow rendering). Top hairline-to-accent rule animation: `::before` element on the card grows from `scaleX(0)` to `scaleX(1)` on hover, same pattern as existing `.project-card::before`.
- **Pull quote:** add a small hand-drawn underline beneath ONE word in each quote (e.g., underline "value" in SyTech quote, "decide" in Blue Luna quote) using the existing `.underlined--sm` pattern with `.scroll-draw` so it animates in when the case study enters the viewport.

### A.5 Aesthetic intent (FEEL)

**Editorial long-form, not card.** This should read like a serious case study in a design annual — confident, deliberate, room to breathe. The pull quote on the left isn't decoration; it's the strategic insight rendered as the case study's takeaway line. The amber section labels ("The challenge / What I did / The outcome") give it newspaper-feature pacing — each block is a beat in a structured story. Calm, dense, expensive-feeling. NOT a "tap to expand for more" card.

### A.6 Copy guidance

Use Reed's drafts verbatim. Both currently sit ~220 words — that's correct. The pull quote should be ONE line, max 18 words, from the closing line of Reed's quote blocks. Bullets stay tight: 1 sentence each, no run-ons.

### A.7 Page-flow recommendation

**Replace the "Selected Work" section in place.** The case studies inherit `#work` as the anchor. Travel With Glines becomes the third item below the two case studies, retained in the existing `.project-card` style — distinct format signals "this is a different kind of project: an experience, not a strategy engagement." That format contrast IS the point.

---

## B. Blog & Reflection Card Grid — "Field Notes"

### B.1 Section naming

Call it **"Field Notes"** (not "Blog"). Operator voice, reads as marginalia / observations from real practice. Mono micro-label: `FIELD NOTES`. H2: *"What I'm noticing."* (or *"Operator's marginalia."*)

### B.2 Layout — 2-column desktop, 1-column mobile, all-expanded posts

5 cards total. Recommend **2-column grid at desktop (≥980px)**, single column on mobile. Cards are tall (200-400 word posts → ~6-9 inches of text), so 3-up grid would be too dense — 2-up gives each card the room its essay deserves.

**Why all-expanded (no truncation):** Truncation with "Read more" toggles adds JS state and creates inconsistent card heights that fight the grid. Field Notes posts are short enough (200-400w) to render in full. The LinkedIn link at the bottom serves as citation, not "read more." If a card gets >500 words later, we'll revisit.

### B.3 Structure

```html
<section class="field-notes" id="field-notes">
  <div class="wrap">
    <div class="section-head">
      <span class="section-rule"></span>
      <p class="eyebrow">Field Notes</p>
      <h2>What I'm <span class="underlined underlined--sm">noticing<svg…/></span>.</h2>
      <p class="section-subhead">Short essays on marketing, branding, and operating in the wild. Originally posted to LinkedIn — restored here in their full form.</p>
    </div>

    <div class="field-notes-grid">
      <article class="field-note">
        <div class="field-note-meta">
          <span class="field-note-num">01</span>
          <span class="field-note-date">May 2026</span>
          <span class="field-note-topic">Brand Loyalty</span>
        </div>
        <h3 class="field-note-title">Why "Coke People" Stay Loyal</h3>
        <div class="field-note-body">
          <p>Over the last 10 years…</p>
          <p>Most people grab a soda…</p>
          <!-- full post text, paragraphs preserved -->
        </div>
        <!-- Optional media slot -->
        <!-- <figure class="field-note-media">…</figure> -->
        <footer class="field-note-footer">
          <span class="field-note-engagement">
            <span class="emoji" aria-hidden="true">♡</span> 8 &middot; 5 comments
          </span>
          <a href="https://linkedin.com/…" class="field-note-source" target="_blank" rel="noopener">
            Originally on LinkedIn <span aria-hidden="true">↗</span>
          </a>
        </footer>
      </article>
      <!-- × 5 -->
    </div>
  </div>
</section>
```

### B.4 CSS specs

- **Grid:** `grid-template-columns: 1fr; gap: clamp(1.5rem, 2.5vw, 2.25rem);` Tablet (≥720px): `repeat(2, 1fr)`. Stays 2-col through desktop (no 3-col jump — preserves reading width).
- **Card:** `background: var(--surface); border: 1px solid var(--hairline); border-radius: 12px; padding: clamp(1.75rem, 2.5vw, 2.5rem);`
- **Index number (`01-05`):** mono, 0.72rem, amber color, weight 500 — micro-label, positioned in meta row
- **Meta row:** flex, gap 1rem, mono uppercase 0.7rem, neutral color. Separated by middle-dot characters.
- **Title:** Fraunces, opsz 48, weight 500, `clamp(1.5rem, 2vw, 1.875rem)`, ink, letter-spacing -0.012em. Tight margin-bottom 1.25rem.
- **Body:** Inter, 0.9375rem, line-height 1.7, ink, max-width none (within card). `p + p { margin-top: 1rem; }`. Emoji preserved inline using existing `.emoji` utility — they're part of Ethan's voice.
- **Optional media (`.field-note-media`):** `aspect-ratio: 16/10`, `border-radius: 8px`, `margin: 1.5rem 0`, `object-fit: cover`. Designed for Post 4 (Japan photos) — accommodates 1 image OR a 2-up gallery via internal grid.
- **Footer:** flex space-between, padding-top 1.25rem, border-top 1px solid `var(--hairline)`, margin-top 1.5rem
- **Engagement:** mono 0.7rem, neutral, with a small ♡ glyph in amber (`color: var(--accent)` on the heart only). Quiet, never the focus.
- **LinkedIn source link:** mono 0.7rem, uppercase, letter-spacing 0.1em, neutral on default — hovers to amber. Arrow glyph (↗) signals external. **This is a citation, not a CTA.** Same visual weight as engagement count.

### B.5 Signature design move — hand-drawn underline on every 3rd post title

Cycle a hand-drawn amber underline (`.underlined--sm` pattern) beneath ONE word in titles on cards 1, 3, and 5. The underlines vary slightly (different SVG paths) so they don't feel mechanical. This is what prevents the grid from feeling like a LinkedIn iframe wall.

### B.6 Behavior

- **Scroll reveal:** `.reveal` cascade with `data-delay` staggered 0/1/2/0/1 down the grid.
- **Hover:** Card-pattern from existing `.project-card`. `transform: translateY(-3px); box-shadow: 0 18px 36px -22px rgba(26,26,26,0.18); border-color: rgba(200,116,42,0.35);` Top `::before` accent rule grows from `scaleX(0)` to `scaleX(1)` (same pattern as project-card). Transition 350ms `var(--ease-out)`.
- **No expansion/collapse JS.** Cards are static-height to their content.
- **LinkedIn link:** standard `target="_blank" rel="noopener noreferrer"`. Arrow translates `2px,-2px` on hover (existing pattern).

### B.7 Aesthetic intent (FEEL)

**Editorial column, not social embed.** Each card should feel like a short essay in a magazine — eyebrow / title / body / citation. The LinkedIn link is a footnote attribution ("originally appeared in…"), NOT a "follow me on LinkedIn" CTA. The post text gets to breathe at full editorial proportions. The cards have personality from the hand-drawn underlines and emoji-in-body — they look unmistakably Ethan's, never templated.

### B.8 Copy guidance

- **Title format:** Use Scout's suggested headlines from `linkedin-posts-extracted.md` (2-6 words, operator voice). Examples already proposed:
  - 01 — "Why 'Coke People' Stay Loyal"
  - 02 — "Positioning Without Research Is an Empty Waiting Room"
  - 03 — "Spreadsheets Can't See the Customer"
  - 04 — "The Photo Sold the Ramen"
  - 05 — "Two Humans, Twenty-Eight AI Roles"
- **Body:** Verbatim post text. Preserve emoji inline. Strip the `#hashtags` block at the bottom (cluttered, doesn't serve the editorial format) — they belong on LinkedIn, not here.
- **Topic tag:** 1-2 word categorization (Brand Loyalty / Market Research / Strategy / Marketing Myopia / AI Workflow).
- **Engagement:** Show only if ≥5 likes. Quiet flex — never a metric flex.

### B.9 Page-flow recommendation

**Between Experience Timeline and Capabilities Strip.** Reasoning: the Timeline is "what I've done"; Field Notes is "what I'm thinking now." That transition is editorially correct — you've earned the right to opine after we've seen the work. Capabilities then catches the reader with a clear "here's what I deliver" closer before the funnel narrows to Resume and Contact.

---

## C. Certifications Badge Strip — "Credentials"

### C.1 Layout — Thin strip, badge cards

Position as a thin section between Capabilities and Resume. **Horizontal strip layout:** badges flow left-to-right in a row at desktop (`grid-template-columns: repeat(auto-fill, minmax(280px, 1fr))`), stacking at mobile. Currently 1 badge — designed to scale to 6-8 cleanly. When ≥4 badges exist, becomes a 4-column grid; until then, it's a small 1-2 card strip.

### C.2 Structure

```html
<section class="credentials" id="credentials">
  <div class="wrap">
    <div class="section-head">
      <span class="section-rule"></span>
      <p class="eyebrow">Credentials</p>
      <h2>Certified. Verified. Linked.</h2>
    </div>

    <div class="credentials-grid">
      <a class="credential" href="https://app-na2.hubspot.com/academy/achievements/fthvrd5w/en/1/ethan-glines/digital-marketing" target="_blank" rel="noopener">
        <div class="credential-mark">
          <span class="credential-mark-glyph">HS</span>
        </div>
        <div class="credential-body">
          <p class="credential-issuer">HubSpot Academy</p>
          <h3 class="credential-name">Digital Marketing</h3>
          <p class="credential-meta">
            <span class="credential-date">Earned 2026</span>
            <span class="credential-sep">·</span>
            <span class="credential-verify">Verify ↗</span>
          </p>
        </div>
      </a>
      <!-- Additional credentials append here -->
    </div>
  </div>
</section>
```

### C.3 CSS specs

- **Section background:** `var(--bg)` (cream), `border-top: 1px solid var(--hairline)`.
- **Grid:** `display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); gap: clamp(1rem, 2vw, 1.5rem);` At ≥720px, max 3-col cap via `repeat(auto-fill, minmax(300px, 0.33fr))` substitute if needed. For now (1-2 badges), they sit small-and-leftward — don't stretch to fill the row.
- **Card:** `display: flex; align-items: center; gap: 1.25rem; padding: 1.25rem 1.5rem; background: var(--surface); border: 1px solid var(--hairline); border-radius: 10px; max-width: 420px;`
- **Mark (left):** 56px × 56px square, `border-radius: 8px`, `background: var(--accent-soft)`, `border: 1px solid rgba(200,116,42,0.25)`. Houses the issuer's initials in Fraunces, weight 500, opsz 36, amber color, 1.25rem font-size. For HubSpot: "HS". Later for Google Analytics: "GA". Etc. **NOT issuer logos** — those become a maintenance nightmare and turn the section into a logo wall. Initials in our typography keep it cohesive with the Warm Editorial system.
- **Issuer name:** mono, 0.7rem, uppercase, letter-spacing 0.1em, neutral color
- **Credential name:** Fraunces, opsz 36, weight 500, 1.125rem, ink, line-height 1.2
- **Meta row:** mono, 0.7rem, neutral, uppercase letter-spacing 0.08em
- **`.credential-verify`:** changes to amber on hover (whole card link)

### C.4 Behavior

- **Hover:** Border shifts to `rgba(200,116,42,0.4)`, mark background deepens slightly (`background: rgba(200, 116, 42, 0.12)`). The verify arrow translates `2px, -2px`. Subtle Y-translate of `-2px`. 250ms ease-soft.
- **Click:** Opens verification URL in new tab.
- **Scroll reveal:** `.reveal` cascade with delays.

### C.5 Aesthetic intent (FEEL)

**Credential plate, not endorsement badge.** This is the visual cousin of a diploma name plate or a museum exhibit label — small, dignified, verifiable. The amber-tinted mark with typographic initials reads as "we made this part of the brand system, we did not staple a logo on." Reads as evidence, not decoration. NOT a LinkedIn skills wall, NOT a "Certified by…" badge dump.

### C.6 Copy guidance

- **Issuer:** Provider name only (HubSpot Academy / Google / Meta / Coursera). No marketing taglines.
- **Credential name:** Official cert title, max 4 words.
- **Date:** Year only ("Earned 2026"). No month — credentials don't expire publicly that way.
- **Verify:** Two-word phrase + arrow. The card itself is the link; "Verify ↗" is the affordance signal.

### C.7 Page-flow recommendation

**Between Capabilities and Resume.** Reasoning: Capabilities says "here's what I do." Credentials says "and here's third-party verification for one slice of that." Resume then says "here's the full record." That's the credibility staircase: claim → proof → record.

### C.8 Future scaling rule

When the section hits 4+ credentials, the layout shifts to a true 3-up or 4-up grid. Until then, badges sit at their natural width (max 420px each) flowed left-to-right. **Do not stretch a single badge across the full row** — that signals "we only have one" and reads as weakness. Single badge appears at its natural width, leaving empty space to the right that reads as "more coming."

---

## D. Elevator Pitch Module

### D.1 Placement — Between Hero and Bio

Position immediately after Hero, before Bio. Reasoning: the Hero says *who* Ethan is in one line. The Elevator Pitch says it in 60 seconds. The Bio then expands to full context. That's natural cinema — wide shot → medium shot → close-up.

This is the highest-prominence non-hero element on the page. Treat it accordingly.

### D.2 Layout — Two-format coexistence (audio + script)

Side-by-side at desktop: **left column (45%)** the audio player; **right column (55%)** the written script. Mobile: audio on top, script below. Both formats coexist — neither replaces the other. Visitors who want to listen, listen. Visitors who want to read, read.

```
┌─ ELEVATOR PITCH ─────────────────────────────────────────────┐
│  EYEBROW: Elevator Pitch                                      │
│  ━━━━                                                         │
│  H2: Sixty seconds.                                           │
│                                                               │
│  ┌──────────────────────┐  ┌──────────────────────────────┐  │
│  │                      │  │  "I'm Ethan Glines, founder  │  │
│  │   [ ▶ ]  amber       │  │   of Blue Luna. I help…"     │  │
│  │   round play         │  │                              │  │
│  │   button             │  │  [2nd paragraph if needed]   │  │
│  │                      │  │                              │  │
│  │   ━━━━━━━░░░░ 0:42  │  │  — Ethan                     │  │
│  │   waveform progress  │  │                              │  │
│  └──────────────────────┘  └──────────────────────────────┘  │
└──────────────────────────────────────────────────────────────┘
```

### D.3 Structure

```html
<section class="elevator-pitch" id="pitch">
  <div class="wrap">
    <div class="section-head reveal">
      <span class="section-rule"></span>
      <p class="eyebrow">Elevator Pitch</p>
      <h2>Sixty seconds.</h2>
    </div>

    <div class="pitch-grid">
      <!-- Left: Custom audio player -->
      <div class="pitch-player reveal" data-delay="1">
        <audio id="pitchAudio" preload="metadata" src="assets/elevator-pitch.mp3"></audio>

        <button class="pitch-play" id="pitchPlayBtn" aria-label="Play elevator pitch" aria-pressed="false">
          <svg class="pitch-play-icon-play" viewBox="0 0 24 24" aria-hidden="true">
            <path d="M5 3.5v17a1 1 0 0 0 1.55.83l13-8.5a1 1 0 0 0 0-1.66l-13-8.5A1 1 0 0 0 5 3.5z"/>
          </svg>
          <svg class="pitch-play-icon-pause" viewBox="0 0 24 24" aria-hidden="true">
            <rect x="6" y="4" width="4" height="16" rx="1"/>
            <rect x="14" y="4" width="4" height="16" rx="1"/>
          </svg>
        </button>

        <div class="pitch-meter">
          <div class="pitch-waveform" aria-hidden="true">
            <!-- 32 bars rendered as <span>s of varying static heights -->
          </div>
          <div class="pitch-progress" id="pitchProgress" role="progressbar" aria-label="Audio progress" aria-valuemin="0" aria-valuemax="100" aria-valuenow="0">
            <div class="pitch-progress-fill" id="pitchProgressFill"></div>
          </div>
          <div class="pitch-time">
            <span id="pitchCurrent">0:00</span>
            <span class="pitch-time-sep">/</span>
            <span id="pitchDuration">1:00</span>
          </div>
        </div>
      </div>

      <!-- Right: Written script -->
      <div class="pitch-script reveal" data-delay="2">
        <p class="pitch-script-label">Or read it:</p>
        <blockquote class="pitch-script-quote">
          <p>I'm Ethan Glines…</p>
          <p>[2nd paragraph if needed]</p>
        </blockquote>
        <p class="pitch-script-attr">— Ethan</p>
      </div>
    </div>
  </div>
</section>
```

### D.4 CSS specs — The custom audio player

**Critical:** zero browser-default `<audio controls>`. The `<audio>` element is `display: none` (or absent visual). All UI is custom HTML controlled by JS.

- **Section padding:** existing `--section-pad`
- **Background:** `var(--bg)` (cream) — same as hero, signals continuation
- **Grid:** `grid-template-columns: minmax(0, 0.85fr) minmax(0, 1fr); gap: clamp(2rem, 5vw, 4rem);` Mobile: 1 col, `gap: 2.5rem`.
- **Player wrapper (`.pitch-player`):** `background: var(--surface); border: 1px solid var(--hairline); border-radius: 14px; padding: clamp(1.75rem, 2.5vw, 2.5rem); display: flex; align-items: center; gap: clamp(1.25rem, 2vw, 2rem);`
- **Play button (`.pitch-play`):**
  - `width: 84px; height: 84px; border-radius: 50%; background: var(--accent); flex-shrink: 0;`
  - `box-shadow: 0 6px 24px -6px rgba(200, 116, 42, 0.45);`
  - SVG icon (play triangle) 28×28, white fill, optical-centered (margin-left 4px on play; pause is symmetric)
  - Hover: `background: var(--accent-deep); transform: scale(1.04); box-shadow: 0 10px 32px -6px rgba(200, 116, 42, 0.55);` 250ms ease-out
  - Focus-visible: 3px outline accent + 3px offset
  - When playing, swap visible SVG (toggle `.is-playing` class on button — CSS `.is-playing .pitch-play-icon-play { display: none; } .is-playing .pitch-play-icon-pause { display: block; }`)
  - **Pulsing ring while playing:** when `.is-playing`, an `::after` pseudo-element pulses outward (60% → 110% scale, 1 → 0 opacity over 1.4s, infinite). Same family as the bio-currently dot — visual signature carryover.
- **Meter column (`.pitch-meter`):**
  - `flex: 1; min-width: 0; display: flex; flex-direction: column; gap: 0.75rem;`
- **Waveform (`.pitch-waveform`):**
  - 32 static `<span>` bars in a flex row, `gap: 3px; align-items: center; height: 36px;`
  - Each bar 4px wide, `background: var(--neutral-mid)`, `border-radius: 2px`
  - Heights vary: programmatic pattern (e.g., heights array of 32 values between 8-32px to simulate audio waveform).
  - Bars currently played get amber via JS: when `currentTime / duration > bar.index / 32`, class `.is-active` → `background: var(--accent)`
- **Progress bar (`.pitch-progress`):** Below waveform. Thin (3px tall) `background: var(--hairline); border-radius: 1.5px;` `.pitch-progress-fill` is the amber fill, width controlled by JS from 0 to 100%. Click anywhere on the progress bar to seek. (Keyboard accessibility: arrow left/right when focused = ±5s; space = play/pause.)
- **Time display (`.pitch-time`):** mono, 0.75rem, uppercase letter-spacing 0.08em, neutral color. `.pitch-time-sep` is amber.
- **Script side (`.pitch-script`):**
  - `pitch-script-label`: mono, 0.72rem, uppercase, accent color, margin-bottom 0.75rem — small intro "Or read it:"
  - `pitch-script-quote`: Fraunces, opsz 72, SOFT 100, weight 400, italic, `font-size: clamp(1.25rem, 1.6vw, 1.5rem); line-height: 1.5;` ink color, `border-left: 2px solid var(--accent); padding-left: 1.5rem; margin: 0;`
  - `pitch-script-attr`: mono, 0.72rem, uppercase, neutral color, margin-top 1rem

### D.5 Behavior — JS spec

**Required events:**
1. `<audio>` element with preload="metadata" — captures duration on load
2. On `loadedmetadata`: populate `#pitchDuration` formatted as `M:SS`
3. Play button click: toggle play/pause, swap icon, toggle `.is-playing` class on button
4. On `timeupdate`: update `#pitchCurrent`, set `.pitch-progress-fill` width, toggle `.is-active` on waveform bars whose index ≤ `(currentTime/duration) * 32`
5. On `ended`: reset to start, remove `.is-playing` class
6. Click on `.pitch-progress`: calculate click position as percentage, seek audio
7. Keyboard support on play button: space = toggle play; arrow left = -5s; arrow right = +5s
8. `aria-pressed` toggles on play button; `aria-valuenow` updates on progress bar
9. **Reduced motion:** disable the pulsing ring on play button (the `.is-playing::after` animation). Audio playback still works.

### D.6 Aesthetic intent (FEEL)

**Intentional play button, not stock media control.** The amber play button is editorial — it looks like a curated affordance, not the default HTML5 `<audio>` widget. The waveform is decorative-but-functional — bars that fill amber as the audio plays. Reads as "this is something Ethan made for you to listen to," not "here's a YouTube embed I dropped on the page." The script alongside the audio respects readers who skim — both formats coexist with equal dignity.

### D.7 Copy guidance

- **Audio length target:** 45-60 seconds. Anything over 90 seconds and people abandon.
- **Script:** Reed drafts. Target 90-130 words written (60s spoken). Format as 1-2 short paragraphs.
- **Script label:** "Or read it:" or "Prefer to read?" — quiet, conversational.
- **H2:** "Sixty seconds." (with period — declarative, confident). Alternates: "The pitch." / "Here's the pitch." / "60 seconds, on me."

### D.8 Page-flow recommendation

**Between Hero and Bio.** This is the prime real estate slot — it's the highest-prominence non-hero element. Putting the pitch here turns the page into a 3-act sequence: Hero (identity) → Pitch (positioning) → Bio (proof). Recruiters who don't scroll past the fold get the hero. Recruiters who give one more scroll get the pitch. Everyone else continues into Bio.

---

## Cross-archetype consistency rules

1. **Eyebrow + section-rule combo** opens every new section — `.section-rule` (56px × 2px amber bar) sits above `.eyebrow` (mono uppercase 0.75rem neutral).
2. **Hand-drawn underline appears in at least one place per section:** Case Studies (in pull quote), Field Notes (in section H2 + select card titles), Credentials (in section H2 only — "Verified" or "Linked"), Elevator Pitch (in script quote — underline "delivered" or "operator").
3. **All hover transitions:** 250-350ms `var(--ease-out)` or `var(--ease-soft)` — no faster, no slower.
4. **Card hover pattern:** border shifts to `rgba(200, 116, 42, 0.35-0.4)`, optional Y-translate of -2 to -3px, optional top-rule `::before` scaleX(0→1). Never all three on the same card — pick two.
5. **Reduced motion:** every animation respects `prefers-reduced-motion: reduce`. The existing block at line 1467 already covers most of this; new animations (audio pulse ring, waveform fill) need explicit reduced-motion overrides.
6. **All external links:** `target="_blank" rel="noopener noreferrer"` and a trailing arrow glyph (→ or ↗).
7. **Mono micro-labels (eyebrows, dates, meta strips) stay at 0.7-0.75rem with letter-spacing 0.08-0.14em.** Don't go smaller — accessibility floor.

---

## Build order recommendation (for Kit)

1. **A. Case Studies** first — highest content priority, replaces existing section in place. Test that Travel With Glines card retention reads correctly below the two case studies before shipping.
2. **D. Elevator Pitch** second — high prominence, requires custom audio player JS that needs standalone testing. Prototype the player in isolation first (per the 2026-05-21 prototype-first rule). Audio asset (`assets/elevator-pitch.mp3`) needs to exist before integration testing.
3. **B. Field Notes** third — content is ready (Reed/Scout extracted), grid is conventional, primarily a CSS exercise.
4. **C. Credentials** last — smallest section, lowest content urgency, easy to ship once the others are stable.

---

## Open questions for Ethan

1. **Case Studies:** Confirm replacing "Selected Work" with the case study format is the call. Alternative: keep "Selected Work" as the section name and put case studies inside it as upgraded cards.
2. **Field Notes naming:** "Field Notes" vs. "Reflections" vs. "Notes" vs. "Marginalia." Recommend "Field Notes."
3. **Field Notes — Post 3:** Reed/Scout flagged that the LinkedIn extract for Post 3 returned a paraphrase, not verbatim text. You'll need to paste the full original post text before we ship.
4. **Field Notes — Post 4 media:** Likely had Japan photos originally. Pull from your LinkedIn feed and supply file paths (or skip — the card design handles "no media" gracefully).
5. **Field Notes — strip hashtags:** Recommend removing `#byuh #marketing` etc. from card bodies. Confirm.
6. **Elevator Pitch — audio:** Do we have `elevator-pitch.mp3` recorded? If not, the section can be built with the script-only version first, audio added later.
7. **Elevator Pitch — script:** Reed needs to draft. Estimate 90-130 words. Should it open with "I'm Ethan Glines, founder of Blue Luna…" or different?
8. **Credentials:** Initials-in-mark approach ("HS" for HubSpot) vs. actual provider logo. Recommend initials. Confirm.
9. **Nav update:** Adding `Pitch` and `Field Notes` to primary nav — confirm. Alternative: skip `Pitch` in nav (it's right after hero, hard to miss).

---

*End of spec v1.*
