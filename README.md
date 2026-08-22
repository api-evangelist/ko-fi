# Ko-fi (ko-fi)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Ko-fi is a creator monetization platform where fans support creators through one-off tips ("buy me a coffee"), recurring memberships, digital and physical shop products, and paid commissions. Ko-fi is best known for charging **0% platform fee on tips and donations**.

**Honest developer-surface note:** Ko-fi does **not** publish a public REST API, GraphQL API, or WebSocket API. Its entire documented developer surface is a single **outbound webhook**. When a payment happens on your Ko-fi page, Ko-fi's servers send an HTTP `POST` to a URL you configure on your [webhooks page](https://ko-fi.com/manage/webhooks). There is no request/response API to read, create, or manage donations, members, orders, or commissions.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/ko-fi/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/ko-fi/refs/heads/main/apis.yml)

## Tags

- Creator Economy
- Donations
- Tips
- Memberships
- Shop
- Payments
- Webhooks
- Creator Monetization

## Timestamps

- **Created:** 2026-07-05
- **Modified:** 2026-07-05

## How the Webhook Works

- Ko-fi sends an HTTP `POST` to your configured URL whenever a payment occurs.
- The request is `application/x-www-form-urlencoded` with a single field named `data` whose value is a **JSON string**.
- The JSON includes a `verification_token` (found on your Ko-fi webhooks page) so you can confirm the request came from Ko-fi and reject spoofed requests.
- A `type` field identifies the event: **Donation**, **Subscription**, **Shop Order**, or **Commission**.
- The webhook fires **only when a payment is made**. Ko-fi documents that it cannot, for example, notify you when a membership *ends* — only when a membership *payment* occurs.
- It is a one-way HTTP webhook — **not** WebSocket, **not** Server-Sent Events.

### Common payload fields

`verification_token`, `message_id`, `timestamp`, `type`, `is_public`, `from_name`, `message`, `amount`, `url`, `email`, `currency`, `is_subscription_payment`, `is_first_subscription_payment`, `kofi_transaction_id`, `tier_name`, `shop_items`, `shipping`.

For **Shop Orders**, `shop_items` is an array of `{ direct_link_code, variation_name, quantity }`, and physical goods include a `shipping` object (`full_name`, `street_address`, `city`, `state_or_province`, `postal_code`, `country`, `country_code`, `telephone`). For **Subscriptions**, `is_subscription_payment` is `true` and `tier_name` names the membership tier.

## APIs

### Ko-fi Webhook

Outbound webhook that Ko-fi HTTP POSTs to a URL you configure whenever a payment happens on your Ko-fi page. A one-way, server-to-endpoint notification, not a readable/queryable REST API.

- **Human URL:** [https://help.ko-fi.com/hc/en-us/articles/360004162298-Does-Ko-fi-have-an-API-or-webhook](https://help.ko-fi.com/hc/en-us/articles/360004162298-Does-Ko-fi-have-an-API-or-webhook)

#### Tags

- Webhooks
- Payments
- Donations
- Memberships
- Shop Orders
- Commissions

#### Properties

- [Documentation](https://help.ko-fi.com/hc/en-us/articles/360004162298-Does-Ko-fi-have-an-API-or-webhook)
- [Console](https://ko-fi.com/manage/webhooks)
- [AsyncAPI](asyncapi/ko-fi-asyncapi.yml) — models the outbound HTTP webhook (not WebSocket)

## Pricing

- **Free:** 0% platform fee on tips and donations; 5% platform fee on memberships, shop sales, and commissions.
- **Ko-fi Gold:** flat monthly subscription (roughly $12/month for new accounts; historically ~$6/month) that removes the 5% platform fee across memberships, shop, and commissions.
- Third-party payment processing fees (~2.9% + $0.30 per transaction via PayPal/Stripe) apply on both plans and are charged by the processor, not by Ko-fi.

See [plans/ko-fi-plans-pricing.yml](plans/ko-fi-plans-pricing.yml) and [finops/ko-fi-finops.yml](finops/ko-fi-finops.yml).

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/ko-fi)
- [Website](https://ko-fi.com)
- [Documentation](https://help.ko-fi.com/hc/en-us/articles/360004162298-Does-Ko-fi-have-an-API-or-webhook)
- [Plans](plans/ko-fi-plans-pricing.yml)
- [Rate Limits](rate-limits/ko-fi-rate-limits.yml)
- [Fin Ops](finops/ko-fi-finops.yml)
- [Blog](https://blog.ko-fi.com)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
