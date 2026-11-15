# Share This Life preview — build log

Times are America/Chicago (CST, UTC-6).

## 2026-11-15

### Plan
Dash asked for a preview (not live) of a $19 done-for-you story chapter, replacing the $7 booklet. Source: Dash's plan (offer, delivery, and risks). Built in a new directory and a new public repo. Did not touch `evanmack45/sharethislife.com`, its `main` branch, or the live site.

### What shipped
- Home page: Thanksgiving / 48-hour offer, $19 chapter, consent checkbox, pay button, privacy line, full-refund line, December 18 Christmas cutoff, “a sample chapter is coming,” and a free hook to twenty questions and table cards.
- Consent gate: the pay button stays disabled until the buyer checks “The person speaking knows they’re being recorded and agreed to it being turned into a chapter.”
- Privacy, consent, and refunds page (`privacy.html`): 30-day deletion, no voice cloning, no reuse, no sharing, full refund on request, quote rule (we don’t invent words; unclear names and dates go back as questions).
- Post-payment page `/thanks-r8m3/` (noindex, not linked from the nav): how to email the recording to sharethislife@agentmail.to, mailto with a prefilled subject (“Share This Life chapter recording”), and a printable one-page “how to record” prompt card (phone voice memo tips plus 10 questions).
- Free hook pages: `questions.html` (the original 20 free questions) and `cards.html` (16 printable table cards). No $7 booklet and no unlock flow.
- Footer: “This domain is for sale” → https://www.afternic.com/domain/sharethislife.com
- Every HTML page has `<meta name="robots" content="noindex, nofollow">`. `robots.txt` is `Disallow: /`. No `CNAME` file.

### Stripe
`STRIPE_PAYMENT_LINK` in `js/config.js` line 11 is the live $19 Payment Link `https://buy.stripe.com/3cIfZ90LO2T77Oz1n93oA05`. Because the value does not contain `PLACEHOLDER`, the “payment link coming” note stays hidden. The one-line swap still works if the link changes.

The link is live mode and charges a real $19. It was not paid. A GET of the URL returned HTTP 200 and the title “Stripe Checkout.” Loading the page in a browser (no form filled, no Pay click) showed: “ETM Industries,” “Story chapter from a recording,” “$19.00,” a required consent dropdown (“The speaker agreed to be recorded”), and “Payment mode: Live mode. Test data not accepted.”

Stripe is set to redirect to `/thanks-r8m3/` on the live domain. That path is not on the live site (this preview must not publish there). The preview thanks page is at `https://evanmack45.github.io/sharethislife-preview/thanks-r8m3/`.

### Local tests (Chromium, `python3 -m http.server` on 127.0.0.1:8766, site served under `/sharethislife-preview/`)
- Home, thanks, privacy, questions, cards, 404, robots.txt, CSS, and JS all returned 200. Relative paths resolved under the subpath.
- Unchecked consent: pay button `aria-disabled="true"`, href stays `#order`, click does not leave the page.
- Checked consent: href becomes the live Stripe link and `aria-disabled` is removed. Unchecking disables it again.
- Placeholder note remains hidden.
- Thanks-page mailto is `mailto:sharethislife@agentmail.to?subject=Share%20This%20Life%20chapter%20recording` (plus a prefilled body for the speaker’s name and relationship).
- Screenshots (viewed): `shots/home-1280.png`, `shots/home-390.png`, `shots/thanks-1280.png`, `shots/thanks-390.png` (gitignored). JPG copies: `/workspace/stl-preview-home-1280.jpg`, `stl-preview-home-390.jpg`, `stl-preview-thanks-1280.jpg`, `stl-preview-thanks-390.jpg`. Offer and consent are visible on the home shots; thanks shows the mailto and the prompt card.

### Hosting
Public repo `evanmack45/sharethislife-preview`, `main` branch, GitHub Pages from `/`. No custom domain and no `CNAME`. Preview URL: `https://evanmack45.github.io/sharethislife-preview/`.
