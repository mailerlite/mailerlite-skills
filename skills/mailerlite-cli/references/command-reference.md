# MailerLite CLI Complete Command Reference

## Global Flags

| Flag | Description |
|------|-------------|
| `--profile <name>` | Select config profile |
| `--verbose` / `-v` | Show HTTP request/response details |
| `--json` | Machine-readable JSON output |
| `--yes` / `-y` | Skip confirmation prompts |

---

## auth - Authentication

### `auth login`

Authenticate via API token or OAuth browser flow.

| Flag | Description |
|------|-------------|
| `--method <token\|oauth>` | Authentication method |
| `--token <token>` | API token (for token method) |
| `--profile <name>` | Profile name to save credentials to |

### `auth logout`

Log out and remove stored credentials.

### `auth status`

Show current authentication status.

---

## profile - Profile Management

### `profile add <name>`

Add a new profile.

| Flag | Description |
|------|-------------|
| `--token <token>` | API token for this profile |

### `profile list`

List all profiles.

### `profile switch <name>`

Switch active profile.

### `profile remove <name>`

Remove a profile.

---

## account - Account Management

### `account list`

List accounts you have access to.

### `account switch [account_id]`

Switch to a different account. Interactive picker if no ID provided. Validates that the account ID exists in your account list.

---

## subscriber - Subscribers

### `subscriber list`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max subscribers to return (default: 25, 0 = all) |
| `--status <status>` | Filter: active, unsubscribed, unconfirmed, bounced, junk |
| `--email <email>` | Filter by email |

### `subscriber count`

Get total subscriber count.

### `subscriber get <id_or_email>`

Get subscriber details. Accepts subscriber ID or email address.

### `subscriber upsert`

Create or update a subscriber.

| Flag | Required | Description |
|------|----------|-------------|
| `--email <email>` | Yes | Subscriber email |
| `--status <status>` | | Subscriber status |
| `--groups <ids>` | | Comma-separated group IDs |
| `--fields <json>` | | JSON object of field key-value pairs |

### `subscriber update <id>`

| Flag | Description |
|------|-------------|
| `--email <email>` | Subscriber email |
| `--status <status>` | Subscriber status |
| `--fields <json>` | JSON object of field key-value pairs |

### `subscriber delete <id>`

Delete a subscriber.

### `subscriber forget <id>`

Forget a subscriber (GDPR compliance).

---

## group - Groups

### `group list`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max groups to return (default: 25, 0 = all) |
| `--sort <field>` | Sort field |

### `group create`

| Flag | Required | Description |
|------|----------|-------------|
| `--name <name>` | Yes | Group name |

### `group update <group_id>`

| Flag | Description |
|------|-------------|
| `--name <name>` | Group name |

### `group delete <group_id>`

Delete a group.

### `group subscribers <group_id>`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max subscribers (default: 25) |

### `group assign <group_id> <subscriber_id>`

Assign a subscriber to a group.

### `group unassign <group_id> <subscriber_id>`

Unassign a subscriber from a group.

---

## campaign - Campaigns

### `campaign list`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max campaigns (default: 25, 0 = all) |
| `--status <status>` | Filter: draft, ready, queued, sending, sent |
| `--type <type>` | Filter: regular, ab, resend |

### `campaign get <campaign_id>`

Get campaign details.

### `campaign create`

| Flag | Required | Description |
|------|----------|-------------|
| `--name <name>` | Yes | Campaign name |
| `--type <type>` | Yes | Campaign type: regular, ab, resend |
| `--subject <text>` | | Email subject |
| `--from <email>` | | Sender email |
| `--from-name <name>` | | Sender name |
| `--content <html>` | | HTML content |
| `--groups <ids>` | | Comma-separated group IDs |
| `--segments <ids>` | | Comma-separated segment IDs |

### `campaign update <campaign_id>`

Same flags as create, all optional.

### `campaign schedule <campaign_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--delivery <type>` | Yes | instant or scheduled |
| `--date <YYYY-MM-DD>` | | Scheduled date |
| `--hours <0-23>` | | Scheduled hour |
| `--minutes <0-59>` | | Scheduled minute |
| `--timezone-id <id>` | | Timezone ID (see `timezone list`) |

### `campaign cancel <campaign_id>`

Cancel a campaign.

