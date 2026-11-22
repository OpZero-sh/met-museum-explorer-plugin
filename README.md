# Met Museum Explorer

Turn a subject you love into a short tour of The Metropolitan Museum of Art. Choose works around a material, an artist or a question. Each stop comes with an object record, a detail to look for and a gallery number when the collection lists one.

[Connect with Claude, ChatGPT, Muse Code, or Grok](PROVIDERS.md)

> “Plan three stops around cats in Egyptian art. Pick works on view and give my six-year-old one thing to look for at each stop.”

> “Compare two views of the same subject in different media. Give me the object records so I can look closer.”

## Use it in Claude Code

```sh
claude plugin marketplace add OpZero-sh/plugins
claude plugin install met-museum-explorer@opzero
```

Run `/met-museum-explorer:build-a-gallery-tour` or ask the **collection-curator** agent to shortlist works for a class, a visit or a digital exhibition. The public collection service requires no account. Gallery locations reflect the latest record returned by the service and can change before your visit.

OpZero uses The Met's Open Access collection records. The plugin preserves museum object links and includes image links when the museum identifies the image as public domain. [Explore the connector](https://met-museum-explorer.mcp.opzero.sh/) · [The Met Collection API](https://metmuseum.github.io/)

## In use

Examples from the connected services in Claude.

![An object record from The Met collection](media/painting.webp)
