---
name: load-supplier-price-list
description: Load a supplier's price list or contract (a PDF, a spreadsheet, a web page the user opened) into itinovo as the supplier with its rates by season, room, board and occupancy. Use when the user attaches or pastes a supplier's prices and wants them in itinovo.
---

# Loading a supplier's price list

## How itinovo holds a supplier

- **A hotel** (also from a bed bank) is a supplier of category `hotel`, type `direct`, with its stars,
  description, amenities and address. Each combination of **room type, board and occupancy** is one of
  its **rates**, with its validity dates. A hotel has no products.
- **Products** are the catalogue of a **tour operator or DMC**: its tours, excursions and packages.
  Never turn a hotel's rooms into products.

## Steps

1. **Read the whole source** and list the rates: room, board (RO, BB, HB, FB, AI), occupancy (single,
   double, triple, quad), season and dates (YYYY-MM-DD), price, unit (per night, per person…),
   currency (ISO code), supplements, minimum stay, cancellation terms.
2. **Load in one call** with `import_supplier`: the supplier's card and its rates (and products for a
   tour operator or DMC). Large lists go in several calls: loading again updates what is there and
   never doubles it.
3. **Report from the result card**: what was created, updated and left out, and why. For each row left
   out, say what is missing (often the price) and ask the user for it.

## Rules

- Give every field the source has and leave out what it does not say: never invent a price, a date or a code.
- Write descriptions in your own words; prices, codes and cancellation terms go in as they are.
- Photos are not loaded through Claude: the agency uploads them in the app (the supplier's card, Media tab).
- Load only what the agency has the right to use, one source at a time, on the user's request.
