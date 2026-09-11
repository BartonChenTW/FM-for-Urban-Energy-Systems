---
title: "2.4.5 Geospatial & Weather FMs"
parent: "2.4 Existing FMs Relevant to Energy"
grand_parent: Part 2 — Foundation Knowledge of FMs
nav_order: 5
status: draft
last_reviewed: 2026-09-11
---

# 2.4.5 Geospatial & Weather Foundation Models
{: .no_toc }

{% include page-status.html %}

1. TOC
{:toc}

---

A family that does not target energy systems directly but is a plausible input encoder for them, and is worth knowing for that reason.

**GraphCast** performs medium-range global weather forecasting with a graph neural network (encode-process-decode) operating on an icosahedral multi-mesh over the sphere.[^lam2023graphcast] It and similar models (FengWu, Aurora) demonstrate that physical fields on a spatiotemporal grid support the foundation-model pattern at global scale.

**Prithvi** is a Vision Transformer masked-autoencoder pretrained over multispectral, multitemporal satellite patches, developed by NASA and IBM Research.[^jakubik2023prithvi] **Prithvi-EO-2.0** scales this up and underlies **Granite-GFM**, which uses a Swin Transformer backbone to estimate land surface temperature at 30 m resolution and hourly frequency for arbitrary cities.[^szwarcman2024prithvieo2]

**Relevance to urban energy systems.** Urban heat islands drive peak cooling load and grid stress simultaneously, which makes a weather- or microclimate-conditioned building energy model a plausible fusion target. No existing paired dataset couples geospatial/weather foundation model output with building load or UBEM data at foundation-model scale — this would need to be built as a corpus, not simply assembled from existing releases. This is flagged as a candidate direction in [§4.2](../part-4-directions/4-2-fms-for-building-stocks.html) and is one of the less mature intersections surveyed in this book.

{: .note }
This sub-section is intentionally brief: geospatial/weather FMs are adjacent rather than core to this book's subject, and the honest state of the art here is "plausible encoder, no demonstrated fusion with UES data yet."

[^lam2023graphcast]: Lam, R., Sanchez-Gonzalez, A., Willson, M. et al. (2023). Learning skillful medium-range global weather forecasting. *Science*, 382(6677), 1416–1421. https://doi.org/10.1126/science.adi2336
[^jakubik2023prithvi]: Jakubik, J., Roy, S., Phillips, C. E. et al. (2023). Foundation models for generalist geospatial artificial intelligence. arXiv:2310.18660.
[^szwarcman2024prithvieo2]: Szwarcman, D., Roy, S., Fraccaro, P. et al. (2024). Prithvi-EO-2.0: A versatile multi-temporal foundation model for Earth observation applications. arXiv:2412.02732.

---
[← Previous: 2.4.4 Tabular FMs](2-4-4-tabular-fms.html) · [Next: 2.5 What Does Not Exist Yet →](2-5-what-does-not-exist-yet.html)
