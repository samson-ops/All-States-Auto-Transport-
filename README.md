# All States Auto Transport — website

Static home page for All States Auto Transport with the live pricing tool.

## What is here

| Path | What it is |
|---|---|
| `index.html` | The home page. The pricing tool is pasted into the hero; only its `PQ_CONFIG` block was edited. |
| `assets/` | Logo, hero photo, service icons and badges. |
| `functions/api/quote/[[path]].js` | Cloudflare Pages Function that forwards quote requests to the lead system. It holds the Lead Source key server-side. |

## Before launch

1. **Lead Source key.** Create a new Lead Source for this website in BeRocker and set its key as the
   `BEROCKER_LEAD_KEY` environment variable in Cloudflare (Pages project → Settings → Environment variables),
   or paste it as `DEFAULT_KEY` in `functions/api/quote/[[path]].js`. Do not reuse the shipguy.com keys.
   Until this is set, quotes will not save.
2. **Phone number and site link.** In `index.html`, find `window.PQ_CONFIG` and fill in `phoneDisplay`,
   `phoneTel` (`+1…` format), `siteUrl` and `siteLabel`. Every phone link on the page reads from these two phone values.
3. **Google Maps key.** `googleMapsKey` in `PQ_CONFIG` is the existing key from the pricing tool. Add this
   site's domain to its referrer restrictions, or swap in a new key. It only powers ZIP suggestions.
4. **Placeholders.** Search `index.html` for `[YOUR` and replace: USDOT #, MC #, email, address,
   deposit policy, personal items policy.
5. **Footer links.** Privacy, Terms, and Licensing & Insurance currently point to the top of the page.

## Deploy (Cloudflare Pages)

Connect this repository as a Pages project with no build command and the repository root as the output
directory. The `functions` folder is picked up automatically.

## Test after deploy

- Pickup and Delivery accept only 5-digit ZIP codes.
- Year → Make → Model load in order.
- Submitting step 3 without the consent box checked is blocked.
- After submit, a price appears and the lead shows up in BeRocker under this site's Lead Source.
