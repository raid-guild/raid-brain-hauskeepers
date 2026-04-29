# DAOhaus DNS Catalog

## Active Subdomains

| Subdomain                | Hosted On                               | Repo                                                                          | Next Steps                        |
| ------------------------ | --------------------------------------- | ----------------------------------------------------------------------------- | --------------------------------- |
| `daohaus.club` (root)    | Netlify (`daohaus-website.netlify.app`) | —                                                                             | Move to Railway                   |
| `www.daohaus.club`       | Netlify (`daohaus-website.netlify.app`) | —                                                                             | Move to Railway                   |
| `app.daohaus.club`       | Netlify (`daohaus-app.netlify.app`)     | —                                                                             | —                                 |
| `admin.daohaus.club`     | Railway                                 | [HausDAO/daohaus-admin](https://github.com/HausDAO/daohaus-admin)             | —                                 |
| `docs.daohaus.club`      | Vercel                                  | —                                                                             | Move to Railway; confirm with e2t |
| `guide.daohaus.club`     | Vercel                                  | —                                                                             | Move to Railway; confirm with e2t |
| `decode.daohaus.club`    | Vercel (sam's personal)                 | [HausDAO/proposal-decode-api](https://github.com/HausDAO/proposal-decode-api) | Move or deprecate                 |
| `links.daohaus.club`     | Vercel                                  | —                                                                             | Deprecate after cataloging links  |
| `summon.daohaus.club`    | Cloudflare Pages                        | —                                                                             | Deprecate with docs update        |
| `cco.daohaus.club`       | Netlify                                 | —                                                                             | —                                 |
| `proposals.daohaus.club` | Netlify                                 | —                                                                             | —                                 |
| `speedball.daohaus.club` | Netlify                                 | —                                                                             | —                                 |
| `stats.daohaus.club`     | Netlify                                 | —                                                                             | —                                 |

---

## Open Questions — Possible Deprecations

Records that may no longer be needed. Needs review before removal.

| Subdomain                | Current Target                         | Question                                       |
| ------------------------ | -------------------------------------- | ---------------------------------------------- |
| `daogroni.daohaus.club`  | `dreamy-leakey-760c51.netlify.app`     | Still in use?                                  |
| `cco.daohaus.club`       | `laughing-euclid-dcc231.netlify.app`   | Still in use?                                  |
| `farm.daohaus.club`      | `silly-nightingale-84955d.netlify.app` | Still in use?                                  |
| `moloch.daohaus.club`    | `gallant-hopper-999067.netlify.app`    | V1 era — likely dead; no known repo or address |
| `speedball.daohaus.club` | `zippy-parfait-37ac33.netlify.app`     | Still in use?                                  |
| `v2-web.daohaus.club`    | `daohaus-website.netlify.app`          | Legacy alias for www — safe to remove?         |
| `yeet.daohaus.club`      | `admiring-johnson-bc0a30.netlify.app`  | Still in use?                                  |

**Mail (MX / SES / DKIM):** Current records point to Google Workspace. Need to confirm mail is still actively used and who owns the Workspace account before touching anything here.

---

## Full Detail Catalog

_Domain: `daohaus.club` — All TTLs: 3600_

---

## A Records

| Hostname                        | Type | Value            | Status               | Notes                                |
| ------------------------------- | ---- | ---------------- | -------------------- | ------------------------------------ |
| `forum.daohaus.club`            | A    | `34.201.34.147`  | Deprecated 4.29.2026 | Forum application                    |
| `idchain.daohaus.club`          | A    | `18.191.241.139` | Deprecated 4.29.2026 | IDChain node                         |
| `subgraph.idchain.daohaus.club` | A    | `18.191.241.139` | Deprecated 4.29.2026 | IDChain subgraph; same IP as idchain |

---

## CNAME Records — App Routing

| Hostname                   | Type  | Value                                 | Status                                | Notes                                                 |
| -------------------------- | ----- | ------------------------------------- | ------------------------------------- | ----------------------------------------------------- |
| `admin.daohaus.club`       | CNAME | `admin-3eg.pages.dev`                 | Deprecated 4.29.2026                  | Admin UI (Cloudflare Pages)                           |
| `books.daohaus.club`       | CNAME | `c34697bea852165f597e.b-cdn.net`      | Deprecated 4.29.2026                  | Books app (BunnyCDN)                                  |
| `dapp.daohaus.club`        | CNAME | `e72a6be83867ccfdd531.b-cdn.net`      | Deprecated 4.29.2026                  | DApp (BunnyCDN)                                       |
| `data.daohaus.club`        | CNAME | `d2bzc58nkck701.cloudfront.net`       | Deprecated 4.29.2026                  | Data API endpoint (CloudFront)                        |
| `decode.daohaus.club`      | CNAME | `b138d47b2173e4ad.vercel-dns-017.com` | Active                                | Decode app used in rg proposal notifications (Vercel) |
| `docs.daohaus.club`        | CNAME | `cname.vercel-dns.com`                | Active                                | Documentation site (Vercel)                           |
| `guide.daohaus.club`       | CNAME | `cname.vercel-dns.com`                | Active                                | Guide/docs (Vercel)                                   |
| `links.daohaus.club`       | CNAME | `cname.vercel-dns.com`                | TODO: Deprated after cataloging links | Links page (Vercel)                                   |
| `migrate.daohaus.club`     | CNAME | `lvdb2kcg.up.railway.app`             | Deprecated 4.29.2026                  | Migration tool (Railway)                              |
| `safe-summon.daohaus.club` | CNAME | `summon-safe.pages.dev`               | Deprecated 4.29.2026                  | Safe summoner (Cloudflare Pages)                      |
| `shadow.daohaus.club`      | CNAME | `q79j0thc.up.railway.app`             | Deprecated 4.29.2026                  | Shadow app (Railway)                                  |
| `storybook.daohaus.club`   | CNAME | `storybook-2i6.pages.dev`             | Deprecated 4.29.2026                  | Storybook component library (Cloudflare Pages)        |
| `summon.daohaus.club`      | CNAME | `summon.pages.dev`                    | TODO: Deprecate with docs update      | DAO Summoner (Cloudflare Pages)                       |

---

## CNAME Records — Infrastructure (ACM / DKIM)

| Hostname                                                   | Type  | Value                                                              | Status               | Notes                                                                                                                      |
| ---------------------------------------------------------- | ----- | ------------------------------------------------------------------ | -------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `_69a53c78a088f8b747b3698110bf7a72.data.daohaus.club`      | CNAME | `_e4229b7926cea4e613c6c25a34861ba7.wggjkglgrm.acm-validations.aws` | Deprecated 4.29.2026 | ACM TLS certificate validation for data.daohaus.club                                                                       |
| `_a4f3ec25d665dd2ba13f3da97a52a0b1.cco.daohaus.club`       | CNAME | `_f7a5e1ff764cabf960c3183d39634bdb.zzxlnyslwt.acm-validations.aws` | Deprecated 4.29.2026 | ACM TLS certificate validation for cco.daohaus.club                                                                        |
| `mp334dbpudvauvv26fiascu72dge2inb._domainkey.daohaus.club` | CNAME | `mp334dbpudvauvv26fiascu72dge2inb.dkim.amazonses.com`              | Active               | SES Easy DKIM public key (key 1 of 3) — allows receiving servers to verify DAOhaus emails weren't spoofed or tampered with |
| `oxvzx6thu5pj5htabve3jkjns3ftjb3r._domainkey.daohaus.club` | CNAME | `oxvzx6thu5pj5htabve3jkjns3ftjb3r.dkim.amazonses.com`              | Active               | SES Easy DKIM public key (key 2 of 3)                                                                                      |
| `xdwcisadpwmo2qjeu65mq722e2427dmt._domainkey.daohaus.club` | CNAME | `xdwcisadpwmo2qjeu65mq722e2427dmt.dkim.amazonses.com`              | Active               | SES Easy DKIM public key (key 3 of 3)                                                                                      |

---

## MX Records

| Hostname       | Type | Value (Priority + Server)     | Status | Notes                              |
| -------------- | ---- | ----------------------------- | ------ | ---------------------------------- |
| `daohaus.club` | MX   | `1 ASPMX.L.GOOGLE.COM.`       | —      | Google Workspace email — primary   |
| `daohaus.club` | MX   | `5 ALT1.ASPMX.L.GOOGLE.COM.`  | —      | Google Workspace email — secondary |
| `daohaus.club` | MX   | `5 ALT2.ASPMX.L.GOOGLE.COM.`  | —      | Google Workspace email — secondary |
| `daohaus.club` | MX   | `10 ALT3.ASPMX.L.GOOGLE.COM.` | —      | Google Workspace email — tertiary  |
| `daohaus.club` | MX   | `10 ALT4.ASPMX.L.GOOGLE.COM.` | —      | Google Workspace email — tertiary  |

---

## NETLIFY Records

| Hostname                     | Type    | Value                                   | Status               | Notes                                           |
| ---------------------------- | ------- | --------------------------------------- | -------------------- | ----------------------------------------------- |
| `app.daohaus.club`           | NETLIFY | `daohaus-app.netlify.app`               | Active               | Main v3 app                                     |
| `cco.daohaus.club`           | NETLIFY | `laughing-euclid-dcc231.netlify.app`    | Active               | CCO (Community Contribution Offering) app       |
| `cco3.daohaus.club`          | NETLIFY | `laughing-euclid-dcc231.netlify.app`    | Deprecated 4.29.2026 | CCO v3 — same Netlify target as cco             |
| `daogroni.daohaus.club`      | NETLIFY | `dreamy-leakey-760c51.netlify.app`      | —                    | DAOgroni app                                    |
| `daohaus.club`               | NETLIFY | `daohaus-website.netlify.app`           | —                    | Root domain → main website                      |
| `farm.daohaus.club`          | NETLIFY | `silly-nightingale-84955d.netlify.app`  | —                    | Farm app                                        |
| `freeryder.daohaus.club`     | NETLIFY | `extraordinary-lily-76e6cf.netlify.app` | Deprecated 4.29.2026 | Free Ryder                                      |
| `hats-demo.daohaus.club`     | NETLIFY | `gorgeous-sable-84c11f.netlify.app`     | Deprecated 4.29.2026 | Hats Protocol integration demo                  |
| `haus-hooks.daohaus.club`    | NETLIFY | `dao-hooks.netlify.app`                 | Deprecated 4.29.2026 | Haus Hooks library/demo                         |
| `moloch.daohaus.club`        | NETLIFY | `gallant-hopper-999067.netlify.app`     | —                    | Moloch v1/v2 era app                            |
| `onbrooder.daohaus.club`     | NETLIFY | `sparkly-trifle-11c6b7.netlify.app`     | Deprecated 4.29.2026 | Onbrooder                                       |
| `proposals.daohaus.club`     | NETLIFY | `transcendent-crepe-b58ddc.netlify.app` | Deprecated 4.29.2026 | Proposals app — same target as whispers         |
| `report.daohaus.club`        | NETLIFY | `practical-edison-84de96.netlify.app`   | Deprecated 4.29.2026 | Reports — same Netlify target as stats          |
| `simple-search.daohaus.club` | NETLIFY | `famous-gelato-53c644.netlify.app`      | Deprecated 4.29.2026 | Simple search                                   |
| `slowball.daohaus.club`      | NETLIFY | `grand-vacherin-1b99cd.netlify.app`     | Deprecated 4.29.2026 | Slowball                                        |
| `speedball.daohaus.club`     | NETLIFY | `zippy-parfait-37ac33.netlify.app`      | —                    | Speedball                                       |
| `stats.daohaus.club`         | NETLIFY | `practical-edison-84de96.netlify.app`   | TODO: Deprecate      | Stats dashboard — same Netlify target as report |
| `v2-web.daohaus.club`        | NETLIFY | `daohaus-website.netlify.app`           | —                    | V2 website — same Netlify target as www         |
| `whispers.daohaus.club`      | NETLIFY | `transcendent-crepe-b58ddc.netlify.app` | Deprecated 4.29.2026 | Whispers — same Netlify target as proposals     |
| `www.daohaus.club`           | NETLIFY | `daohaus-website.netlify.app`           | —                    | www → main website                              |
| `yeet.daohaus.club`          | NETLIFY | `admiring-johnson-bc0a30.netlify.app`   | —                    | Yeet app                                        |

---

## TXT Records

| Hostname                               | Type | Value                                                                                              | Status               | Notes                                               |
| -------------------------------------- | ---- | -------------------------------------------------------------------------------------------------- | -------------------- | --------------------------------------------------- |
| `_amazonses.daohaus.club`              | TXT  | `cFxzIKza7GO3kx8p5DcZjXq+rstF9U+9uT/HuE0T6Ls=`                                                     | —                    | Amazon SES domain verification                      |
| `_railway-verify.migrate.daohaus.club` | TXT  | `railway-verify=f9e3b935e061b8936c5d675a5d08cf1fc753a8f4e39dd053d970bb33ef2cab49`                  | Deprecated 4.29.2026 | Railway domain verification for migrate subdomain   |
| `_vercel.daohaus.club`                 | TXT  | `vc-domain-verify=decode.daohaus.club,b8991e211330fb8e3e33`                                        | —                    | Vercel domain verification for decode               |
| `_vercel.daohaus.club`                 | TXT  | `vc-domain-verify=docs.daohaus.club,7679e98382e730821e8e`                                          | —                    | Vercel domain verification for docs                 |
| `_vercel.daohaus.club`                 | TXT  | `vc-domain-verify=guide.daohaus.club,88f627d952641a3b74fb`                                         | —                    | Vercel domain verification for guide                |
| `_vercel.daohaus.club`                 | TXT  | `vc-domain-verify=links.daohaus.club,6f55e27a2546b85c5aae`                                         | —                    | Vercel domain verification for links                |
| `daohaus.club`                         | TXT  | `amazonses:cFxzIKza7GO3kx8p5DcZjXq+rstF9U+9uT/HuE0T6Ls=`                                           | —                    | Amazon SES sending authorization                    |
| `daohaus.club`                         | TXT  | `fortmatic-site-verification=6AqdPyEZ0Cz2pgsg`                                                     | Deprecated 4.29.2026 | Fortmatic (Magic.link) wallet provider verification |
| `daohaus.club`                         | TXT  | `google-site-verification=FmpJiXfwd7RCfpic29fLrKmDwNUO8RqZLarZ2HO2NxY`                             | —                    | Google Search Console verification                  |
| `daohaus.club`                         | TXT  | `wallet-connect-dns-verification=b69c46cb697db60861b2177243205669e60ff15e3bb4ed7da44328c131a69ffd` | —                    | WalletConnect domain verification                   |
