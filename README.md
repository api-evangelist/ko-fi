# Ko-fi (ko-fi)

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
