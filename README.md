# MHO: Mobile Health Outreach

Standalone site for Health Matters Clinic's Mobile Health Outreach program, built
on the same design system and animation layer as TEAMHMC/SMO and Unstoppable so
behaviour is identical across HMC surfaces.

Live target: https://mho.healthmatters.clinic (GitHub Pages, see CNAME)

## Structure

    index.html                         the page
    assets/css/hmc-parallax.css        shared parallax + reveal layer
    assets/js/vendor/                  GSAP, ScrollTrigger, Lenis (vendored, not CDN)
    assets/js/hmc-immersive.js         scroll layer: reveals, count-ups, parallax
    assets/js/hmc-parallax.js          lightweight layer: kinetic marquee
    assets/site/hmc-buttons-1.0.3.*    shared HMC button system
    photos/                            program photography

`assets/` is copied verbatim from SMO. Do not fork it here. If the shared layer
changes, copy the whole folder across again so the two sites stay in step.

## Deploy

GitHub Actions, same workflow as SMO and Unstoppable: `.github/workflows/deploy.yml`
uploads the repo root as the Pages artifact on every push to main. Do not switch to
"deploy from a branch"; every other HMC site uses Actions and this matches.

DNS: `mho` CNAME to `teamhmc.github.io`, set to **DNS only** in Cloudflare (grey
cloud), matching `smo` and `unstoppable`. Cloudflare will warn that this exposes the
origin IP. That IP is GitHub's shared infrastructure, not an HMC server, so the
warning does not apply. Proxying through the orange cloud commonly breaks Pages TLS
issuance.

## Framing rule, read before editing copy

The numbers on this page come from a **community needs and engagement assessment**
completed by 169 people. It is community feedback collected for program planning.

It is not research, it carries no IRB determination, and none of SMO's ethics
language may be copied onto this page. The words *research*, *study*, *participants*
and *IRB* are deliberately absent from `index.html`. Keep them out.

## The figures used, and where

Counts are exact. Percentages are of the people who answered each question, which is
why every figure on the page is shown with its count. n = 169 total respondents.

| Figure | Section |
| --- | --- |
| 169 respondents; 87 cost; 133 want updates | Hero stat row |
| Cost 87 (56.1%), time 60 (38.7%), transportation 59 (38.1%) | What the community told us |
| Free or low-cost service info 104 (68.4%); help accessing services 86 (56.6%) | What the community told us |
| Attended for: giveaways 129 (77.7%), food 90 (54.2%), child or family activities 89 (53.6%), screenings 79 (47.6%), resources or referrals 73 (44.0%) | How that shapes deployment |
| Would attend for: free items 91 (59.1%), child or family activities 89 (57.8%), food 84 (54.6%) | How that shapes deployment |
| Phone or text 61 (37.9%); in person 51 (31.7%); digital tool very likely 114 (75.5%), somewhat likely 29 (19.2%); want updates 133 (84.7%) | How people want to hear from us |
| Among the 61 preferring phone or text: services 32, access help 30, education 19, children and youth 17, updates 10, mental health 8 | How people want to hear from us |

Bar widths in the two ranked panels use the published percentage. In the phone and
text panel the bars are the count as a share of 61, because no percentage was
published for that breakdown and none was invented.

Nothing else on the page is a statistic. There are no quotes, no partner names, no
outcome claims, and no count of people served, because none of those are sourced.

## Animation hooks

Driven by `hmc-immersive.js`, unmodified:

- `[data-reveal]` scroll reveal
- `.impact-num` count-up. Only matches `^\d+%?$`, so decimals are split: the integer
  animates and the decimal tail sits in a sibling span
- `.hero-slide` hero carousel, 4 slides on a 5500ms cycle with Ken Burns
- `.hero-grain` SVG turbulence overlay at .055 opacity
- `.hmc-kinetic-row` marquee

The immersive layer disables itself under `prefers-reduced-motion`, when GSAP is
missing, and when the page is inside an iframe. That last case matters: if this page
is ever embedded in Webflow the animations will not run, exactly as with SMO. The
ranked bars are driven by a separate IntersectionObserver so they still animate in
the iframe case.

## Buttons

Use `hmc-btn` plus `hmc-btn-primary` or `hmc-btn-secondary`, and set `data-hmc-label`
to the same text as the label. The 1.0.3 CSS builds the roll-up from that attribute.
Do not also load `hmc-buttons-1.0.0.js`: it wraps text nodes for the older 1.0.0 CSS
and renders every label twice.

## Photos still needed

Only two images exist for this program, both pulled from the Webflow CMS:

    photos/vitals-pop-up.png        blood pressure screening at an outdoor pop-up
    photos/outreach-team-park.jpg   outreach team group shot at a park deployment

No Skid Row photography is used here. SMO's photos belong to a different program and
reusing them would blur the two.

Consequences of the shortage, and what to shoot:

1. **Hero slides 3 and 4 are second crops of the same two photos.** Drop in
   `photos/mho-hero-3.jpg` and `photos/mho-hero-4.jpg` and swap the two `background-image`
   values in the hero carousel markup. Shoot landscape, at least 2000px wide, with
   room at the bottom for the headline scrim.
2. **`vitals-pop-up.png` is only 1024px wide.** It is sharp in the framed figure and
   in the split panel, but it is soft as a full-bleed hero slide. A higher resolution
   version of the same scene would fix both hero appearances.
3. **There is no photo of the education table or the navigation table.** The
   deployment section runs as text cards for that reason. Two photos, one of each
   table with a volunteer working it, would let that section carry a photo band.
4. **There is no photo of the family or children's activity.** That is the finding
   the page argues hardest, so an image of it would do real work.

Consent: anyone identifiable in a new photo needs a signed media release on file
before it goes on this page. The face in `vitals-pop-up.png` is already blurred at
source; keep it that way.

## Open items

- Nothing links to a downloadable version of the community feedback summary. If a
  one-page summary is published later, add a card in the same style as SMO's reports
  grid and link it.
- The hero stat row shows raw counts for two of three figures. If a percentage is
  preferred there, split the decimal the way the stat cards do so the count-up still
  fires.