### `campaign subscribers <campaign_id>`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max subscribers (default: 25) |

### `campaign languages`

List available campaign languages.

### `campaign delete <campaign_id>`

Delete a campaign.

---

## automation - Automations

### `automation list`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max automations (default: 25, 0 = all) |
| `--enabled <true\|false>` | Filter by enabled status |

### `automation get <automation_id>`

Get automation details.

### `automation subscribers <automation_id>`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max subscribers (default: 25) |

---

## form - Forms

### `form list`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max forms (default: 25, 0 = all) |
| `--type <type>` | Filter: popup, embedded, promotion |
| `--sort <field>` | Sort field |

### `form get <form_id>`

Get form details.

### `form update <form_id>`

| Flag | Description |
|------|-------------|
| `--name <name>` | Form name |

### `form delete <form_id>`

Delete a form.

### `form subscribers <form_id>`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max subscribers (default: 25) |

---

## field - Subscriber Fields

### `field list`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max fields (default: 25, 0 = all) |
| `--sort <field>` | Sort field |

### `field create`

| Flag | Required | Description |
|------|----------|-------------|
| `--name <name>` | Yes | Field name |
| `--type <type>` | Yes | Field type: text, number, date |

### `field update <field_id>`

| Flag | Description |
|------|-------------|
| `--name <name>` | Field name |

### `field delete <field_id>`

Delete a field.

---

## segment - Segments

### `segment list`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max segments (default: 25, 0 = all) |

### `segment update <segment_id>`

| Flag | Description |
|------|-------------|
| `--name <name>` | Segment name |

### `segment delete <segment_id>`

Delete a segment.

### `segment subscribers <segment_id>`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max subscribers (default: 25) |

---

## webhook - Webhooks

### `webhook list`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max webhooks (default: 25, 0 = all) |
| `--sort <field>` | Sort field |

### `webhook get <webhook_id>`

Get webhook details.

### `webhook create`

| Flag | Required | Description |
|------|----------|-------------|
| `--name <name>` | Yes | Webhook name |
| `--url <url>` | Yes | Webhook URL |
| `--events <events>` | Yes | Comma-separated event types |
| `--enabled` | | Enabled (default: true) |

Valid events: `subscriber.created`, `subscriber.updated`, `subscriber.unsubscribed`, `subscriber.added_to_group`, `subscriber.removed_from_group`, `subscriber.bounced`, `subscriber.automation_triggered`, `subscriber.automation_completed`, `campaign.sent`, `campaign.draft_created`

### `webhook update <webhook_id>`

| Flag | Description |
|------|-------------|
| `--name <name>` | Webhook name |
| `--url <url>` | Webhook URL |
| `--events <events>` | Event types |
| `--enabled` | Enabled |

### `webhook delete <webhook_id>`

Delete a webhook.

---

## timezone - Timezones

### `timezone list`

List available timezones. Use timezone IDs with `campaign schedule --timezone-id`.

---

## shop - E-Commerce Shops

### `shop list`

| Flag | Description |
|------|-------------|
| `--limit <n>` | Max shops (default: 25, 0 = all) |

### `shop get <shop_id>`

Get shop details.

### `shop create`

| Flag | Required | Description |
|------|----------|-------------|
| `--name <name>` | Yes | Shop name |
| `--url <url>` | Yes | Shop URL |

### `shop update <shop_id>`

| Flag | Description |
|------|-------------|
| `--name <name>` | Shop name |
| `--url <url>` | Shop URL |

### `shop delete <shop_id>`

Delete a shop.

### `shop count`

Get total shop count.

---

## product - E-Commerce Products

All commands require `--shop <shop_id>`.

### `product list`

| Flag | Description |
|------|-------------|
| `--shop <id>` | Shop ID (required) |
| `--limit <n>` | Max products (default: 25, 0 = all) |

### `product get <product_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

### `product create`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--name <name>` | Yes | Product name |
| `--price <price>` | | Product price (default: 0) |
| `--url <url>` | | Product URL |
| `--image-url <url>` | | Product image URL |
| `--description <text>` | | Product description |
| `--quantity <n>` | | Product quantity |

### `product update <product_id>`

Same flags as create, all optional (except `--shop`).

### `product delete <product_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

### `product count`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

---

## category - E-Commerce Categories

