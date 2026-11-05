# Dukkani دكّاني — Saudi neighbourhood groceries for Claude

Dukkani is a Saudi app for neighbourhood groceries (بقالات وتموينات): shoppers find the grocery nearest to them and send it their shopping list on WhatsApp, and grocery owners run their shop from a phone (cashier with barcode, debt book, stock). This plugin teaches Claude to do those jobs well, in Arabic or English.

## What it adds

| Skill | What Claude does with it |
| - | - |
| `nearby-grocery` | Finds groceries by Saudi city and district (about 3,000 in 70+ cities), shows which ones customers recently confirmed open, and turns a shopping list into a ready order page the user sends on WhatsApp. |
| `grocery-budget` | Estimates a household's monthly grocery cost, and how an item's price changed, from the official monthly average prices of the General Authority for Statistics (GASTAT). |
| `grocery-owner` | Helps a grocery owner organise sales, credit customers and workers, and points to Dukkani to try it without an account. |

It also connects the **Dukkani MCP server** (`https://dukkanlink.com/mcp`), the same server as the Dukkani connector in the Claude directory. Its tools are read-only: `find_groceries`, `prepare_grocery_order`, `list_cities`, `dukkani_for_shop_owners`.

## What it sends and fetches

- **To the Dukkani MCP server** (`dukkanlink.com/mcp`): the city or district the user asks about, the coordinates only if the user shares them, and the shopping-list lines when preparing an order. No account, name or phone number is needed. Nothing is sent to any grocery: the user opens the order page and sends it on WhatsApp themselves.
- **From `dukkanlink.com/app/asaar/asaar.csv`** (public file, `grocery-budget` only): GASTAT's monthly average prices, fetched with Claude's web fetch tool. Nothing about the user is sent.
- The plugin has no hooks, runs no local code and stores nothing.

Privacy policy: https://dukkanlink.com/privacy · Support: contact@dukkanlink.com · More: https://dukkanlink.com/app/claude/

## Install

In Claude (chat and Cowork), add it from the directory. In Claude Code:

```
/plugin install dukkani --marketplace suhaH5/dukkani-plugin
```

## Examples

- «وين أقرب بقالة في حي النهضة بعفيف؟ وأبي أرسل لها: 2 حليب، كرتون بيض، رز 10 كيلو»
- "How much do monthly groceries cost for a family of five in Saudi Arabia?"
- «عندي بقالة وأبي برنامج كاشير ودفتر ديون على الجوال»

## Notes

The grocery directory comes from public listings and may be out of date; Claude says so and never invents opening hours, phone numbers or prices. Prices are Kingdom averages including VAT, so a store's price can differ.

License: MIT.
