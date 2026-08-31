# TR Service og Byg

Website for a small construction company in Kokkedal, Denmark — two employees, no marketing department, and customers who find them on a phone in the middle of a problem.

**Live:** https://oskar-bobro.github.io/TR-Service-og-Byg/

My first web project, built while moving into software development.

## How it was built

Plain HTML and CSS. No framework, no build step, no dependencies, no JavaScript. Deployed with GitHub Pages — a push to `main` publishes.

Every line was written by hand with MDN as the reference. I used Claude as a mentor and reviewer: it supplied the copy and the design specifications, explained mechanisms I had not met before, and criticised what I wrote. It did not write the code. I can explain any line in this repository and why it is there.

The commit history is the real record — 69 commits, one intent each.

## Three decisions worth explaining

**No width-based breakpoints.**
There is exactly one media query on this site, and it asks about `prefers-reduced-motion`, not screen width. Fluid type with `clamp()`, a reading column capped in `ch`, and `repeat(auto-fit, minmax(13rem, 1fr))` for the cards each handle width on their own. I checked the layout from 320px upwards before concluding that a breakpoint was not needed — every extra breakpoint is another state to keep consistent later.

**Two container widths, not one.**
`.container` is 70ch, `.container-wide` is 72rem. A reading column and a page shell should not be the same width: the 45–75 character limit exists because the eye loses its place on long lines, and that reason does not apply to a company name and four nav links. I tried one shared width first — 70ch left roughly 50px for `space-between` to distribute, and the header collapsed in on itself. Both classes carry the same `padding-inline`, so the left edges still line up down the page.

**Only the phone number is solid.**
After the service cards there were five identical filled buttons. A page where everything shouts has no hierarchy. The phone number is the filled one wherever it appears — in the hero and in the contact section — and everything else is a ghost variant of the same class. These customers call, so calling should be the loudest thing on the page.

## Accessibility

Checked, not assumed:

- Contrast measured in DevTools for every text and background pair. White on the accent colour is 4.84:1 against WCAG AA's 4.5:1 minimum; body text is 15.87:1; the button's hover state rises to 7.15:1, so hovering makes it more readable rather than less
- `:focus-visible` rather than `:focus`, so keyboard users get a focus ring and mouse users do not
- Tap targets measured in DevTools against the 44px minimum instead of guessed
- `font-size: 100%` on `html`, so the browser's own font-size setting is respected
- Smooth scrolling is opt-in through `prefers-reduced-motion: no-preference` — if the browser says nothing, the safe default wins
- Validates with no errors at validator.w3.org

## Structure

```
index.html
css/style.css
```

Two files. The stylesheet is built on two tiers of custom properties — raw values (`--color-brick-50`) with semantic names layered on top (`--color-accent`) — so changing my mind about a colour is one line rather than forty.

## Status

The layout is finished and live. The remaining work is content: real jobs, photos and a coverage area are coming from the owner and go in as they arrive, which is why a few descriptions are still generic. The site began as a surprise for him, so anything I could not ask about was written as a placeholder on purpose.
