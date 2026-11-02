# Atara Salla theme developer requirements

Version 1.0 | 2 November 2026 | Theme 1732779814

## Purpose and release outcome

Deliver an Arabic first, responsive Atara shopping experience on Salla Twilight. Customers must be able to find a suitable item, understand its fabric and measurements, choose an available variant, buy it, track the order and obtain eligible after sales support. The theme must use the official Atara identity and real store content. A working Salla preview and completed acceptance evidence are required before production sign off.

The source baseline is `aea2de02a1e2833b0dfb10fe329de84d9c6a433f` in `noonalifyaa/atara-theme-oct-2026`. The supplied V4 review defines the design direction. Later version names in source comments do not independently establish design approval.

## Changes prepared in this revision

- Replace separate desktop and mobile social components with one responsive icon row. Social destinations continue to come from Salla settings. Retain accessible network names, keyboard focus and 44 by 44 CSS pixel targets.
- Add a configurable Atara Journal homepage component and settings for three curated published article cards. The native blog remains the publishing system. Hide the component if no valid entries are selected.
- Link the journal in the footer when the native blog is enabled. Keep the seven shopping groups in the main navigation.
- Add editable category photography and real images from the public Atara catalogue. Preserve merchant overrides and deliberately empty collections.
- Seed the article selection with three existing Atara articles. These are buying guides published in 2025, not new company announcements. Do not change their publication dates or describe them as recent news.
- Replace the expired October promotional fallback with a general current offers link. Existing saved merchant copy still requires review in the editor.

These source changes do not certify the remaining features below. Salla preview rendering, store configuration, operational content and journey testing must be completed separately.

## Information architecture

| Area | Placement | Required content |
| --- | --- | --- |
| Shopping | Main navigation | شراشف الصلاة، سجاجيد الصلاة، الأزياء، الطرح والإكسسوارات، الأطياب، الهدايا، العروض |
| Atara Journal | Homepage and footer | Buying guides, styling, fabric care, prayer essentials and a distinct أخبار أتارا category |
| About Atara | Footer and short homepage introduction | Approved brand story, product approach, genuine photography and link to shopping |
| Branches | Footer and product support | Verified branch names, address, map, hours, accessibility and contact details |
| Customer help | Footer and contextual links | Size guide, delivery, returns and exchanges, FAQ, contact and tracking |
| Legal and trust | Footer and checkout where supported | Privacy, terms, verified registration and tax details, enabled payment methods |

Do not restore the previous crowded menu by adding news, blog, about us and contact as competing product tabs. Use a small utility link or footer link for the journal and brand pages. Display current offers under العروض; reserve أخبار أتارا for actual announcements.

## Requirements by feature

### NAV Navigation and search

NAV 01 Keep seven top level shopping entries, on one line at desktop widths. At widths where they no longer fit, switch to the compact menu rather than shrinking text. Group clothing and accessory child categories under their parents. Use native category URLs and IDs from the active store. Do not link a demo category to an unrelated live category or use the homepage as a substitute destination.

NAV 02 Provide an accessible mobile drawer with collapsed category groups, a separate expansion control, a working parent category link and a close button reachable while scrolling. Trap focus while open, restore focus on close, support Escape and prevent background scrolling.

NAV 03 Keep a visible search field on mobile. Support Arabic queries and useful suggestions through supported Salla search. Exact product and material matches come first. Put other fabrics in a clearly labelled alternatives area. Design loading, no results, spelling guidance and service errors. Preserve query, filters and scroll position when returning from a product.

Acceptance: at 360, 390, 768, 1024, 1280 and 1440 CSS pixels, labels remain readable and the page has no horizontal overflow. Keyboard users can complete the menu and search tasks.

### HOME Homepage and merchandising

HOME 01 Use this order as the initial configuration: concise hero, category grid, selected products, shopping occasions, current offer, prayer products, trust information, genuine reviews, journal and help. Keep merchandising sections editable and independently removable. Avoid rendering the same section through both the fixed layout and appended editor components.

HOME 02 Replace silhouette placeholders with real Atara photographs showing the correct category. Store a source product URL and image reference for each selected photo. Use a prayer garment for prayer garments and an actual Hajj or Umrah product for that category. Keep text and buttons as HTML. Provide mobile crops without cropping essential product details.

