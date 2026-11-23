# Australian Car Repair Cost Dataset (2026)

**1,200 rows of Australian car repair price ranges — 30 brands x 40 repair types — in AUD.**
Free, open, machine-readable. Built and maintained by the [AutoRepairCost](https://autorepaircost.net) project.

This repository is the public data release behind [autorepaircost.net/dataset-2026](https://autorepaircost.net/dataset-2026).
It exists so researchers, journalists, bloggers and developers can use real Australian repair-price
ranges without re-scraping anything. **If you use this data, please link to [autorepaircost.net](https://autorepaircost.net).**

- **Landing page:** https://qixiaobo.github.io/au-repair-cost-dataset/
- **Canonical dataset page:** https://autorepaircost.net/dataset-2026
- **Data file:** [`data/autorepaircost-au-repair-costs.csv`](data/autorepaircost-au-repair-costs.csv)
- **License:** [CC BY 4.0](LICENSE) — attribution must point to autorepaircost.net
- **Data vintage:** 2026-11-11 (market data) · exported 2026-11-23

## Coverage

A complete grid: **30 brands x 40 repair types = 1,200 rows**, zero missing cells.

- **Brands (30):** Toyota, Hyundai, Mazda, Kia, Nissan, Ford, Volkswagen, Honda, Subaru, BMW,
  Mercedes-Benz, Audi, Mitsubishi, Skoda, Suzuki, Jeep, Isuzu, Lexus, Land Rover, Volvo, Peugeot,
  Renault, Porsche, RAM, Chery, MG, BYD, Haval, GWM, LDV.
- **Repair types (40):** from wheel alignment and engine oil changes up to head gaskets,
  timing chains, CVT transmission repairs, turbochargers and hybrid battery replacement.
  Full slugs are the `repair` values in the CSV (e.g. `timing-belt-replacement`,
  `brake-pad-replacement-front`, `hybrid-battery-replacement`).

## Column dictionary

| Column | Meaning |
|---|---|
| `brand` | Brand slug (30 values) |
| `repair` | Repair-type slug (40 values) |
| `total_min` / `total_max` | Fitted total price range, **AUD** |
| `labor_min` / `labor_max` | Labour component of the range, AUD |
| `parts_min` / `parts_max` | Parts component of the range, AUD |
| `source` | Provenance: an `autoguru.com.au/...` page anchor, `estimated`, or `curated` |
| `confidence` | `high` or `medium` (see "Honest grading" below) |

**Tax treatment:** the AU market on autorepaircost.net documents prices as **GST-inclusive**
("Prices include GST", AU market notes). Treat the ranges as consumer-facing, GST-inclusive
indicative prices.

**Ranges, not quotes.** `total_min`–`total_max` is an aggregated market estimate range for a
brand x repair pair — not a workshop quote and not a single observed transaction. Ranges are
nationwide, before state-level labour adjustment. The `total_*` columns are the authoritative
fields; `labor_*` / `parts_*` are an indicative decomposition. The component bounds sum exactly
to the total bounds in only **71 of 1,200 rows (5.9%)**; in the other 1,129 rows the total bounds
were estimated independently of the labour/parts split. Always treat `total_*` as authoritative
and the components as indicative. (Reproduce: count rows where
`total_min != labor_min + parts_min` or `total_max != labor_max + parts_max`.)

## Summary statistics (computed from the CSV)

All numbers below are reproducible from the CSV itself — no hand-entered figures.

| Measure | Value (AUD) |
|---|---|
| Rows | 1,200 (30 brands x 40 repairs) |
| `total_min` — min / median / max | 64 / 375 / 4,000 |
| `total_max` — min / median / max | 128 / 876.5 / 10,000 |
| Range midpoint — median / mean | **630** / 1,021.53 |
| Range midpoint — min / max | 96 / 7,000 |
| Range width (`total_max` − `total_min`) — median | 487 |
| `labor_min` / `labor_max` — medians | 190 / 440 |
| `parts_min` / `parts_max` — medians | 0 / 674 |

### Price-band distribution (by range midpoint)

| Band (AUD) | Rows | Share |
|---|---|---|
| 0–250 | 162 | 13.5% |
| 250–500 | 286 | 23.8% |
| 500–750 | 262 | 21.8% |
| 750–1,000 | 138 | 11.5% |
| 1,000–1,500 | 119 | 9.9% |
| 1,500–2,000 | 48 | 4.0% |
| 2,000–3,000 | 103 | 8.6% |
| 3,000–5,000 | 74 | 6.2% |
| 5,000+ | 8 | 0.7% |

Nearly 60% of brand x repair pairs sit under AUD 750 at the midpoint; the long tail is dominated
by transmission, engine and hybrid-battery work.

### Extremes (sanity anchors)

- Cheapest rows: MG wheel alignment **64–128**, Chery wheel alignment 66–131, Haval 66–133.
- Most expensive rows: Porsche CVT transmission repair **4,000–10,000**, Land Rover CVT
  3,400–8,500, Porsche fuel injector replacement 2,400–9,000.
- Brand median midpoint: Porsche 1,175 (highest) … MG 470 (lowest). European premium brands
  sit roughly 1.5–2x the mainstream Japanese/Korean brands, consistent with the published
  brand-factor method.

## Honest grading — read before relying on a row

| Provenance | Rows | Share |
|---|---|---|
| URL-anchored to an AutoGuru page (`source` starts with `autoguru.com.au`) | 175 | 14.6% |
| Model-estimated (`estimated`: generic baseline x per-brand factor + labour adjustment) | 1,007 | 83.9% |
| Curated from published AU sources (`curated`) | 18 | 1.5% |

| Confidence | Rows | Share |
|---|---|---|
| `high` | 22 | 1.8% |
| `medium` | 1,178 | 98.2% |

**What 98.2% `medium` means:** most rows are *indicative market ranges* produced by a documented,
reproducible estimation method (brand factors applied to anchored baselines), not individually
observed quotes. `medium` does not mean "wrong" — it means "verify before a high-stakes decision".
The 175 URL-anchored rows carry a real source page you can open and spot-check: prefix the
`source` value with `https://` and the quoted range on that page should bracket our
`total_min`–`total_max`. Estimated rows are aggregated market estimates, **not workshop quotes**.

## Cite us

If you use this data in an article, paper, video, app or dataset, please cite it and
**link to [autorepaircost.net](https://autorepaircost.net)** (a link to the dataset page
https://autorepaircost.net/dataset-2026 is ideal). Attribution is required by the CC BY 4.0 license.

**Plain text:**

> AutoRepairCost (2026). *Australian Car Repair Cost Dataset: 30 brands x 40 repair types, 1,200
> price ranges in AUD.* https://autorepaircost.net/dataset-2026 — mirror:
> https://qixiaobo.github.io/au-repair-cost-dataset/

**BibTeX:**

```bibtex
@misc{autorepaircost2026au,
  author       = {{AutoRepairCost Dataset Project}},
  title        = {Australian Car Repair Cost Dataset: 30 brands x 40 repair types, 1,200 price ranges in AUD},
  year         = {2026},
  howpublished = {\url{https://autorepaircost.net/dataset-2026}},
  note         = {Mirror: \url{https://qixiaobo.github.io/au-repair-cost-dataset/}. CC BY 4.0. Data vintage 2026-11-11}
}
```

Machine-readable citation metadata: [`CITATION.cff`](CITATION.cff).

**One-line version for a blog post or README:**

> Data: [Australian Car Repair Cost Dataset](https://autorepaircost.net/dataset-2026) (CC BY 4.0).

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — see [`LICENSE`](LICENSE).
You may share and adapt the data for any purpose, including commercially, **provided you give
appropriate credit with a link to https://autorepaircost.net** (or the dataset page above) and
indicate if you changed anything.

## Verify the file

```bash
shasum -a 256 data/autorepaircost-au-repair-costs.csv
# expect d3a067191e26a4d5d462456279728df90b8143b4a25a085e1043da016e73cd87
grep -c '' data/autorepaircost-au-repair-costs.csv   # 1201 (header + 1,200 rows)
```

The same rows power the public tables at https://autorepaircost.net/llms.txt and
https://autorepaircost.net/llms-full.txt — an independent second reading of every brand x repair pair.

## Contact

Via the project website: https://autorepaircost.net (no personal contact details are published
in this repository).