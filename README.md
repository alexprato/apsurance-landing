# Handoff: APsurance Landing Page

## Overview
A high-converting marketing landing page for **APsurance**, an independent insurance agency that helps U.S. consumers check eligibility for low-cost Health Insurance Marketplace coverage and book a quick consult with a licensed agent. The page captures qualified leads via an inline form (name, phone, state, household size, income range, callback time) and routes them to a licensed agent for follow-up.

**Primary CTA:** "Check My Options" (form submit)
**Secondary CTA:** "Schedule a 5-Minute Call" (phone)

## About the Design Files
The file in this bundle (`Landing Page.html`) is a **design reference** built in plain HTML/CSS/vanilla-JS — it is a prototype showing intended look, copy, and behavior, **not** production code to ship as-is. The task is to **recreate this design in the target codebase's environment** (likely Next.js / React + Tailwind for a marketing site of this kind, or whatever the team is standardized on) using the team's existing component library, form-handling conventions, and CMS/copy pipeline.

If no codebase exists yet, recommended stack:
- **Next.js 14 (App Router)** + **TypeScript** for SEO + fast TTFB on a lead-capture page
- **Tailwind CSS** for styling (tokens map cleanly — see Design Tokens below)
- **react-hook-form** + **zod** for form validation
- **shadcn/ui** primitives for inputs/select/dialog if needed
- A backend route (e.g. `/api/leads`) that forwards to the **APCC backend** (see "Form Backend Integration" below)

## Fidelity
**High-fidelity (hi-fi).** Final colors, typography, spacing, copy, animations, and interaction states are all production-intent. Recreate pixel-perfectly. The Tweaks panel in the prototype (`#tw-panel`) is a **design tool only** — do NOT ship it.

## Brand & Aesthetic Direction
- Clean, trustworthy, modern, professional insurance brand
- Black / gold / blue palette
- Generous whitespace, confident typography, conversion-focused
- Mobile-first responsive
- No emoji, no AI-tropes (no em dashes used in copy — replaced with commas)

---

## Design Tokens

### Colors (CSS custom properties)
```css
--ink:       #0A1628;  /* primary near-black, headings, dark surfaces */
--ink-2:     #142844;  /* hover for ink */
--ink-soft:  #2C3E5C;  /* secondary text */
--paper:     #FAF8F4;  /* page background, warm off-white */
--paper-2:   #F2EEE5;  /* secondary surface (CTA band, strip) */
--line:      #E6E0D2;  /* hairline borders */
--gold:      #C8A24B;  /* primary accent, CTA */
--gold-deep: #A7842F;  /* gold hover */
--gold-soft: #F1E6C5;  /* gold tint backgrounds */
--blue:      #1E5BA8;  /* trust blue, italic accents, link */
--blue-deep: #154382;  /* blue hover */
--blue-soft: #DCE8F7;  /* blue tint */
--green:     #2E7D5B;  /* success */
--danger:    #B23A3A;  /* form errors */
```

### Shadows
```css
--shadow-sm: 0 1px 2px rgba(10,22,40,0.06), 0 1px 1px rgba(10,22,40,0.04);
--shadow-md: 0 6px 24px -8px rgba(10,22,40,0.18), 0 2px 6px rgba(10,22,40,0.06);
--shadow-lg: 0 24px 60px -20px rgba(10,22,40,0.32), 0 8px 20px -10px rgba(10,22,40,0.18);
```

### Typography
- **Display / headings:** `Inter Tight` (Google Fonts), weights 400/500/600/700/800, `letter-spacing: -0.02em`, `line-height: 1.1`, `text-wrap: balance`
- **Body:** `Inter` (Google Fonts), weights 400/500/600/700, `font-size: 16px`, `line-height: 1.55`, `text-wrap: pretty`
- **Mono accent (rarely used):** `JetBrains Mono`
- Italic accent words in headlines use `font-style: italic` on Inter Tight (acts as serif-italic accent)

Google Fonts URL:
```
https://fonts.googleapis.com/css2?family=Inter+Tight:wght@400;500;600;700;800&family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap
```