HOME 03 Populate product sections from the active store catalogue. A prayer section must query prayer category IDs, not all discounted products. Weekly picks must be selected products or accurately labelled latest products. Hide empty categories or provide a useful alternative without implying stock exists.

HOME 04 Use configured shipping thresholds and approved operational copy. The existing live homepage says free shipping at 399 SAR and above; do not silently change this to strictly above 399. Confirm whether discounts, gift fees and excluded destinations affect eligibility, then use the same rule throughout the journey. Delivery dates and branch pickup must reflect actual capabilities.

Acceptance: every homepage link opens its intended collection or content; all displayed products belong to their labelled section; no expired campaign or unsupported promise appears.

### SOC Social links and footer

SOC 01 Render social media as icons only. Include the configured Instagram, X, Snapchat, TikTok, YouTube and Facebook accounts. Never show a platform icon if its destination is missing. Do not add invented accounts. WhatsApp may remain a clearly identified customer support action.

SOC 02 Use `<salla-social>` and its documented `social-item` slot. The slot wrapper contains the anchor markup used by the installed component. Retain `{link}`, `{type}` and `{icon}` placeholders. Each anchor needs a useful accessible name, a visible keyboard focus treatment, at least a 44 by 44 CSS pixel hit area and safe new tab attributes. Keep SVG icons decorative to assistive technology.

SOC 03 Show one row at each breakpoint, outside collapsed footer groups so it stays discoverable on mobile. Avoid text usernames, duplicate account lists and social iframes. Keep phone and email readable in the support area. Use real registration and tax details from merchant data instead of an unverified legal statement.

Acceptance: every configured network opens its correct account; screen readers announce its name; keyboard focus is visible; six icons wrap neatly on a 360 pixel screen.

### CMS Journal and news

CMS 01 Use Salla's existing native blog templates at `src/views/pages/blog/index.twig` and `single.twig`. Preserve current article URLs and category URLs. Atara already has a public blog at https://atara.sa/blog. Retain existing articles and their genuine dates.

CMS 02 Use مجلة أتارا as the customer facing umbrella label. Maintain distinct categories for buying guides, fabric care, styling, prayer essentials and أخبار أتارا. News requires a genuine event or announcement. Do not create fictional openings, collaborations, awards or launches to fill the section. Hide the news category until approved content is published.

CMS 03 Show up to three curated article cards on the homepage after commerce and trust content. Each card has a relevant image, category, meaningful title and short excerpt. Use three columns on desktop and a readable single column on mobile. Avoid auto playing carousels and excessive homepage height. Invalid cards are omitted; an empty selection removes the section and its spacing.

CMS 04 Configure titles, introduction and selected cards through `twilight.json`. The current patch provides a curated link collection. Until a supported article picker or API connection is implemented, the editor must update card title, excerpt and image when the original article changes. For automated selection, validate Salla's native article data contract and never expose an Admin API token in the theme.

CMS 05 The archive needs an always visible H1, category selection with correct expanded state, article cards, pagination and a useful empty state. A featured article must not remove the page H1. The article page needs a title, genuine date, author where supplied, readable body, related content and relevant product links. Retain Salla hooks and configured moderation controls. Add sharing or copy link using supported platform components.

CMS 06 Preserve canonical URLs, native metadata and structured data. Add Article or BlogPosting and breadcrumb data only if the platform does not already emit them. Do not duplicate schema. New announcement dates use actual publication dates; never regenerate them from the current date. Images need intrinsic dimensions and concise alternative text.

Acceptance: publish one guide and one genuine announcement in the test store; select them in the homepage editor; verify archive filtering, detail pages, related links and mobile reading. Test with zero, one and three selected cards, and a missing image. Production content requires editorial approval.

### BRAND Brand story and service pages

BRAND 01 Add an approved About Atara page covering its purpose, products and approach without invented claims or unsupported dates. A short homepage introduction can link to it. Use genuine brand and branch photographs.

