---
name: build-a-gallery-tour
description: "Plan a short themed tour of The Metropolitan Museum of Art from live collection records, with a gallery number and one thing to look for at each stop. Use when someone says plan my Met visit, three stops about cats in Egyptian art, a tour for my kids, what should I see at The Met in an hour, a themed walk through the museum, or wants an online tour or lesson built from Met objects."
---

# Build a gallery tour

Turn a theme into a handful of stops, each backed by a collection record the visitor can open.

## When to use

- A visit in person: "three stops on armor for a nine year old", "an hour at The Met, I love textiles".
- An online tour, lesson or slideshow built from Met objects.

For one object or one artist's works use `find-an-artwork`. For "what does this department have" use `explore-a-department`. This skill cannot give opening hours, ticket prices, routes, floor maps or current exhibitions: the service returns collection records only.

## Tools

All three are read only and need no sign in.

| Tool | Use | Arguments that matter |
| --- | --- | --- |
| `search_met_artworks` | Find candidates | `query` (required), `on_view`, `department_id`, `highlights_only`, `has_images` (default true), `limit` (default 6, most 10) |
| `get_met_artwork` | Full record for one object | `object_id` (the number at the end of a result's collection link) |
| `list_met_departments` | Department names and ids | none |

Search cards do not carry the gallery number. Only the full record does, so every stop needs a `get_met_artwork` call.

## Workflow

1. **Settle the brief.** You need the theme, whether the visit is in person or online, and roughly how many stops. If the request leaves these open, assume in person and four stops and say so. Ask one question only when the theme itself is unclear. Note the audience (a child's age, a class, a specialist) because it changes the looking prompts.
2. **Narrow by department when the theme sits in one.** Call `list_met_departments` and pass the matching `department_id`. Do not reuse an id from memory. Skip this for themes that cross departments, such as an animal or a material.
3. **Search with concrete terms.** Call `search_met_artworks` with a subject, object type, artist or culture as `query`, and `limit: 10` so there is something to choose from. For a visit in person set `on_view: true`. Run two or three searches with different terms when a theme has several angles (for cats: `cat`, `lion`, `Bastet`). There is no next page, so a different query is the only way to see more.
4. **Screen the cards.** Keyword matching is broad: a search for an animal can return a work by an artist with that name, and a search for an artist returns works "after" that artist by other hands. Keep cards whose title, maker label, date and medium fit the theme. Details are in [references/search-notes.md](references/search-notes.md).
5. **Open each candidate with `get_met_artwork`.** For a visit in person, keep only records that have a `Gallery` line. Open about twice as many records as you need stops, and stop there.
6. **Choose the stops.** Prefer variety in material, period and scale, and a link to the theme that the record itself supports. Drop any object whose connection rests on a guess.
7. **Order the stops.** For a visit, group them by gallery number so stops in the same gallery come together. Say that this is a grouping by number and not a walking route. For an online tour, order by date or by the argument you are making.
8. **Write the tour** using [references/tour-template.md](references/tour-template.md): title, maker or culture as recorded, date, medium, gallery, the collection link, one thing to look for, and a bridge to the next stop.
9. **Close with the caveats that apply:** gallery locations change, so check the object page on the day; the service has no hours or routing.

Field meanings and the cases where a line is missing are in [references/record-fields.md](references/record-fields.md).

## Writing the looking prompts

- The record gives facts, not a description of how the object looks. Build the prompt from what the record states (material, size, date, title) or phrase it as an open invitation: "Find where the metal has worn smooth."
- For a famous work you may add widely known background, labelled as background. Do not describe details of an object you have no description of.
- A question you cannot answer from the record is fine if it is clearly a question for the visitor.
- For young children: one concrete thing to find, in a short sentence. For adults: one comparison or one question about how it was made or used.
- The maker label on a card can be a culture ("American"), a period or "Unknown maker". Keep it that way. Never turn it into an artist's name.

## Empty or thin results

- **Nothing on view:** try a broader term, then drop `department_id`. If still empty, say that no matching object is recorded as on view and offer an online tour with `on_view` left off.
- **Too few results overall:** set `has_images: false`. The default hides records without images.
- **"No objects in The Met collection match":** check spelling, try the singular, a synonym or the culture instead of the object type.
- **A record without a `Gallery` line:** the collection data does not place it in a gallery. Use it for an online tour only.
- **"No Met object with id":** the id is wrong or withdrawn. Go back to search.
- **Tool failure:** say so and retry once. Never fill a stop from memory with an invented gallery number.

## Limits to state honestly

- Records come from The Met's Open Access collection data through an OpZero service. The plugin is not affiliated with or endorsed by The Metropolitan Museum of Art. See [references/data-source.md](references/data-source.md).
- "On view" and gallery numbers are what the collection data says at the time of the call. Objects rotate, travel on loan and galleries close.
- Works in The Cloisters department are at The Met Cloisters, a separate site from the Fifth Avenue building. Do not mix them into one visit without saying so.
- Image links appear only for objects the museum marks as public domain.

## Examples

**"Plan three stops around cats in Egyptian art. Pick works on view and give my six year old one thing to look for at each stop."**
Call `list_met_departments` and find Egyptian Art. Search `cat` with that `department_id`, `on_view: true`, `limit: 10`. Open several records, keep three with gallery numbers and different materials or sizes, order by gallery, and give one short "can you find" prompt per stop.

**"An online tour of quilts for my guild, five works."**
Search `quilt` without `on_view`. If results are thin, repeat with `has_images: false`. Open records, choose five that differ in date and technique as stated in the medium line, order by date, and include the public domain image link where the record gives one.

**"What should I see in an hour?"**
The theme is open. Ask one question about what they enjoy, or offer two or three themes. For highlights of a single department, hand over to `explore-a-department`.
