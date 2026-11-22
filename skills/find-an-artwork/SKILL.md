---
name: find-an-artwork
description: "Look up artworks and objects in The Met collection and report what the record says: artist or culture, date, medium, dimensions, credit line, whether it is on view and in which gallery, and a public domain image link when the museum provides one. Use when someone asks does The Met have, find works by an artist, show me the record for object 436524, is it on view, which gallery is it in, can I use this image, compare two works, or needs a citation for a Met object."
---

# Find an artwork

Answer a question about one object, one artist's works or a small set of objects, using live collection records.

## When to use

- "Does The Met have any Vermeers?" "Is the Temple of Dendur on view?" "What is object 436524?"
- "Can I use the image of this painting on my blog?" "Give me a citation for this object."
- "Compare these two works." "Find a few examples of jade carving."

For a sequence of stops use `build-a-gallery-tour`. For a survey of one department use `explore-a-department`. The service does not answer questions about hours, tickets, exhibitions or what an object is worth.

## Workflow

1. **Work out what you have.**
   - An object id or a metmuseum.org collection link: the id is the number at the end of the link. Go to step 3.
   - A title, artist, subject or object type: go to step 2.
2. **Search.** Call `search_met_artworks` with the most specific words as `query`: an artist's surname, a title word, an object type. Useful arguments:
   - `limit`: up to 10. Use 10 when the person wants a list.
   - `on_view: true`: only when they ask what they can see in the galleries now.
   - `has_images: false`: when the default search comes back thin. The default hides records without images.
   - `department_id`: when a name is common across departments. Get the id from `list_met_departments`.
   Read the count line. "34 objects match, showing 10" means you are showing a sample, and there is no next page.
3. **Open the record.** Call `get_met_artwork` with `object_id`. Do this before stating a gallery, dimensions, a credit line or an image link, because search cards do not carry them.
4. **Answer the question that was asked,** then give the collection link. Typical answers:
   - *Is it on view?* If the record has a `Gallery` line, say the collection data places it in that gallery today and that this can change. If not, say the data does not place it in a gallery.
   - *Can I use the image?* If the record has an `Image (public domain)` line, give the link and say the museum marks this object as public domain under its Open Access policy. If not, say the museum has not marked it as public domain, give the object page, and do not supply an image link from anywhere else.
   - *Who made it?* Give the `Artist` line if present. If the record has only a maker label that names a culture or period, say that no individual artist is recorded.
   - *A citation:* build it from record fields only, as shown in `../build-a-gallery-tour/references/data-source.md`.
5. **For a list,** give each work as title, maker label, date, medium and link, in the order returned, and say how many matched in total.
6. **For a comparison,** open both records and set the same fields side by side: maker, date, medium, dimensions, department, gallery. Say what the records show to be alike and different. Anything about style or meaning beyond the records must be labelled as background or as a question.

## Disambiguation

- **Several works share a title** (many are called "Untitled" or simply name an object type). List the candidates with date and medium and ask which one, unless one clearly fits.
- **Works "after" an artist.** A search for a painter also returns copies and prints after that painter by other people. Separate them when listing an artist's works.
- **Attribution words** such as "attributed to" or "workshop of" stay in the answer.
- **A culture or period in the maker label** is not a person. Do not write "by New Kingdom".

## Empty results and errors

- **"No objects in The Met collection match":** try another spelling, the surname alone, the singular, or a broader term. Then try `has_images: false`. If still nothing, say the search found no record. Do not conclude that the museum has never held such a work, since search matching is keyword based.
- **"No Met object with id":** check the digits with the person. Ids are whole numbers.
- **"Please give something to search for":** the query was empty or a wildcard. Use a real keyword.
- **A well known work does not appear with `on_view: true`:** repeat without the filter. It may be in the collection and off view.
- **Tool failure:** say so and retry once. Do not answer from memory with a gallery number or an image link.

## What the answer should look like

Lead with the direct answer in one sentence. Then the record as a short list: title, artist or maker label, date, medium, dimensions, credit line, gallery if present, object id, link. Add the image link only when the record has one and it helps. Close with one line on freshness when a gallery is mentioned.

Shared reference files live beside the `build-a-gallery-tour` skill:

- `../build-a-gallery-tour/references/record-fields.md`: every line of a card and a record, and what a missing line means.
- `../build-a-gallery-tour/references/search-notes.md`: how search matches, its limits and how to pick query terms.
- `../build-a-gallery-tour/references/departments.md`: department ids and names.
- `../build-a-gallery-tour/references/data-source.md`: the data source, image rights and a citation pattern.

## Limits to state honestly

Records come from The Met's Open Access collection data through an OpZero service. The plugin is not affiliated with or endorsed by The Metropolitan Museum of Art. The service returns facts from the record and no descriptive text, provenance or valuation. Gallery data is a snapshot.

## Examples

**"Is Van Gogh's Sunflowers at The Met on view, and can I use a picture of it?"**
Search `Van Gogh sunflowers`, open the matching record, report the gallery line and the public domain image line if each is present, and add that locations can change.

**"Show me what The Met has by Jackson Pollock."**
Search `Jackson Pollock` with `limit: 10`. List the cards and give the total count. If asked for an image of one, open its record. If there is no public domain image line, say so and give the object page.

**"What is object 552027?"**
Call `get_met_artwork` with `object_id: 552027` and report the record. The maker label is a period, so say no individual artist is recorded.
