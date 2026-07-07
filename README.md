# RetiredRefi

Flagship landing site for retiredrefi.com — retiree refinance/cash-out lead generation, an AdaptLend service.

Static site: `index.html` + `styles.css` + `script.js`. No build step.

## Lead storage

The form inserts into the **same Supabase `leads` table as adaptlend.com** (project `jaqtpjsnnsyxispgyzya`, insert-only RLS, publishable key in `script.js`). RetiredRefi leads are attributed via the `matched_product` suffix `— RetiredRefi` (e.g. "Asset-Based Loan — RetiredRefi").

Optional cleaner attribution: add a nullable `source` column to `leads` and set `source: "retiredrefi"` in `script.js`'s lead object.

Note: the AdaptLend `send-welcome` edge function is NOT called from this site (it sends AdaptLend-branded email). Add a RetiredRefi-branded welcome email later if wanted — the success screen already tells borrowers to watch their email, so wire that up before heavy traffic or soften the copy.

## Deploy (GitHub Pages, same pattern as adaptlend)

1. `git init && git add -A && git commit -m "RetiredRefi landing site"`
2. Create GitHub repo (e.g. `mohamedalloo/retiredrefi`), push `main`.
3. Repo Settings → Pages → deploy from `main` branch root. `CNAME` file is already in place.
4. Namecheap DNS for retiredrefi.com: four GitHub Pages A records (185.199.108.153 / .109. / .110. / .111.) + `www` CNAME to `mohamedalloo.github.io`, then enable Enforce HTTPS once the cert issues.
5. Point retiredrefinance.com (and other retiree satellite domains) at this site with permanent redirects in Namecheap.

## Compliance notes

- RetiredRefi is a DBA-style brand of the AdaptLend service (Honest Casa LLC, NMLS #1566096, DRE #02022356); footer discloses the relationship and links to AdaptLend's Terms/Privacy. Confirm with counsel whether RetiredRefi needs its own DBA filing before spending on traffic.
- Reverse-mortgage content is deliberately educational-only (no urgency, explicit non-affiliation with HUD/FHA disclosure in footer) — keep it that way; reverse advertising is the most-enforced category in mortgage.
- The asset-depletion calculator is labeled illustrative; keep the "not a quote or commitment" footer language.
