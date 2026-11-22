# Record fields

What the two record tools return, checked against live results in November 2026.

## A search card (`search_met_artworks`)

The result starts with a count, such as "127 objects in The Met collection match cat, showing 4." Each card then has:

| Line | Meaning | Notes |
| --- | --- | --- |
| Title (maker label) | The object's title, then a label in parentheses | The label is an artist when one is recorded. Otherwise it can be a culture ("American"), a period ("New Kingdom") or "Unknown maker" |
| `Date` | Date or date range as the museum writes it | Can include "ca.", a span of years, "BCE", "dated 1549", "18th century". The line is missing when the record has no date |
| `Medium` | Materials and technique | The museum's wording. A long line can be cut short with an ellipsis on a card |
| `Department` | Curatorial department | See `departments.md` for name differences |
| Collection link | The object's page on metmuseum.org | The number at the end is the object id |

A card does not include the gallery, dimensions, credit line or image link.

## A full record (`get_met_artwork`)

Everything on the card, plus:

| Line | Meaning | When it is missing |
| --- | --- | --- |
| `Artist` | Name, nationality and life dates or places as recorded | No individual artist is recorded. The maker label then carries a culture or period |
| `Dimensions` | Size as the museum writes it, usually in both inches and centimetres | Not recorded |
| `Credit` | The credit line: how the object entered the collection | Not recorded |
| `Gallery` | Gallery number where the object is installed | The collection data does not place the object in a gallery. Treat it as not on view |
| `Image (public domain)` | Link to an image file | The museum has not marked the object as public domain, or there is no image |
| `Object id` | The id to use with `get_met_artwork` | Always present |
| Collection link | The object page | Always present |

## Reading the fields correctly

- **Object id.** A whole number. It is not the accession number printed on museum labels, and the service does not return accession numbers.
- **Gallery.** Text, not a number: it can have leading zeros (a Cloisters record returned `017`). Quote it as given. It is a number only, with no building, floor or wing.
- **On view.** There is no separate on view line. A `Gallery` line is the sign that the data places the object in a gallery. The `on_view` search filter asks the collection data for objects currently on view.
- **Public domain image.** The label "public domain" is the museum's Open Access marking for that object. When the line is absent, link the object page and do not link, embed or describe an image as free to reuse.
- **Maker label versus artist.** The first line of a full record reads "<title> by <maker label>". When the label is a period or culture this sentence is just a template. Do not repeat it as if a person made the object.
- **Titles can contain markup.** Some titles include italic tags around a foreign term. Render them as italics or drop the tags.
- **Dates before the common era** are written with BCE. Keep the museum's form and do not convert a range to a single year.
- **Attribution words** such as "attributed to", "workshop of", "after" and "copy after" change who made the object. Keep them.

## What no tool returns

Descriptive or catalog text, wall label text, provenance, exhibition history, bibliography, accession number, subject tags, related objects, valuation, opening hours, ticketing, maps, routes and current exhibitions. If a visitor asks for any of these, say the service does not provide it and point to the object page.