### Type scale
| Element | Size | Weight | Notes |
|---|---|---|---|
| H1 hero | `clamp(40px, 5.2vw, 64px)` | 700 | balance |
| H2 section | `clamp(32px, 4vw, 44px)` | 700 | |
| H2 explainer | `clamp(28px, 3.5vw, 38px)` | 700 | on dark |
| H3 card | 17–22px | 600–700 | |
| Eyebrow | 12px | 600 | uppercase, `letter-spacing: 0.06–0.08em` |
| Body lg | 18px | 400 | hero sub |
| Body | 15–16px | 400 | |
| Body sm | 13–14px | 400 | |
| Caption | 11–12px | 500–600 | |

### Spacing
- Container: `max-width: 1200px; padding: 0 24px;`
- Section vertical padding: `96px` standard, `64px` tight
- Card padding: 20–32px
- Form field padding: `12px 14px`
- Gap scale used: 6, 8, 10, 12, 16, 20, 24, 32, 48, 56, 64

### Border radius
- Pills: `999px` (eyebrow, phone CTA)
- Cards/forms: `16–20px`
- Inputs/buttons: `10px`
- Inner chips: `8px`
- Logo mark: `8px`

### Responsive breakpoints
- `@media (max-width: 960px)`: hero stacks; nav links hide; benefits → 2-col; trust/cta → 1-col; FAQ stacks; footer → 2-col
- `@media (max-width: 560px)`: form rows → 1-col; callback chips → 2-col; benefits → 1-col; footer → 1-col

---

## Page Sections (top to bottom)

### 1. Top bar (`.topbar`)
- Background: `--ink`, text `--paper`, 13px
- Left: gold pulse dot + "**Open Enrollment** assistance available, licensed agents standing by"
- Right: "Mon–Fri 8a–8p ET" | "Sat 9a–4p ET"
- Pulsing gold dot animation: 7px circle, `animation: pulse 2s infinite` (box-shadow expands and fades)

### 2. Sticky nav (`nav.nav`)
- `position: sticky; top: 0;` with `backdrop-filter: blur(12px)`, paper background at 92% alpha
- Logo: 32px black square mark with gold "A" + inner gold-stroked square; wordmark "APsurance." with gold dot
- Links: How it works, Coverage, Why us, FAQ
- Right CTA: pill phone button "(954) 999-4342" — ink bg, gold phone icon
- Hides nav-links under 960px

### 3. Hero (`.hero`)
- Two-column grid `1.05fr 0.95fr` with 64px gap
- Background gradient overlays (gold + blue radials at low opacity)
- **Left column:**
  - Eyebrow pill: "★ Licensed Marketplace help · No cost to you" (gold-soft bg)
  - H1: "Find out if you may qualify for **low-cost** *health insurance*"
    - "low-cost" gets a gold highlighter underline (`linear-gradient(180deg, transparent 65%, var(--gold-soft) 65%)`)
    - "health insurance" italic in `--blue`
  - Sub: "Take 60 seconds to check your options through the Health Insurance Marketplace. A licensed agent will walk you through plans you may be eligible for, at zero cost to you."
  - 3 bullets with gold check-circle icons:
    1. Plans may include **$0 monthly premiums** for those who qualify based on income
    2. Compare medical, dental, vision, life, and Medicare options in one call
    3. Speak with a real licensed agent, no robocalls, no spam, no pressure
  - Trust row: 4 stacked avatars (initials JM/RT/DK/+) + 5 gold stars + "Trusted by families across the U.S."
- **Right column:** Lead form card (see Form section)

### 4. Lead form card (`.form-card` / `#lead-form`)
See **Form Fields & Validation** section below.

### 5. Carrier strip (`.strip`)
- Paper-2 bg, hairline borders top/bottom
- Label: "HELPING ENROLL IN PLANS FROM MAJOR CARRIERS"
- Items (text only — replace with real logo SVGs in production): Aetna, BCBS, Cigna, Humana, UnitedHealth, Oscar
- *Note: Verify carrier permission before showing logos. Text wordmarks shown in the prototype as placeholders.*

