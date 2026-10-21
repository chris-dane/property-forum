# The Property Forum: brochure site with membership

The brochure site plus a membership offer: Guest (tickets on Eventbrite),
Member and Patron (subscriptions through Stripe Payment Links). Still no build
step, no JavaScript, no CMS and no third-party scripts on the page itself;
checkout happens on Stripe's hosted page and comes back to `/welcome/`.

Read `../docs/membership-design.md` for the thinking, the mechanics, and the
setup steps in Stripe and Eventbrite. Prices on the page are placeholders.

```
index.html          The page. Plain HTML, no build step.
privacy/index.html  Privacy policy.
welcome/index.html  Where Stripe sends people after they join.
../docs/            Membership design notes and setup steps (kept out of the deployed folder).
404.html            Not-found page.
css/style.css       All styling.
fonts/              Outfit, four weights, served from here.
images/             Photos, team portraits, sponsor logos, logo.
wrangler.jsonc      Cloudflare config (optional).
```

## Events

The page deliberately carries no event dates. Eventbrite is the source of
truth: the "What's on" band describes the season and sends people to the
organiser page, so nothing on the site goes stale and there is no recurring
edit. Every Eventbrite link currently points at `https://www.eventbrite.co.uk/`;
replace those with the Forum's organiser page URL once Jo supplies it.

Everything on the page (team, sponsors, testimonials, venues) is plain HTML
in `index.html`. To add a sponsor, drop a logo into `images/sponsors/` and
copy one of the `<li>` lines in the sponsors list.

## Going live with membership

Five placeholders need real URLs from Stripe before this is published:
`PAYMENT_LINK_MEMBER_MONTHLY`, `PAYMENT_LINK_MEMBER_YEARLY`,
`PAYMENT_LINK_PATRON_MONTHLY`, `PAYMENT_LINK_PATRON_YEARLY` in `index.html`,
and `STRIPE_CUSTOMER_PORTAL_LINK` in `index.html` and `welcome/index.html`.
Search for them. The design notes explain how to create each.

## Hosting

Currently on GitHub Pages as a preview for Jo, served from the root of `main`
in https://github.com/chris-dane/property-forum:

- **Preview:** https://chris-dane.github.io/property-forum/
- **To publish a change:** commit and push from this folder. Pages rebuilds
  in about a minute. Paths in the pages are relative, so the same files work
  at the real domain or on any other host without edits. The one exception
  is the `og:image` tag in `index.html`, which must be an absolute URL and
  currently points at the preview.

Any static host works if this moves later. Three options:

- **Cloudflare Workers:** `npx wrangler deploy` from this folder uploads it.
  Add the custom domain in the dashboard, or uncomment `routes` in
  `wrangler.jsonc` once the domain is in that Cloudflare account.
- **GitHub Pages** (current): push this folder to a repo, Settings > Pages >
  Source: "Deploy from a branch", branch `main`, folder `/`. No workflow needed.
- **Netlify:** drag the folder onto the Netlify dashboard.

## Design

Two acts. The top of the page is the room with the lights down: the headline
beside three photos of the Forum in session, the amber of a table lamp coming
up, and a band about what's on. Below that the house lights come up: a pale
stone ground for who the Forum is, the membership offer, where it meets, who
runs it, who backs it, and how to get involved. The footer dims again.

The photos are phone shots capped at 1500 pixels wide by Webflow's CDN, which
is why the hero shows them at under half the viewport rather than full-bleed.
If Jo can supply originals, a full-bleed hero becomes an option.

One typeface (Outfit, already the brand's heading face), set light and large.
One accent: the four-colour stripe from the logo, used three times, and once
as a chart, where the audience breakdown becomes the stripe itself.

No slider, no form, no cookie banner. Booking goes to Eventbrite; contact is
an email link. Because there are no cookies or analytics, there is no banner.
