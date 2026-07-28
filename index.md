# Privacy Policy — VexAI (AI Translate & Reading Assistant)

**Effective date:** 25 July 2026
**Last updated:** 25 July 2026
**Contact:** pyktools@gmail.com

VexAI is a browser extension that translates web pages, images and documents, answers
questions about the page you are reading, and dubs YouTube videos. This policy explains
exactly what data the extension handles, where it goes, how long it is kept, and what
control you have over it.

We do not sell your data. We do not use it for advertising. The extension contains no
analytics, tracking pixels, or telemetry of any kind.

---

## 1. Summary

| | |
|---|---|
| **Do we sell or share data with data brokers?** | No. |
| **Do we use your data for advertising?** | No. |
| **Is there analytics or usage tracking?** | No. The extension sends no telemetry. |
| **Do we read your browsing history?** | No. We never collect a list of sites you visit. |
| **Is an account required?** | No — but AI features require signing in with Google. |
| **Can you use your own AI API keys instead of our servers?** | Yes. See §6. |

---

## 2. What the extension does *not* do

These are worth stating plainly, because the extension requests broad permissions:

- It does **not** run in the background collecting the pages you visit. Page content is
  read **only** at the moment you invoke a feature on that page (e.g. you click
  "Translate" or open the Page Assistant).
- It does **not** transmit your cookies, passwords, or form data to us or to any third
  party. See §7 for the one narrow use of cookies.
- It does **not** contain analytics, crash reporting, session recording, fingerprinting,
  or advertising code.
- It does **not** scan, index, or bulk-read your Google Drive, Gmail, Sheets or Docs.
  See §8.

---

## 3. Account data

Signing in is optional; it is required only for AI-powered features and for purchasing
credits.

When you sign in with Google, we receive from Google and store on our servers:

- your Google account ID
- your email address
- your display name
- your profile picture URL

We store this in our database (hosted on Supabase) together with your credit balance.
We use it to identify your account, apply your credit balance, and contact you about
your purchases. We do not receive or store your Google password.

Your session token and profile are also stored locally in your browser
(`chrome.storage.local`) so you stay signed in.

---

## 4. Data sent to our servers when you use a feature

Requests go to our backend (`api.vexa.app`), which forwards them to AI model providers
(§5). Nothing below is sent unless you actively invoke the feature.

| Feature you invoke | What is sent | Retained on our servers |
|---|---|---|
| **Page Assistant (chat)** | Your message, the conversation history, and — if page reading is enabled — the current page's URL, title and extracted text; plus any screenshot or image you attach | Conversation stored so you can resume it. **Auto-deleted after 60 days.** |
| **Image / comic translation** | The image content, plus source and target language | Not stored against your account. Extracted + translated text may be cached — see §9. |
| **Snip & translate (OCR)** | The screen region you selected | Not retained |
| **Web page translation** | The text segments to translate | Not retained |
| **Advanced / document translation** | The text or document you submitted | Not retained |
| **AI content detector** | The text or image you submitted | Not retained |
| **Safe link — "Check link with AI"** | Only the single link URL you selected from the right-click menu. Our server then fetches that page itself, without any of your cookies or credentials, and analyses its content. We never receive the links you merely hover over, click, or visit. | Not retained |
| **Writing assistant** | Your prompt and the text you are working on | Not retained |
| **News / topic search** | Your search keywords and language | Search history stored. **Auto-deleted after 90 days.** |
| **Music recognition** | The audio file or URL **you explicitly upload or paste** — the extension never records audio on its own | Not retained |
| **YouTube dubbing** | The subtitle / transcript text to be translated and voiced | Not retained |
| **Custom Vibes effects** | The effect definition you create | Stored until you delete it |
| **Feedback form** | The message you write | Stored |
| **Buying credits** | Handled by Paddle (§5). We store the transaction record. | Transaction log auto-deleted after 60 days |

Retention above is enforced automatically by a daily cleanup job on our servers.

---

## 5. Third parties who process data for us

| Provider | Role | What they receive |
|---|---|---|
| **Supabase** | Database hosting | Account record, chat sessions, search history, transactions |
| **AI model providers** — Alibaba Qwen, Google Gemini, OpenAI, DeepSeek, accessed via OpenRouter and our LiteLLM proxy | Generating translations and AI answers | The content of the specific request you made (text, image, page extract). Routing depends on the model selected for the feature. |
| **Google** | Sign-in; machine translation; OCR | OAuth identity check; text sent to Google Translate for the fast translation mode |
| **Paddle** | Payment processing (Merchant of Record) | Your billing details, collected **directly by Paddle**. We never see or store your card number. |

---

## 6. Using your own API keys (BYOK)

In Settings you may supply your own OpenAI, Google Gemini, or Google Cloud Vision API
key. When a key is set, those requests go **directly from your browser to that provider**
— they do not pass through our servers, and we never see that content or the key.

**Important:** these keys are saved in `chrome.storage.sync`, which means Chrome
synchronises them to your Google account and to your other signed-in Chrome
installations. This is standard Chrome behaviour, not a transmission to us. If you do
not want your keys synced, remove them from Settings.

---

## 7. Why the extension needs each permission