### 6. Marketplace explainer (`.explainer`, id `#how`)
- Dark `--ink` rounded card (24px radius), 56px padding, two-column
- Decorative gold radial glow top-right
- Left: gold eyebrow "What is Marketplace coverage?" + H2 "Quality health coverage, often at a fraction of the **sticker price.**" + 2 paragraphs
- Right: 2x2 stat grid
  - "4 of 5" — Marketplace enrollees may find a plan for $10 or less per month after subsidies\*
  - "$705" — Average annual premium savings reported by subsidy-eligible enrollees\*
  - "60s" (full-width gold-tinted) — Average time to complete our quick eligibility check
- Stats are **illustrative**, attributed to CMS public reports; verify with legal before publish.

### 7. Benefits grid (`.benefits-grid`, id `#benefits`)
- Eyebrow "What's covered" + H2 "More than just *medical.*"
- 5 cards (1 featured dark + 4 light), each with 44px rounded icon tile
- **Health** (featured/dark with gold "CORE" tag): heart icon
- **Dental**: shield icon
- **Vision**: eye icon
- **Life**: pulse line icon
- **Medicare**: briefcase + plus icon
- Hover: lift -3px + ink border + shadow-md

### 8. Trust section (`.trust-grid`, id `#trust`)
- 3 cards, each with 48px rounded blue-soft badge tile (24px stroked icon)
- **Licensed insurance professionals** — shield+check icon
- **Privacy-focused, no spam** — lock icon
- **5-minute call, zero pressure** — clock icon

### 9. CTA band (`.cta-band`)
- paper-2 bg, hairline top/bottom
- Centered eyebrow + H2 "Two ways to get started." + subtitle
- Two paired cards:
  - **Light card #1:** "Check my options online" → outline button "Check My Options" (anchors to `#lead-form-card`)
  - **Dark card #2:** "Schedule a 5-minute call" → gold button "Schedule a 5-Minute Call" (`tel:9549994342`)
- Numbered with 32px gold circle (1, 2)

### 10. FAQ (`.faq-grid`, id `#faq`)
- Two-column: 380px sticky sidebar + accordion list
- Sidebar: paper-2 card, sticky `top: 96px`, contact phone + email
- 6 FAQ items (single-open accordion, click toggles, first item open by default):
  1. Is this really free, or are there hidden fees?
  2. How do I know if I qualify for low-cost coverage?
  3. Will I be flooded with marketing calls?
  4. What if I already have a plan through my employer?
  5. Can I enroll outside Open Enrollment?
  6. What information do I need to provide on the call?
- Toggle icon: 32px circle border, "+" → rotates 45° to "×" when open. Filled ink/gold when open.
- Animation: `max-height: 0` → `400px` with `transition: max-height 0.3s`

Full FAQ copy is in the source HTML — copy verbatim.

### 11. Footer (`footer.footer`)
- `--ink` bg, 64px top / 28px bottom
- 4 columns: brand+blurb / Coverage links / Company links / Get in touch
- Coverage links: Health insurance, Dental, Vision, Life insurance, Medicare help
- Company links: How it works, Why APsurance, FAQ, Privacy Policy, Terms of Service
- Contact: phone (954) 999-4342, email APsurance@outlook.com, web APsurance.com (each with gold icon)
- **Legal disclaimer block** (gold-labeled "Disclaimer"): independent agency, no promise of free insurance, no guarantee of eligibility, not affiliated with the U.S. government or Medicare, statistics illustrative. **Required — do not omit.**
- Bottom row: "© 2026 APsurance. All rights reserved." + Privacy / Terms / Accessibility / Licenses

---

## Form Fields & Validation

### Schema (suggest zod)
```ts
const LeadSchema = z.object({
  name: z.string().min(2, "Please enter your name"),
  phone: z.string()
    .transform(v => v.replace(/\D/g, ''))
    .refine(v => v.length === 10, "Enter a valid 10-digit phone"),
  state: z.enum([/* 50 US states, see HTML for list */]),
  household: z.enum(["1 person","2 people","3 people","4 people","5+ people"]),
  income: z.enum([
    "Under $20,000",
    "$20,000 – $35,000",
    "$35,000 – $50,000",
    "$50,000 – $75,000",
    "$75,000 – $100,000",
    "Over $100,000"
  ]),
  callback_time: z.enum(["ASAP","Morning","Afternoon","Evening","No preference"]).default("No preference"),
  // optional UTM/source fields (recommended)
  utm_source: z.string().optional(),
  utm_medium: z.string().optional(),
  utm_campaign: z.string().optional(),
  page_url: z.string().url().optional(),
  user_agent: z.string().optional(),
  submitted_at: z.string().datetime().optional(),
});
```