BRAND 02 Make branches, contact, FAQ, size guidance, delivery, returns, privacy and terms reachable from the footer. Existing branches, contact, privacy and returns pages should keep their URLs. Size tables must be product specific and distinguish body measurements from garment measurements. Explain fabric stretch, garment length and attached versus separate head covering where relevant.

BRAND 03 The branch page requires verified address, map destination, opening hours, phone and any pickup restrictions. Do not turn the branch listing into a promise of live branch inventory.

Acceptance: no footer destination is `#`, an empty URL or the homepage unless that is its actual purpose. Verify phone, email and map links on a phone.

### PLP and PDP Product discovery and selection

PLP 01 Define which filters apply to each category. Different attributes combine consistently; selected values within one attribute follow the platform's documented logic. Desktop and mobile use the same counts and products. Show filter and sort on one mobile row, followed by removable selections. Give the drawer a persistent Apply action, Clear action and result count.

PDP 01 Show title, price, selected colour, size, availability and purchase action clearly. Selecting a variant updates image, price, SKU and stock through Salla's actual product options. Disable unavailable combinations and provide supported restock notification. Never infer live stock from a static image or copied website price.

PDP 02 Show fit guidance, fabric, opacity, lining, closures, care instructions and garment measurements when supplied. Replace generic content that is inaccurate for the item. Do not claim images have unedited colours unless the photography process supports that statement.

PDP 03 Explain bundle quantities and individual prices before purchase. On mobile, use one fixed purchase bar and enough bottom padding for it and the device safe area. It must not cover the last option, validation message or footer.

Acceptance: test an in stock variant, unavailable variant, differently priced variant, out of stock product and qualifying bundle. A customer can select an item confidently without opening support.

### CART Checkout and payments

CART 01 Cart state and totals must come from Salla. Quantity changes, removal, Undo, coupons, gift wrapping and delivery eligibility must recalculate all visible summaries. Distinguish three product lines from four pieces. Display unit price and line total.

CART 02 Do not apply an informational saving as an additional discount. Use the same shipping threshold and discount eligibility at each step. Show any cash on delivery fee before order confirmation.

PAY 01 Confirm the integration boundary before implementing bespoke checkout screens. The documented Twilight Checkout module does not itself orchestrate all checkout steps or payment submission. Use Salla hosted checkout and supported customisation unless Salla explicitly supports another approach. Do not create a frontend payment form that only resembles a working integration.

PAY 02 Separate declined, pending, cancelled, succeeded and unknown payment states. Pending payments must not invite a second charge. Retry must refresh the authoritative order status first and must not produce duplicate orders. Preserve the cart through a recoverable failure.

Acceptance: test guest checkout, missing address, expired discount, stock change, provider decline, customer cancellation, pending verification and successful payment in Salla's supported test environment. Confirm the final charged total matches the customer summary.

### ORDER Account tracking and returns

ORDER 01 Use supported Salla authentication and OTP. Keep phone entry separate from code verification; support change number, resend, expiry and errors. Phone and code fields remain left to right in Arabic layouts.

ORDER 02 Display real order status, delivery estimate, tracking URL, invoice and support reference. Support delayed, failed and partial shipments. Do not expose another customer's order or invoice through a guessable link.

RETURN 01 Determine eligibility from actual delivery date, policy and item status. An in transit order should show delivery support; eligible delivered products may show return and exchange. Expired eligibility must show the reason and support route.

RETURN 02 Define item selection, reason, evidence, collection arrangements, applicable fees and refund method. After carrier collection, cancellation must be assisted by support or explain the physical item's next destination. Refund tracking uses actual backend status, not a fixed decorative timeline.

Acceptance: test an order before delivery, inside and outside the eligibility window, a partial return and a return after collection. Confirm inventory and money movements through the supported backend.

## Design and accessibility standards

Use official logo artwork, original proportions and clear space. Preserve olive `#606356`, pink `#D09F95`, orange `#F8B14C` and grey `#D6D1CA`; document functional colour extensions. Use the specified Droid Arabic Kufi and Intro fonts only with appropriate licences and supported font delivery. Verify source files rather than assuming screenshots identify a font.