| Permission | Why it is needed |
|---|---|
| `<all_urls>` / `activeTab` / `scripting` | To read and translate the page you are currently on, and to draw the translation overlay and side panel. Content is read only when you invoke a feature. |
| `storage` | To save your settings, notes, and sign-in session |
| `tabs` | To know which tab a feature was invoked on, and to open the settings page |
| `contextMenus` | The right-click "VexAI" submenu on selected text (Translate, Summarize, Explain, Reply), and — when Safe link check is enabled — the "Check link with AI" entry shown on links |
| `identity` | Google sign-in |
| `cookies` | **Two narrow uses only:** (a) when downloading an image that is protected against hotlinking, we re-attach the cookie you already have for *that image's own site* so the download succeeds; (b) we attach your youtube.com cookie when fetching YouTube subtitles. In both cases the cookie is sent **only back to the site it belongs to**. Cookies are never sent to VexAI or to any third party. |
| `offscreen` | Audio playback for YouTube dubbing |
| `declarativeNetRequestWithHostAccess` | To set the correct `Referer` when fetching images from sites that block hotlinking |
| Host access to `api.openai.com`, `generativelanguage.googleapis.com`, `vision.googleapis.com`, `translate.googleapis.com` | Direct calls to these providers in BYOK mode and for fast translation |

---

## 8. Google Sheets and Google Docs access

Signing in to VexAI asks only for your basic Google identity (`openid`, `email`,
`profile`). Two further scopes exist, and they are requested **separately and only at the
moment you first open the Google Sheets or Google Docs skill** — never during normal
sign-in:

- `.../auth/spreadsheets` — read and edit Google Sheets
- `.../auth/documents` — read and edit Google Docs

If you only use VexAI to translate and read, you are never asked to grant these at all.

We deliberately do **not** request any Google Drive scope. The extension cannot list,
browse, or download files from your Drive — it can only act on the specific Sheet or Doc
you have open at the time.

These scopes are used **only** by the Page Assistant's optional Google Sheets / Google
Docs skills, and only when you have explicitly enabled that skill and are working on such
a document. In that case:

- the relevant cell range or document content is sent to the AI model so it can answer
  or perform the edit you asked for;
- any edit is written **directly from your browser to the Google API**;
- we do **not** browse, list, index, or back up your Drive, and we do not store your
  Sheets or Docs content on our servers.

If you never enable these skills, these scopes are never exercised. You can revoke them
at any time at [myaccount.google.com/permissions](https://myaccount.google.com/permissions).

---

## 9. Shared translation cache

To reduce cost and latency, translations of **images** are cached on our servers keyed by
a hash of the image, and reused for anyone who later translates the identical image. The
cache entry contains the extracted and translated text — it is **not linked to your
account or to any user identifier**, and entries expire after 180 days.

Because the translated text of an image you process may be served to another user who
processes the same image, **do not use image translation on private or confidential
images while this is enabled.**

You can turn this off: **Settings → Comic settings → "Enable global translation cache"**.
With it off, your translations are not written to the shared cache.

---

## 10. Features that never leave your device

These run entirely locally and make no network requests:

- **Gmail pre-send check** — the confirmation dialog before you send an email. Your email
  content is analysed in the page and never transmitted.
- **Safe-link check (automatic warning)** — the warning shown when you click a link with a
  suspicious URL structure is computed entirely in the page. No link you hover, click, or
  visit is transmitted. The separate **"Check link with AI"** action is *not* local — it
  only runs when you choose it from the right-click menu, and it does send that one URL.
  See §4.
- **Quick Notes** — stored in `chrome.storage.local` on your machine only.
- All extension settings and panel layout state.

---

## 11. Data stored on your own device

| Location | Contents |
|---|---|
| `chrome.storage.sync` (synced by Chrome to your Google account) | Settings: languages, theme, enabled sites, translation mode, and any API keys you entered |
| `chrome.storage.local` (this device only) | Sign-in token and profile, quick notes, translation cache, panel state |

Uninstalling the extension removes both. Removing your server-side account requires a
request — see §12.

---

## 12. Your rights and choices

- **Access / export** — Settings → Data → Export copies your local settings and data.
- **Delete your server-side data** — email **pyktools@gmail.com** from the address you
  signed up with. We will delete your account record, chat sessions, and search history
  and confirm within 30 days. (There is currently no self-service delete button; this is
  handled manually.)
- **Delete local data** — sign out, or uninstall the extension.
- **Withdraw Google access** — [myaccount.google.com/permissions](https://myaccount.google.com/permissions).
- **Opt out of the shared cache** — see §9.
- **Avoid our servers entirely** — use your own API keys (§6).

Depending on where you live you may have additional rights (access, rectification,
erasure, portability, objection) under the GDPR or similar laws. Use the contact address
above to exercise them.

---

## 13. Security

Traffic between the extension and our servers uses HTTPS. Access to your account data is
protected by a signed session token, and database rows are isolated per user by row-level
security. No system is perfectly secure; please report vulnerabilities to
pyktools@gmail.com.

---

## 14. Children

VexAI is not directed to children under 13, and we do not knowingly collect data from
them. If you believe a child has provided us data, contact us and we will remove it.

---

## 15. International transfers

Our infrastructure and AI providers operate in multiple regions, including outside your
country of residence. By using the extension you understand your request content may be
processed in those regions.

---

## 16. Changes to this policy

If we change how data is handled we will update this page and revise the "Last updated"
date. Material changes will also be noted in the extension's release notes on the Chrome
Web Store.

---

## 17. Contact

Questions, requests, or complaints: **pyktools@gmail.com**