### Required fields (in form order)
| Field | Type | Required | Notes |
|---|---|---|---|
| Full name | text | yes | min 2 chars |
| Phone | tel | yes | auto-format to `(XXX) XXX-XXXX`; strip non-digits before submit; require 10 digits |
| State | select | yes | 50 US states (full list in HTML) |
| Household size | select | yes | 1 / 2 / 3 / 4 / 5+ people |
| Annual income | select | yes | 6 ranges as above |
| Preferred callback time | chip group | optional | ASAP / Morning / Afternoon / Evening — single select; defaults to "No preference" if none picked |

### Validation behavior
- **On submit:** validate all required; add `.has-error` class to wrapper + `.error` to input; show inline error message in `.err-msg` (currently hidden via `display: none`).
- **On input/change:** clear errors immediately as user types.
- **Phone formatting:** live-format on each keystroke. Strip non-digits, format progressively: `(XXX`, `(XXX) XXX`, `(XXX) XXX-XXXX`. Cap at 10 digits.
- **Empty submit:** show all errors, do not submit.
- **Success:** replace form contents with confirmation card showing:
  - Gold ring success checkmark
  - "Thanks, [first name], we got it."
  - Subtitle: "A licensed APsurance agent will reach out at the time you preferred. No spam, no pressure."
  - Summary table: Phone / State / Household / Income / Callback
  - Fallback CTA: "Need help sooner? Call (954) 999-4342"
  - Smooth-scroll to confirmation
- **HTML escape** all user-supplied values when echoing in success state (prototype includes `escapeHtml()` helper).

### Callback time chip behavior
- Buttons inside `.callback-times`. Click sets `.active` (single-select), writes value to hidden `input[name="callback_time"]`. Active state = ink bg, paper text.

### Disclaimer copy under submit (required)
> By submitting, you agree a licensed agent may contact you about coverage options. We respect your privacy, see our [Privacy Policy](/privacy). No spam, ever.

---

## Form Backend Integration (APCC)

The prototype short-circuits to a local success state. Production wiring:

### Recommended client flow
```ts
// On valid submit:
const res = await fetch('/api/leads', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify(leadPayload),
});
if (!res.ok) {
  // show inline error + fallback phone CTA
} else {
  // render success state
  // fire conversion analytics (GA4 'generate_lead', Meta 'Lead', etc.)
}
```

