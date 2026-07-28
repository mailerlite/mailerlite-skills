---
name: mailerlite-cli
description: >-
  This skill should be used when the user asks to "manage subscribers", "create a campaign",
  "list automations", "manage groups", "manage forms", "manage segments", "manage fields",
  "manage webhooks", "list timezones", "manage e-commerce shops", "manage products",
  "manage categories", "manage customers", "manage orders", "manage carts", "manage cart items",
  "import e-commerce data", "switch mailerlite account", "configure mailerlite",
  "set up mailerlite profile", "launch the mailerlite dashboard", or any task involving the
  MailerLite email marketing platform via CLI. Provides comprehensive guidance for using the
  `mailerlite` command-line tool.
---

# MailerLite CLI

The MailerLite CLI (`mailerlite`) is a command-line tool and interactive TUI dashboard for the MailerLite email marketing API. It supports managing subscribers, campaigns, automations, groups, forms, segments, fields, webhooks, e-commerce (shops, products, categories, customers, orders, carts), and full account management.

## Check CLI Availability First

Before running any commands, verify the CLI is installed:

```bash
command -v mailerlite
```

If the binary is not available, do not guess at commands. Either offer to install it (see Installation below), or use another available MailerLite interface instead — the MailerLite MCP server, if connected, or the [REST API](https://developers.mailerlite.com/) directly.

## Installation

Install via Homebrew, Nix, or download a binary from GitHub releases:

```bash
# Homebrew
brew install --cask mailerlite/tap/mailerlite

# Nix flake
nix profile install github:mailerlite/mailerlite-cli

# Or download from https://github.com/mailerlite/mailerlite-cli/releases
```

The binary is called `mailerlite`.

## Authentication

Before using the CLI, authenticate with MailerLite:

```bash
# Interactive login (prompts for method — OAuth or API token)
mailerlite auth login

# Direct token login
mailerlite auth login --method token --token "your_token_here"

# Check authentication status
mailerlite auth status
```

### Multi-Profile Support

Manage multiple accounts or tokens with named profiles:

```bash
mailerlite profile add production --token "prod_token"
mailerlite profile add staging --token "staging_token"
mailerlite profile switch production
mailerlite profile list
```

Use `--profile <name>` on any command to override the active profile.

### Multi-Account Support

If your OAuth credentials have access to multiple accounts:

```bash
mailerlite account list
mailerlite account switch <account_id>
```

**Token resolution order:** `MAILERLITE_API_TOKEN` env var > `--profile` flag > active profile > first profile.

Config is stored at `~/.config/mailerlite/config.yaml`.

## Global Flags

These flags work on all commands:

| Flag | Description |
|------|-------------|
| `--profile <name>` | Select config profile |
| `--verbose` / `-v` | Show HTTP request/response details |
| `--json` | Output as machine-readable JSON |
| `--yes` / `-y` | Skip confirmation prompts |

The CLI respects the `NO_COLOR` environment variable.

## Critical: Always Use JSON Output

When executing `mailerlite` commands, **always append `--json`** to every command. JSON output is structured and parseable, making it reliable for extracting IDs, statuses, and other data needed for follow-up commands. The default table output is for human reading only and difficult to parse programmatically.

```bash
# Correct - always use --json
mailerlite subscriber list --json
mailerlite campaign get <id> --json

# Incorrect - table output is hard to parse
mailerlite subscriber list
```

The only exceptions are `dashboard` (interactive TUI), `completion` (shell scripts), and simple write confirmations.

## Core Workflows

### Managing Subscribers

```bash
# List subscribers
mailerlite subscriber list --json
mailerlite subscriber list --status active --email user@example.com --json

# Get subscriber count
mailerlite subscriber count --json

# Get subscriber details (by ID or email)
mailerlite subscriber get user@example.com --json

# Create or update a subscriber
mailerlite subscriber upsert \
  --email "user@example.com" \
  --status active \
  --groups "group_id_1,group_id_2" \
  --fields '{"name":"John","company":"Acme"}' --json

# Update a subscriber
mailerlite subscriber update <id> --status unsubscribed --json

# Delete a subscriber
mailerlite subscriber delete <id>

# Forget a subscriber (GDPR)
mailerlite subscriber forget <id>
```

### Managing Campaigns

```bash
# List campaigns
mailerlite campaign list --json
mailerlite campaign list --status sent --type regular --json

# Get campaign details
mailerlite campaign get <campaign_id> --json

# Create a campaign
mailerlite campaign create \
  --name "Welcome Campaign" \
  --type regular \
  --subject "Welcome!" \
  --from "sender@yourdomain.com" \
  --from-name "Sender Name" \
  --content "<h1>Hello</h1>" \
  --groups "group_id" --json

# Schedule a campaign
mailerlite campaign schedule <campaign_id> \
  --delivery scheduled \
  --date 2026-03-01 \
  --hours 10 \
  --minutes 0

# Cancel a campaign
mailerlite campaign cancel <campaign_id>

# List campaign subscriber activity
mailerlite campaign subscribers <campaign_id> --json

# List available campaign languages
mailerlite campaign languages --json

# Delete a campaign
mailerlite campaign delete <campaign_id>
```

### Managing Groups

```bash
mailerlite group list --json                                    # List groups
mailerlite group create --name "Newsletter" --json              # Create group
mailerlite group update <id> --name "Weekly Newsletter" --json  # Update group
mailerlite group delete <id>                                    # Delete group
mailerlite group subscribers <group_id> --json                  # List subscribers in group
mailerlite group assign <group_id> <subscriber_id>              # Assign subscriber
mailerlite group unassign <group_id> <subscriber_id>            # Unassign subscriber
```

### Managing Automations

```bash
mailerlite automation list --json                       # List automations
mailerlite automation list --enabled true --json        # Filter by enabled
mailerlite automation get <id> --json                   # Get automation details
mailerlite automation subscribers <id> --json           # List subscriber activity
```

### Managing Forms

```bash
mailerlite form list --json                             # List forms
mailerlite form list --type popup --json                # Filter by type
mailerlite form get <id> --json                         # Get form details
mailerlite form update <id> --name "Updated" --json     # Update form
mailerlite form delete <id>                             # Delete form
mailerlite form subscribers <id> --json                 # List form subscribers
```

### Managing Fields

```bash
mailerlite field list --json                            # List subscriber fields
mailerlite field create --name "Company" --type text --json  # Create field
mailerlite field update <id> --name "Organization" --json    # Update field
mailerlite field delete <id>                            # Delete field
```

### Managing Segments

```bash
mailerlite segment list --json                          # List segments
mailerlite segment update <id> --name "VIP" --json      # Update segment
mailerlite segment delete <id>                          # Delete segment
mailerlite segment subscribers <id> --json              # List subscribers
```

### Managing Webhooks

```bash
mailerlite webhook list --json                          # List webhooks
mailerlite webhook get <id> --json                      # Get webhook details
mailerlite webhook create \
  --name "My Webhook" \
  --url "https://example.com/webhook" \
  --events "subscriber.created,campaign.sent" \
  --enabled --json                                      # Create webhook
mailerlite webhook update <id> --name "Updated" --json  # Update webhook
mailerlite webhook delete <id>                          # Delete webhook
```

### E-Commerce: Shops

```bash
mailerlite shop list --json                             # List shops
mailerlite shop get <id> --json                         # Get shop details
mailerlite shop create --name "My Store" --url "https://mystore.com" --json
mailerlite shop update <id> --name "Updated" --json     # Update shop
mailerlite shop delete <id>                             # Delete shop
mailerlite shop count --json                            # Get shop count
```

### E-Commerce: Products

All product commands require `--shop <shop_id>`.

```bash
mailerlite product list --shop <shop_id> --json
mailerlite product get <product_id> --shop <shop_id> --json
mailerlite product create --shop <shop_id> \
  --name "T-Shirt" --price 29.99 \
  --url "https://mystore.com/tshirt" --json
mailerlite product update <product_id> --shop <shop_id> --price 24.99 --json
mailerlite product delete <product_id> --shop <shop_id>
mailerlite product count --shop <shop_id> --json
```

### E-Commerce: Categories

All category commands require `--shop <shop_id>`.

```bash
mailerlite category list --shop <shop_id> --json
mailerlite category get <id> --shop <shop_id> --json
mailerlite category create --shop <shop_id> --name "Apparel" --json
mailerlite category update <id> --shop <shop_id> --name "Clothing" --json
mailerlite category delete <id> --shop <shop_id>
mailerlite category count --shop <shop_id> --json
mailerlite category products <id> --shop <shop_id> --json
mailerlite category assign-product <id> --shop <shop_id> --product <product_id>
mailerlite category unassign-product <id> --shop <shop_id> --product <product_id>
```

### E-Commerce: Customers

All customer commands require `--shop <shop_id>`.

```bash
mailerlite customer list --shop <shop_id> --json
mailerlite customer get <id> --shop <shop_id> --json
mailerlite customer create --shop <shop_id> \
  --email "customer@example.com" \
  --first-name "John" --last-name "Doe" --json
mailerlite customer update <id> --shop <shop_id> --first-name "Jane" --json
mailerlite customer delete <id> --shop <shop_id>
mailerlite customer count --shop <shop_id> --json
```

### E-Commerce: Orders

All order commands require `--shop <shop_id>`.

```bash
mailerlite order list --shop <shop_id> --json
mailerlite order get <id> --shop <shop_id> --json
mailerlite order create --shop <shop_id> \
  --customer <customer_id> --status complete \
  --total 59.98 --currency USD \
  --items '[{"product_id":"prod1","quantity":2,"price":29.99}]' --json
mailerlite order update <id> --shop <shop_id> --status complete --json
mailerlite order delete <id> --shop <shop_id>
mailerlite order count --shop <shop_id> --json
```

### E-Commerce: Carts & Cart Items

```bash
# Carts (require --shop)
mailerlite cart list --shop <shop_id> --json
mailerlite cart get <id> --shop <shop_id> --json
mailerlite cart update <id> --shop <shop_id> --currency EUR --json
mailerlite cart count --shop <shop_id> --json

# Cart items (require --shop and --cart)
mailerlite cart-item list --shop <shop_id> --cart <cart_id> --json
mailerlite cart-item create --shop <shop_id> --cart <cart_id> \
  --product <product_id> --quantity 2 --price 29.99 --json
mailerlite cart-item update <item_id> --shop <shop_id> --cart <cart_id> --quantity 3 --json
mailerlite cart-item delete <item_id> --shop <shop_id> --cart <cart_id>
mailerlite cart-item count --shop <shop_id> --cart <cart_id> --json
```

### E-Commerce: Bulk Import

```bash
mailerlite import categories --shop <shop_id> --file categories.json --json
mailerlite import products --shop <shop_id> --file products.json --json
mailerlite import orders --shop <shop_id> --file orders.json --json
```

### TUI Dashboard

```bash
mailerlite dashboard
```

Launch an interactive terminal dashboard with sidebar navigation, real-time data, and vim-style keybindings (`j`/`k` to navigate, `Enter` to select, `?` for help, `q` to quit).

## Key Patterns

- **Pagination:** Use `--limit <n>` to control results. `--limit 0` fetches all results.
- **Interactive mode:** Omit required flags and the CLI prompts interactively.
- **JSON output:** Append `--json` to any command for machine-readable output.
- **E-commerce nesting:** Products, categories, customers, orders, and carts are nested under shops via `--shop <shop_id>`. Cart items require both `--shop` and `--cart`.

## Additional Resources

### Reference Files

For the complete command reference with all subcommands and flags, consult:
- **`references/command-reference.md`** - Full command tree for all 20+ command groups with every flag documented
