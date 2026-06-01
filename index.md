# Privacy Policy — Leads Harvest

**Effective date:** 2026-06-01
**Contact:** leadsharvestsupport@gmail.com

Leads Harvest is a Chrome extension that helps you collect publicly available business contact information from Google Maps for your own sales prospecting. This policy explains exactly what data the extension touches, where it goes, and what we (the developer) can and cannot see.

## Short version

- Harvested lead data stays on your device. It is never transmitted to us or to any server we control.
- The only data that leaves your browser to a server operated by us-or-our-vendor is your **license key**, which is sent to Lemon Squeezy to verify your Pro subscription.
- During enrichment, the extension fetches pages from the **business websites you've harvested** to read publicly visible email addresses and social media links from those pages. No data is sent to those sites beyond a normal page request.
- There is no analytics, no telemetry, no tracking pixel, no user account, no advertising SDK.

## What the extension processes

### 1. Lead data (your harvested results)

When you click **Start Harvest** on a Google Maps search results page, the extension reads publicly visible business information from that page and from each business's detail panel:

- Business name, category, address
- Phone number, website
- Star rating and review count
- Business hours (per-day)
- Logo image URL
- Social media URLs (Facebook, Instagram, X/Twitter, LinkedIn, YouTube, TikTok) and email address — discovered by fetching the business's own website (see "Enrichment" below)

All of this is stored in `chrome.storage.local` — a local, per-device area provided by Chrome. It is **not synced**, **not backed up by us**, and **not transmitted anywhere**. You can delete it at any time via the **Clear Saved Leads** button in the popup, or by uninstalling the extension.

When you click **Export to CSV** or **Export to JSON**, the file is generated locally and saved through Chrome's standard download flow. We do not receive a copy.

### 2. Enrichment (fetching business websites)

To find email addresses and social media links that Google Maps does not show, the extension visits each harvested business's website. There are two modes:

- **Phase 1 (all users):** The background service worker makes ordinary HTTP `GET` requests to the business's home page and a small set of common contact paths (`/`, `/contact`, `/contact-us`, `/about`, `/about-us`). Only publicly returned HTML is read.
- **Phase 2 (Pro only):** For sites that didn't return useful results in Phase 1 (typically because their footer is rendered by JavaScript), the extension opens the business's website in a hidden background tab, waits for it to load, reads the rendered page, and closes the tab.

In both modes, the extension is acting as a normal web client. It does not send any data about you to those websites beyond what your browser would normally send when visiting them (User-Agent, IP address, etc., handled by Chrome — not by us).

### 3. License key and Pro activation

If you purchase a Pro license, activation, periodic validation, and deactivation requests are sent directly from the extension to **Lemon Squeezy** at `https://api.lemonsqueezy.com/v1/licenses/*`. Lemon Squeezy is our Merchant of Record and license provider.

- **Sent to Lemon Squeezy:** your license key and a generated instance identifier.
- **Returned from Lemon Squeezy and cached locally:** license status, instance ID, product name, and the customer email associated with the license (so the popup can display "Pro · your@email" as confirmation).
- **Where it's stored:** `chrome.storage.sync` — a Chrome-managed area that syncs across your Chrome installs when you're signed in to Chrome. We do not receive a copy. You can remove it at any time via the **Deactivate this device** link in the popup, or by uninstalling.

Lemon Squeezy's own privacy practices are governed by their privacy policy at https://www.lemonsqueezy.com/privacy.

### 4. Free quota counter

For users on the free tier, the extension stores a single integer (`freeLeadsUsed`) in `chrome.storage.sync` so the lifetime free quota survives reinstalls and tracks across devices signed in to the same Chrome account. No business data is included — only the count.

## What we do **not** collect

- We do not operate any server that receives your harvested leads.
- We do not collect analytics, crash reports, usage statistics, IP addresses, or device identifiers.
- We do not place advertising, fingerprinting, or third-party tracking code in the extension.
- We do not sell, share, or rent any data.

## Permissions and why each is needed

| Permission | Why |
|---|---|
| `storage` | Save your harvested leads, settings, and license state locally |
| `scripting` | Inject the extractor into hidden enrichment tabs (Pro phase-2 only) |
| `activeTab` | Read the Google Maps page when you click Start Harvest |
| `downloads` | Save your CSV / JSON export to your Downloads folder |
| `tabs` | Open and close hidden tabs used for phase-2 enrichment |
| Host access to `https://www.google.com/maps/*` | Harvest from Maps |
| Host access to `<all_urls>` | Fetch and load arbitrary business websites during enrichment — we cannot know in advance which domains your leads' websites will be on |

## Your responsibilities as the user

The data Leads Harvest helps you collect is publicly listed business contact information. Once it's in your browser, **you become the data controller** for it. If you plan to use it for outreach in jurisdictions covered by laws such as GDPR, UK GDPR, CCPA, CAN-SPAM, CASL, or similar, you are responsible for complying with those laws — including any required lawful basis for processing, suppression of opt-outs, and identification requirements in your outreach.

## Data retention and deletion

- **Lead data and free quota counter:** removed when you click **Clear Saved Leads** in the popup, or when you uninstall the extension (local data) / clear Chrome sync data (synced data).
- **License:** removed when you click **Deactivate this device** in the popup, when the license is deactivated server-side, or when you clear Chrome sync data.

We retain no copies because we never receive any.

## Children

Leads Harvest is a business tool not directed at children under 13 and we do not knowingly process data from them.

## Changes to this policy

If we change this policy, we will update the **Effective date** above and post the revised policy at the same location. Material changes will also be noted in the extension's Chrome Web Store listing.

## Contact

Questions, complaints, or deletion requests (though we hold no data to delete on our end): **leadsharvestsupport@gmail.com**.
