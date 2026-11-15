# Share This Life — $19 chapter preview

This is a **preview** of a new offer for [sharethislife.com](https://sharethislife.com/): a $19 done-for-you story chapter made from a 10–20 minute family recording.

It is a separate repo and a separate GitHub Pages site. It does **not** change the live site or the `evanmack45/sharethislife.com` repo.

Preview URL: https://evanmack45.github.io/sharethislife-preview/

Every page is `noindex, nofollow`. `robots.txt` disallows all crawlers. There is no `CNAME` file.

## The offer

A customer records (or already has) a 10–20 minute conversation with a parent or grandparent, emails it in, and within 48 hours gets back a finished story chapter in that person’s own words (PDF plus editable text), with one free revision. $19.

The thanks page (`/thanks-r8m3/`, unlinked, noindex) tells them to email the audio — or a Google Drive, Dropbox, or iCloud share link — to sharethislife@agentmail.to.

## Stripe

The pay button is wired from one constant in `js/config.js`:

```
var STRIPE_PAYMENT_LINK = "https://buy.stripe.com/3cIfZ90LO2T77Oz1n93oA05";
```

If the value contains `PLACEHOLDER`, a “payment link coming” note is shown and the button will not navigate. With a real link, that note stays hidden. The on-page consent checkbox still has to be checked before the button works.

After payment, Stripe should redirect to `/thanks-r8m3/`. On this preview host that path is `https://evanmack45.github.io/sharethislife-preview/thanks-r8m3/` — the live-domain redirect will work once this offer is published on the real site.

This domain is listed for sale: [Afternic listing](https://www.afternic.com/domain/sharethislife.com).