### Recommended Next.js API route (`/app/api/leads/route.ts`)
```ts
import { NextResponse } from 'next/server';
import { LeadSchema } from '@/lib/schemas';

export async function POST(req: Request) {
  const body = await req.json();
  const parsed = LeadSchema.safeParse(body);
  if (!parsed.success) {
    return NextResponse.json({ error: parsed.error.flatten() }, { status: 400 });
  }

  // Server-side enrich
  const payload = {
    ...parsed.data,
    ip: req.headers.get('x-forwarded-for') ?? '',
    user_agent: req.headers.get('user-agent') ?? '',
    submitted_at: new Date().toISOString(),
  };

  // ===== APCC backend handoff =====
  // Replace URL + auth scheme with whatever APCC exposes:
  const apccRes = await fetch(process.env.APCC_LEADS_ENDPOINT!, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${process.env.APCC_API_KEY}`,
      // or 'X-API-Key': ..., per APCC docs
    },
    body: JSON.stringify({
      // Map to APCC lead schema. Confirm field names with APCC team.
      first_name: payload.name.split(' ')[0],
      last_name: payload.name.split(' ').slice(1).join(' ') || null,
      phone: payload.phone,
      state: payload.state,
      household_size: payload.household,
      income_range: payload.income,
      preferred_callback: payload.callback_time,
      source: 'apsurance_landing',
      utm: {
        source: payload.utm_source,
        medium: payload.utm_medium,
        campaign: payload.utm_campaign,
      },
      meta: {
        page_url: payload.page_url,
        ip: payload.ip,
        user_agent: payload.user_agent,
        submitted_at: payload.submitted_at,
      },
    }),
  });

  if (!apccRes.ok) {
    // Log to Sentry / observability — do NOT expose APCC error to user
    console.error('APCC ingest failed', await apccRes.text());
    // Optional fallback: write to a queue (SQS, Inngest, Upstash Q) for retry
    return NextResponse.json({ error: 'Server error, please call us' }, { status: 502 });
  }

  return NextResponse.json({ ok: true }, { status: 200 });
}
```

### APCC integration TODOs (confirm with APCC team)
1. **Endpoint URL** — production + staging
2. **Auth method** — Bearer token, API key header, OAuth, signed JWT?
3. **Field mapping** — exact field names APCC expects (the mapping above is a starting point)
4. **Required vs optional fields** on their side
5. **Idempotency key** — pass a UUID so retries don't dupe leads
6. **Lead routing logic** — how does APCC assign to a licensed agent by state license? Do we need to send licensed-state info?
7. **Compliance fields** — TCPA consent timestamp, IP, page URL captured for record (already in payload above)
8. **Webhook back to us** — when an agent picks up the lead, do we get a callback to update analytics?

### Compliance / TCPA
- The disclaimer text under the submit button is the consent disclosure. Capture and persist `submitted_at`, `ip`, `user_agent`, `page_url` alongside the lead — this is the audit trail for TCPA.
- Do **not** auto-dial without an explicit consent checkbox if your legal team requires it. Add `<input type="checkbox" required>` with TCPA consent language if APsurance's compliance counsel asks.

### Analytics events to fire
- `form_view` on hero render
- `form_field_focus` (first interaction)
- `form_submit_attempt`
- `form_submit_success` → also fire GA4 `generate_lead`, Meta Pixel `Lead`, optional Google Ads conversion
- `form_submit_error` with reason
- `cta_click` for both CTAs in section #9 and the phone button in nav

---

## Interactions Summary

| Interaction | Behavior |
|---|---|
| Sticky nav | `position: sticky; top: 0`, blurred bg |
| Phone button hover | `--ink-2` bg |
| Primary buttons hover | `translateY(-1px)` + larger shadow |
| Gold button hover | `--gold-deep` bg + paper text |
| Outline button hover | inverts to ink fill |
| Benefit card hover | lift -3px, ink border, `--shadow-md` |
| FAQ item | accordion: only one open at a time; first open by default; "+" rotates 45° |
| Time chip | single-select toggle |
| Phone input | live `(XXX) XXX-XXXX` formatting |
| Form field error | red border + 3px red ring; cleared on input |
| Anchor links | smooth-scroll (use `behavior: 'smooth'` — but prefer CSS `scroll-behavior: smooth` on `html`) |
| Success state | replaces form content, smooth-scroll into view |
| Pulse dot | 2s infinite box-shadow expand+fade |

---

## Copy / Text (verbatim, all in `Landing Page.html`)

All marketing copy is in the HTML. Key strings to extract for i18n / CMS:
- All H1/H2/H3 headings
- All `<p>` body copy
- All FAQ Q&A pairs
- All CTA button labels: "Check My Options", "Schedule a 5-Minute Call", "(954) 999-4342"
- Footer disclaimer block (legally required, do not edit without legal review)
- Form field labels, placeholders, error messages, disclaimer

Brand voice: clear, plain-English, no marketing jargon, "may qualify" / "check options" language throughout. **Never** say "free insurance" or "guaranteed eligibility."

---

## Assets

The prototype contains **no external images**. All iconography is inline SVG (Lucide-style stroke icons at 1.5–2.5 stroke width). For production:

- **Logo:** Replace text wordmark with a real logo SVG. Current placeholder is the letter "A" in a 32px ink-filled rounded square with an inner gold-stroked frame.
- **Carrier logos:** Replace text with permission-cleared carrier logo SVGs (Aetna, BCBS, Cigna, Humana, UnitedHealth, Oscar).
- **Favicon / OG image:** Need to be designed.
- **Avatar testimonial images:** Currently initial-circles. Either keep as-is or swap for licensed customer photos (with consent + photo release).
- **Icons:** Recommend [lucide-react](https://lucide.dev) — every icon in the design has a Lucide equivalent (heart, shield, eye, activity, briefcase, shield-check, lock, clock, plus, arrow-right, phone, mail, globe, check, x).

---

## Accessibility Checklist

- [ ] Color contrast: ink on paper passes AAA; gold on ink passes AA large; verify gold-on-paper for body text — **avoid gold for body text** (only use for accents/icons).
- [ ] Form labels are visible (not just placeholders) — already done.
- [ ] Required fields announced via `aria-required="true"`.
- [ ] Errors announced via `aria-invalid` + `aria-describedby` pointing to `.err-msg`.
- [ ] FAQ accordion uses `<button aria-expanded>` + `aria-controls`. Currently uses `<button>` but `aria-expanded` should be added in production.
- [ ] Time chip group: use `role="radiogroup"` with `role="radio"` and `aria-checked`, or convert to native `<input type="radio">` visually styled.
- [ ] Skip-to-content link in nav.
- [ ] Focus-visible rings on all interactive elements (currently inputs have a focus ring; add to buttons).
- [ ] `prefers-reduced-motion`: disable pulse animation and CTA transforms.
- [ ] `<html lang="en">` ✓ already set.

---

## SEO / Meta (add for production)

```html
<meta name="description" content="See if you may qualify for low-cost Marketplace health insurance. Compare medical, dental, vision, life, and Medicare plans with a licensed agent — at no cost to you.">
<meta property="og:title" content="APsurance | Find out if you may qualify for low-cost health insurance">
<meta property="og:description" content="...">
<meta property="og:image" content="/og.png">
<meta property="og:url" content="https://apsurance.com">
<meta name="twitter:card" content="summary_large_image">
<link rel="canonical" href="https://apsurance.com/">
```

LocalBusiness / InsuranceAgency JSON-LD recommended. Confirm NAP consistency (phone `(954) 999-4342`, email `APsurance@outlook.com`, web `APsurance.com`).

---

## Files in this Bundle

- `Landing Page.html` — full prototype, single-file (HTML + inline CSS + inline JS).
  - **Strip out the entire `#tw-panel` UI, all `.tw-*` CSS rules, the `TWEAK_DEFAULTS` block, and the `applyTweaks()/buildTweaksPanel()/setTweak()` JS** — those are dev-only design tools.
  - Keep everything else as a styling/copy reference.

