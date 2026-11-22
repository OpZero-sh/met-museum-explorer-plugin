---
name: explore-a-department
description: "Browse The Met by curatorial department: list the departments, then surface highlights or works on view in one of them. Use when someone asks what departments The Met has, what are the highlights of Egyptian Art, what is in Arms and Armor, show me the best of the Asian Art collection, where do I start with Greek and Roman, or wants an overview of one part of the museum before choosing what to see."
---

# Explore a department

Give a visitor a grounded first look at one department of The Metropolitan Museum of Art.

## When to use

- "What departments does The Met have?"
- "What are the highlights in Egyptian Art?" "What's on view in Musical Instruments?"
- "I only have time for one wing. Help me pick."

For a planned sequence of stops use `build-a-gallery-tour`. For a specific object or artist use `find-an-artwork`.

## Workflow

1. **List the departments.** Call `list_met_departments`. It takes no arguments and returns each department with its id. Use the ids from this call, not from memory.
2. **If the person only asked what departments exist,** give the list as returned and stop. Offer to look inside one.
3. **Match the request to a department.** People say "Egypt", "armor", "fashion" or "modern". Map these to a department on the list and say which one you chose. When two could fit, name both and ask, or search both.
4. **Search inside it.** `search_met_artworks` always needs a `query`. It refuses an empty or wildcard query. For a broad look use a word that fits the whole department, such as the culture, material or object type in its name (`Egyptian`, `armor`, `violin`, `photograph`). Then add:
   - `department_id`: the id from step 1.
   - `highlights_only: true`: for "highlights", "best of" or "must see". This uses the museum's own highlight marking.
   - `on_view: true`: when they plan to visit.
   - `limit: 10`.
5. **Run a second and third query with different words** to cover more of the department: another object type, a period, a material. One query shows at most ten cards and there is no next page.
6. **Check the `Department` line on every card.** Drop any card from another department. Records sometimes name the department differently from the list. The known differences are in `../build-a-gallery-tour/references/departments.md`.
7. **Present a short survey.** Group the cards by object type or period. For each work give the title, maker label, date, medium and link. Say how many records each query matched and that you are showing a sample.
8. **Offer the next step:** open any record for its gallery and image, or build a tour from the ones they like.

Open a record with `get_met_artwork` only for the works the person picks, or for the few you recommend when they ask where things are. A survey does not need every record opened.

## Saying it accurately

- "Highlights" means objects the museum has marked as highlights in its data. It is not a ranking, and this plugin adds no judgment of its own. Do not call a work the most famous or most valuable.
- A survey built from a few keyword searches is a sample. Say "among the highlights the search returned" and not "the highlights are".
- The maker label can be a culture or period. Keep it as recorded.
- Search cards do not show galleries. Do not state where something is until you have opened its record.
- Works in The Cloisters department are at The Met Cloisters, a separate site.

## Empty results and errors

- **Nothing with `highlights_only`:** the keyword may be too narrow. Try a broader word for the department, then drop `highlights_only` and say that the results are no longer limited to marked highlights.
- **Nothing with `on_view`:** drop it and say that the works shown are in the collection and may not be in the galleries.
- **Cards from other departments appear:** the id was wrong or not on the list. Call `list_met_departments` again and use the id exactly.
- **"Please give something to search for":** supply a real keyword.
- **Tool failure:** say so and retry once. Do not list department contents from memory as if they were search results.

## Limits to state honestly

Records come from The Met's Open Access collection data through an OpZero service. The plugin is not affiliated with or endorsed by The Metropolitan Museum of Art. The service has no floor plans, hours, exhibition listings or visitor counts, and it cannot list every object in a department.

More detail is in the reference files beside the `build-a-gallery-tour` skill: `../build-a-gallery-tour/references/search-notes.md` for search behaviour, `../build-a-gallery-tour/references/record-fields.md` for field meanings and `../build-a-gallery-tour/references/data-source.md` for the source and rights.

## Examples

**"What are the highlights of Arms and Armor that I can see today?"**
Call `list_met_departments` and find Arms and Armor. Search `armor` with that `department_id`, `highlights_only: true`, `on_view: true`, `limit: 10`. Search again with `sword` and `helmet`. Present the cards grouped by type, with the match counts, and offer to open records for gallery numbers.

**"What departments are there?"**
Call `list_met_departments` and give the list. Ask which one they would like to look into.

**"Show me the best of modern art."**
The list has a department for modern art, and its records carry a slightly different department name. Search within its id with `highlights_only: true` using two or three broad words such as `painting` and `sculpture`. Note that many modern works have no public domain image link.