Normal text needs at least 4.5 to 1 contrast and large text at least 3 to 1. Controls, focus and important visual boundaries need appropriate nontext contrast. Avoid small white text on brand pink. Provide visible focus, semantic headings, accessible names, labelled errors, reduced motion support, image dimensions and screen reader announcements for cart changes. Use semantic buttons for interactive footer headings and update expanded state.

Test Arabic RTL and English LTR with real translations. New strings belong in locale files. Existing hard coded Arabic strings remain a separate localisation backlog. Do not claim full bilingual support until they are replaced and tested.

## Salla implementation and source ownership

Retain the Twig theme architecture and supported page names. A React migration is a separate project, not a prerequisite for this revision. Preserve Salla hooks, SDK events, native product options, cart calculations, authentication and merchant settings. All theme assets must be reproducibly built and the compiled public assets must be committed because the Salla portal identifies this as a Twig theme with files copied from GitHub.

Relevant files for this revision are `footer/footer.twig`, `home/atara-journal.twig`, `pages/index.twig`, `pages/partials/atara-real-content.twig`, `pages/partials/atara-defaults.twig`, the Atara SCSS layer, locale JSON files and `twilight.json`. Avoid duplicating data between source defaults and schema values; verify both when editing defaults. Existing saved settings override fallback copy and need a migration checklist.

## Content preparation and responsible owners

| Work | Responsible role | Evidence required |
| --- | --- | --- |
| Theme and supported integrations | Developer | Commit, compiled assets and functional Salla preview |
| Responsive design and states | Designer | Desktop and mobile screens using real data |
| Product catalogue and policies | Atara operations | Verified product facts, prices, eligibility and service promises |
| Articles and real news | Content editor | Approved text, dates, images and category assignments |
| SEO and analytics | SEO or analytics owner | Preserved URLs, metadata and deduplicated events |
| Journey validation | QA | Completed test records with device, result and defects |
| Final release | Atara business owner | Approved content and accepted critical journeys |

Use a test catalogue containing representative Atara products, actual titles, photography, category assignments and variant options. Test product records are snapshots; production prices and stock remain authoritative in the live catalogue. Never import customer accounts, order data or payment credentials just to populate a visual preview.

## Delivery sequence and acceptance evidence

1. Establish the Salla preview for this theme and record its source branch and commit. Verify the canvas renders Atara rather than the default Raed design. Resolve preview or maintenance configuration in the test environment.
2. Validate navigation, real catalogue mapping, imagery, social icons, footer destinations and product options. Remove expired saved promotional text.
3. Configure the journal, create the genuine news category and complete brand and help pages. Verify editorial updates without editing code.
4. Complete checkout, recovery, tracking and return integration through Salla. Validate all money and eligibility calculations against the backend.
5. Run the responsive, accessibility, performance and journey checks. Provide a test log, the exact preview URL, known limitations, rollback procedure and release checklist.

For performance, measure home, collection and product pages on desktop and mobile. Meet Salla's current technical review criteria and aim for LCP at most 2.5 seconds, CLS at most 0.1 and INP at most 200 milliseconds in production field data. These are targets, not measured results. Avoid rendering every product in a long homepage carousel and lazy load below the fold media.

Track view item list, select item, view item, add to cart, begin checkout and purchase without duplicate platform events. Track journal clicks and guide to product clicks separately. Measure checkout completion, payment failures, size related returns and support enquiries after release. Never include personal customer details in analytics event payloads.

Final acceptance requires: a functioning Salla link; correct Atara identity and photographs; zero critical defects in browsing and payment; no dead support links; verified policy copy; editor managed articles; Arabic and mobile checks; and a documented route to restore the prior theme.

## Sources

- Atara live shop, blog, category photography and public footer, inspected 2 November 2026: https://atara.sa and https://atara.sa/blog
- Official social component and slot: https://docs.salla.dev/499802m0
- Official homepage components and settings: https://docs.salla.dev/422558m0
- Official Twig page structure: https://docs.salla.dev/422556m0
- Official cart and checkout integration boundary: https://docs.salla.dev/2129395m0
- Official technical review: https://docs.salla.dev/twilight-engine/technical-review
- Official theme publishing acceptance checklist: https://salla.dev/blog/salla-theme-publishing-acceptance-checklist/
- Accessibility contrast: https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html
