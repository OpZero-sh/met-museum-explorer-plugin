# Data source, rights and limits

## Where the records come from

- The Met Museum Explorer server at met-museum-explorer.mcp.opzero.sh is run by OpZero. It reads The Metropolitan Museum of Art's Open Access collection data through The Met Collection API (documented at https://metmuseum.github.io/).
- OpZero and this plugin are not affiliated with, sponsored by or endorsed by The Metropolitan Museum of Art. "The Met" is used only to say whose collection the records describe.
- The server needs no account. Its own description says requests are not stored.

## Rights

- The museum publishes its collection data for open use under its Open Access policy. Record facts such as title, date and medium can be quoted.
- An image is offered only on the `Image (public domain)` line, which appears when the museum marks that object as public domain under Open Access. Those images can be linked and reused.
- When that line is absent, the work or its photograph may be under copyright, as with many modern and contemporary works. Link the object page. Do not link or embed an image from elsewhere and do not say an image is free to use.
- The service returns no catalog essays or label text. Do not paste such text from memory into an answer or a reference file.
- For any formal reuse question, send the person to the museum's own terms on metmuseum.org. This plugin does not give legal advice.

## Freshness

- Every call reads the current collection data. Nothing here is a live sensor of the building: "on view" and gallery numbers are what the data says, and installations change for rotation, loans, conservation and gallery closures.
- Tell a visitor to check the object page on the day when a particular work matters to them.

## Coverage

- The service covers objects in the museum's collection database. It does not cover current exhibitions, loans from other museums on display at The Met, events, tours run by the museum, hours, admission or maps.
- Records vary in completeness. Dates, dimensions, artists and galleries can each be missing.
- Search returns at most ten cards per call with no paging, so a list from this plugin is a sample of the matches, not a full inventory.

## Citing an object

A simple citation built only from record fields:

[Artist or maker label]. [Title]. [Date]. [Medium]. The Metropolitan Museum of Art, New York. [Credit line]. Object id [id]. [Collection link].

Leave out any part the record does not have. Adapt the order to the style guide the person uses. The record has no accession number, so say so if a style asks for one and point to the object page.
