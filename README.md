# NICU to Home

A shopping agent for parents of premature and medically complex children, in Canada and the US.

Parents of children with central lines, feeding tubes, ostomies, oxygen and conditions such as short bowel syndrome spend hours hunting for the right products. The best answers are buried in invite-only parent groups. The hardest part is not buying. It is knowing what to search for: "Broviac line cover", "tubie pads", "TPN backpack".

NICU to Home lets a parent describe a problem in plain words and get the solutions other families actually used, with why each one helped and where to buy it.

> **Peer experience, not medical advice.** Every suggestion here was shared by a parent, not a professional. Check with your child's care team before using it.

## How it works

1. **Knowledge from families.** Muse captures recommendations from parent groups each week. AI sorts them, merges duplicates across groups and removes anything that identifies a family. The maintainer reviews one weekly summary before anything is published. See [docs/muse-weekly-capture.md](docs/muse-weekly-capture.md).
2. **Need map.** A map from situations (devices, conditions, stage, country) to needs and the words sellers use for them. See [docs/keywords.md](docs/keywords.md).
3. **Agent.** Turns a parent's question into searches against the [Shopify Global Catalog](https://shopify.dev/docs/agents/catalog). When a product isn't there, it opens a ready-made search on Etsy, Amazon or Walmart for the family's country.
4. **Eval harness.** Real parent questions, scored for relevance, fit, grounding and safety, so every change is measured.
5. **Unanswered searches.** Searches without a good answer are logged and tagged, so we know what to cover next.

## Principles

- **No paid ranking.** Nobody can pay to appear or rank higher.
- **Labelled as peer experience.** Every suggestion says it came from a parent and should be checked with the care team.
- **Country-aware.** Results and wording fit Canada or the US. For example, a diet suggestion points Canadian families to their dietitian and US families to their child's doctor, since many US families don't have a dietitian.

## Status

Early planning. The first milestone is a coverage test: how many of the products families actually use can be found in the Shopify catalog.

## Contributing

Contributions are welcome, especially from parents, nurses, dietitians and therapists. The most useful contribution is often a solution or keyword we have missed. See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)
