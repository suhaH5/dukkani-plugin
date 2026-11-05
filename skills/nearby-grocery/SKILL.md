---
name: nearby-grocery
description: Find the nearest neighbourhood grocery (بقالة / تموينات) in a Saudi city or district and turn the user's shopping list into a ready WhatsApp order for it. Use when someone in Saudi Arabia asks for «أقرب بقالة», a grocery in a حي, whether a grocery is open, or wants to send a قائمة مقاضي to a nearby shop.
---

# Nearby grocery and shopping-list order (Saudi Arabia)

Uses the Dukkani connector tools: `find_groceries`, `prepare_grocery_order`, `list_cities`.

## Steps

1. **Know where.** You need a city, and ideally the district (حي). Use the Arabic names when the user gives them («النهضة»، «عفيف»). If the user shared coordinates, pass `latitude` and `longitude`. Never guess a district the user did not name; ask one short question instead.
2. **Find.** Call `find_groceries` with `city` and `district` (or coordinates), `limit` 5–8. If nothing comes back, call `list_cities` and offer the closest city that exists, or ask for a nearby district.
3. **Show** at most 5 groceries: name, district, distance when known, and its `map_url`. Groceries with `on_dukkani=true` take orders inside Dukkani, so list them first, as returned.
   - `open` is customers' confirmations from the last 3 hours, not opening hours. Say it only as «أكّدها زبون مفتوحة قبل m دقيقة»; when it is `null`, say nobody confirmed recently. Never invent opening hours, phone numbers or prices.
   - When the user wants the closest one to where they stand right now, or asks if one is open, also give `nearest_url` (the live radar).
4. **Order.** When the user has a list, clean it into one item per line with quantity and size when they said it («2 حليب المراعي 1 لتر», «رز بسمتي 10 كيلو»). Call `prepare_grocery_order` with the grocery's `id` and the lines, plus any `note` («التوصيل بعد العصر»).
5. **Hand over.** Give the returned `order_url` exactly as returned and say plainly: the page opens with the list written, the user checks it and sends it to the grocery on WhatsApp themselves. Nothing is sent by Claude or by the tool.

## Tone

- Reply in the user's language; for Arabic, plain Saudi dialect («أقرب بقالة لك»، «اطلب منها»).
- The directory may be out of date: say so in one line when a grocery looks closed or moved, and offer the `more_url` page.
- Don't rank groceries as better or worse, and don't compare their prices.