## Suggested file layout (Next.js)
```
app/
  page.tsx                       # Landing
  api/leads/route.ts              # APCC handoff
  layout.tsx                      # Fonts (next/font for Inter + Inter Tight)
  globals.css                     # Tailwind + token CSS vars
components/
  marketing/
    TopBar.tsx
    Nav.tsx
    Hero.tsx
    LeadForm.tsx                  # react-hook-form + zod
    CarrierStrip.tsx
    MarketplaceExplainer.tsx
    BenefitsGrid.tsx
    TrustGrid.tsx
    CtaBand.tsx
    FAQ.tsx
    Footer.tsx
lib/
  schemas.ts                      # LeadSchema (zod)
  apcc.ts                         # APCC client wrapper
  analytics.ts                    # GA4/Meta event helpers
```

## Open questions for the APsurance team
1. APCC backend endpoint, auth, and field mapping
2. TCPA consent — explicit checkbox or implicit via disclaimer text? (legal call)
3. State licensing — do we filter the State dropdown to states APsurance is licensed in, or accept all and route?
4. Carrier logo permission for the strip
5. Real testimonial avatars/quotes if we want to keep that trust row
6. CMS or hardcoded copy? (FAQ + disclaimers tend to need legal-reviewed updates)
7. Phone number — is `(954) 999-4342` the live ring-pool, or do we need dynamic number insertion (CallRail etc.) for source attribution?
