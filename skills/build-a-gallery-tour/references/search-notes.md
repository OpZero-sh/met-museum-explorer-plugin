# Search notes

How `search_met_artworks` behaves, from live calls in November 2026.

## Arguments

| Argument | Default | Effect |
| --- | --- | --- |
| `query` | required | Keywords, up to 100 characters. An empty or wildcard query is refused with "Please give something to search for." |
| `limit` | 6 | Cards returned, 1 to 10 |
| `on_view` | false | When true, only objects the museum flags as currently on view |
| `has_images` | true | When true, only objects with images. Set false to include records without images |
| `highlights_only` | false | When true, only objects the museum marks as highlights |
| `department_id` | none | Limits results to one department. Take the id from `list_met_departments` |

## Behaviour to plan around

- **The count is the total, the cards are a slice.** "1208 objects match, showing 3" means the query matched 1208 records. There is no offset or page argument, so the most you can see for one query is 10 cards. To see other works, change the query or the filters.
- **Matching is broad keyword matching.** It is not limited to titles. A search for `cat` returned a garment by a designer whose name contains the word. A search for `sunflowers` with highlights only returned garments along with a painting.
- **An artist's name also finds works after that artist.** A search for `Vermeer` returned the painter's own works and then prints and a painting "after Vermeer" by others. Check the maker label on each card.
- **Order is the service's relevance order.** Do not describe the first card as the best known or most important work.
- **Filters combine.** `department_id`, `on_view` and `highlights_only` together can cut a large set to a short list or to nothing. Remove one filter at a time when a search comes back empty.
- **`on_view: true` removes a lot.** Many well known works on paper, textiles and light sensitive objects are not on view. A specific query with this filter can return nothing even though the museum holds the work.
- **A department id that is not on the list is not rejected.** In testing, an unused id returned results from several departments. Always check the `Department` line on the cards.
- **No result message:** "No objects in The Met collection match <query>."

## Choosing query terms

| The visitor wants | Good first query | Then try |
| --- | --- | --- |
| A subject or animal | The plain noun, singular (`cat`) | Related nouns, a deity or symbol tied to it |
| An artist | The surname, or the full name for a common surname | Add `on_view` only after seeing the full set |
| An object type | The type (`quilt`, `armor`, `tapestry`) | A technique or material from the medium lines you get back |
| A culture or period | The culture word with a `department_id` | An object type within that department |
| A material | The material (`jade`, `ivory`) | The department where it is common |

Use two or three distinct queries for a theme. Do not run many near duplicates.

## Call budget

A four stop tour usually needs one department lookup, two or three searches and six to eight record lookups. If you pass about a dozen record lookups without enough good stops, stop and tell the visitor what you found and what was thin.
