# kimberlyberg.com

One-page site for Kimberly Berg, plus a Stripe "Book & pay" button.
Plain HTML and CSS — no build step, no dependencies. Hosted free on GitHub Pages.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole page. Every editable bit is marked `EDIT:` |
| `styles.css` | Colours, type, layout. Palette is at the top in `:root` |
| `assets/kimberly-1.jpg` | Hero photo — **placeholder**, overwrite with the real one |
| `assets/kimberly-2.jpg` | About-section photo — **placeholder**, overwrite or delete |
| `CNAME.example` | Rename to `CNAME` once the domain is bought |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is |

## The five things to fill in

Search `index.html` for `EDIT:`.

1. **Bio copy** — `#about`, three paragraphs of draft text to replace with Kimberly's own words.
2. **Photos** — drop real images over `assets/kimberly-1.jpg` and `kimberly-2.jpg`. Keep them portrait (4:5), roughly 800×1000 or larger, under ~400KB each.
3. **Email and phone** — `#contact` and the footer. Currently `hello@kimberlyberg.com` / `+1 (000) 000-0000`.
4. **Stripe link** — the `data-stripe-link` attribute on the Book & pay button. Paste the payment link URL there; the button wires itself up.
5. **Domain** — rename `CNAME.example` to `CNAME`, and update `og:url` / `canonical` in `index.html`.

## Preview locally

```
python3 -m http.server 8000
```

Then open http://localhost:8000

## Deploy to GitHub Pages

1. Push this repo to GitHub.
2. Repo → **Settings** → **Pages** → Source: **Deploy from a branch**, branch `main`, folder `/ (root)`.
3. It goes live at `https://<user>.github.io/<repo>/` within a minute or two.

### Custom domain

1. Buy the domain (~$15/yr, registered in Kimberly's name).
2. Rename `CNAME.example` → `CNAME` and commit it.
3. At the registrar, add these DNS records:

   | Type | Name | Value |
   |---|---|---|
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | CNAME | www | `<user>.github.io` |

4. Settings → Pages → Custom domain → enter the domain → tick **Enforce HTTPS** once the certificate is issued (can take up to 24h).

## Stripe — read before promising the split

The button just points at a Stripe URL, so the site itself is done either way. But the
"client pays $180 → Kimberly gets $150, Michael's 20% goes to him automatically" part
is a **Stripe Connect** setup, not a plain payment link:

- Michael's account has to be the **platform**, with Kimberly's account connected to it.
- The payment link must be created *through the platform* with an application fee, so the
  20% is routed on Michael's side and card fees come off his share.
- A standalone payment link made in Kimberly's own dashboard **cannot** split — the full
  $180 lands with her and Michael would have to invoice.

Worth confirming which of the two is actually being set up before the proposal goes out.