All commands require `--shop <shop_id>`.

### `category list`

| Flag | Description |
|------|-------------|
| `--shop <id>` | Shop ID (required) |
| `--limit <n>` | Max categories (default: 25, 0 = all) |

### `category get <category_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

### `category create`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--name <name>` | Yes | Category name |

### `category update <category_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--name <name>` | | Category name |

### `category delete <category_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

### `category count`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

### `category products <category_id>`

List products in a category.

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

### `category assign-product <category_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--product <id>` | Yes | Product ID |

### `category unassign-product <category_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--product <id>` | Yes | Product ID |

---

## customer - E-Commerce Customers

All commands require `--shop <shop_id>`.

### `customer list`

| Flag | Description |
|------|-------------|
| `--shop <id>` | Shop ID (required) |
| `--limit <n>` | Max customers (default: 25, 0 = all) |

### `customer get <customer_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

### `customer create`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--email <email>` | Yes | Customer email |
| `--first-name <name>` | | First name |
| `--last-name <name>` | | Last name |

### `customer update <customer_id>`

Same flags as create, all optional (except `--shop`).

### `customer delete <customer_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

### `customer count`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

---

## order - E-Commerce Orders

All commands require `--shop <shop_id>`.

### `order list`

| Flag | Description |
|------|-------------|
| `--shop <id>` | Shop ID (required) |
| `--limit <n>` | Max orders (default: 25, 0 = all) |

### `order get <order_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

### `order create`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--customer <id>` | Yes | Customer ID |
| `--status <status>` | Yes | Order status (pending, complete) |
| `--total <amount>` | | Order total (default: 0) |
| `--currency <code>` | | Currency code (default: USD) |
| `--items <json>` | | JSON array of order items |

### `order update <order_id>`

Same flags as create, all optional (except `--shop`).

### `order delete <order_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

### `order count`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

---

## cart - E-Commerce Carts

All commands require `--shop <shop_id>`.

### `cart list`

| Flag | Description |
|------|-------------|
| `--shop <id>` | Shop ID (required) |
| `--limit <n>` | Max carts (default: 25, 0 = all) |

### `cart get <cart_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

### `cart update <cart_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--customer <id>` | | Customer ID |
| `--currency <code>` | | Currency code |

### `cart count`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |

---

## cart-item - E-Commerce Cart Items

All commands require `--shop <shop_id>` and `--cart <cart_id>`.

### `cart-item list`

| Flag | Description |
|------|-------------|
| `--shop <id>` | Shop ID (required) |
| `--cart <id>` | Cart ID (required) |
| `--limit <n>` | Max items (default: 25, 0 = all) |

### `cart-item get <item_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--cart <id>` | Yes | Cart ID |

### `cart-item create`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--cart <id>` | Yes | Cart ID |
| `--product <id>` | Yes | Product ID |
| `--quantity <n>` | | Quantity (default: 1) |
| `--price <amount>` | | Price (default: 0) |

### `cart-item update <item_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--cart <id>` | Yes | Cart ID |
| `--quantity <n>` | | Quantity |
| `--price <amount>` | | Price |

### `cart-item delete <item_id>`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--cart <id>` | Yes | Cart ID |

### `cart-item count`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--cart <id>` | Yes | Cart ID |

---

## import - Bulk Import

### `import categories`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--file <path>` | Yes | Path to JSON file |

### `import products`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--file <path>` | Yes | Path to JSON file |

### `import orders`

| Flag | Required | Description |
|------|----------|-------------|
| `--shop <id>` | Yes | Shop ID |
| `--file <path>` | Yes | Path to JSON file |

---

## dashboard - TUI Dashboard

### `dashboard`

Launch interactive terminal dashboard.

**Keybindings:**
- `j`/`k` - Navigate up/down
- `Enter` - Select/view details
- `?` - Show help overlay
- `q` - Quit

**Views:** Subscribers, Campaigns, Automations, Groups, Forms

---

## version

Print CLI version, commit hash, and build date.

---

## completion <shell>

Generate shell completion scripts.

Valid shells: `bash`, `zsh`, `fish`, `powershell`

```bash
# Example: add to shell config
mailerlite completion fish > ~/.config/fish/completions/mailerlite.fish
mailerlite completion zsh > ~/.zsh/completions/_mailerlite
```
