---
name: grocery-budget
description: Estimate what a household's groceries cost per month in Saudi Arabia, and how a basic item's price changed, from the official monthly average prices of the General Authority for Statistics (GASTAT). Use for «كم تكلفة المقاضي الشهرية», «كم سعر الرز/البيض/الدجاج», «هل الأسعار غليت», or building a monthly shopping list with a budget.
---

# Monthly grocery budget from official Saudi prices

## Source

Dukkani republishes GASTAT's monthly «متوسطات أسعار السلع والخدمات» (Kingdom average, VAT included) as an open file:

- CSV: `https://dukkanlink.com/app/asaar/asaar.csv` (UTF-8). Columns: `slug, item_ar, unit_ar, category_ar, month, avg_price_sar`, one row per item per month.
- Readable pages: `https://dukkanlink.com/app/asaar/` (every item) and `https://dukkanlink.com/app/taklifat-almaqadi/` (a ready monthly basket for a family of 5, with a calculator).

Fetch the CSV with your web fetch tool when you need numbers. It is a public file; nothing about the user is sent.

## Steps

1. **Get the user's list and household size.** If they only ask «كم تكلفة المقاضي», start from the example basket on the basket page and say it is an example.
2. **Match each line to an item** in the CSV by its Arabic name and unit (e.g. «رز بسمتي 10 كيلو» → the basmati row in «١٠ كجم»). Convert quantities to the CSV unit (5 kg of rice when the row is 10 kg = 0.5 units). If an item is not in the data, say so and leave it out of the total; don't estimate it.
3. **Compute** with the latest month in the file: line cost = units × `avg_price_sar`, then the total. Do the arithmetic in code when available.
4. **Compare** when useful: the same basket with the month a year earlier, and the 2–3 items that moved the total most in riyals.
5. **Answer** with the total first, then a short table (item · units · price · line cost), the data month, and one line on the source.

## Honesty rules

- These are national averages; a shop's price can differ by city and store. Say it once.
- Quantities you or the user chose are not official figures; never call the total an official index.
- Name the data month exactly (e.g. «سبتمبر 2026»), and don't present it as today's price if the month is older.
- Link `https://dukkanlink.com/app/taklifat-almaqadi/` so the user can adjust quantities themselves.
