# NICU to Home

A shopping agent for parents of premature and medically complex babies.

Parents of babies with central lines, feeding tubes, ostomies, oxygen and conditions such as short bowel syndrome spend hours hunting for the right products, often in Facebook groups. The hardest part is not buying. It is knowing what to search for: "Broviac line cover", "tubie pads", "TPN backpack".

NICU to Home lets a parent describe their situation in plain words and get products that families like theirs ended up using, with a short note on why each one helps and a link to buy.

> **Not medical advice.** This project recommends products, never care decisions. Always check with your baby's care team before using anything near a line, tube or stoma site.

## How it works

1. **Need map.** A parent-written map from situations (devices, conditions, stage) to needs and the words sellers use for them. See [docs/keywords.md](docs/keywords.md).
2. **Agent.** Asks a few questions, turns the answers into searches against the [Shopify Global Catalog](https://shopify.dev/docs/agents/catalog), and explains each result. When something is not in the catalog, it gives the parent the right words to search elsewhere.
3. **Eval harness.** A set of real parent questions, scored for relevance, device and stage fit, sizing and safety, so every change is measured.

## Status

Early planning. The first milestone is a coverage test: how many of the products families actually use can be found in the Shopify catalog.

## Contributing

Contributions are welcome, especially from NICU parents, nurses and therapists. The most useful contribution is often a keyword or product type we have missed. See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)
