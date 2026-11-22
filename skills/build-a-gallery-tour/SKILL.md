---
name: build-a-gallery-tour
description: "Use to design a short themed tour, compare artworks in The Met collection, or choose works to visit in person."
---

Set a theme from the request and a manageable number of stops. For an in-person visit use `search_met_artworks` with `on_view: true`. For a department-specific request use `list_met_departments` to obtain its current ID. Use concrete subjects, artist names or object types as search terms. For an online study, omit the on-view filter. A search defaults to works with images, so try `has_images: false` to broaden a thin result.

Pick contrasting objects that have a clear connection to the theme. Open each candidate using `get_met_artwork` with the returned object ID. A search card's maker label can name a culture or period when an artist is unknown. Preserve that distinction. Use the supplied title, date or date range, medium, department and collection link. If available, quote the gallery number for a physical visit and include the explicitly marked public-domain image when an image was requested.

Give each stop one detail to look for or one question to ask of the object. Ground the prompt in the record or phrase it as an invitation to observe. Tie successive stops together through visible material, shared use or a documented difference. Group stops by returned gallery numbers when helpful. A gallery label is a collection-data snapshot and the service has no routing or opening-hours data.
