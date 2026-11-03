# Leveraging Smartphone Inertial Data for User Authentication

Academic project page for the AVSS 2026 paper by **Gabriele Bortolai, Nicoletta Noceti,
and Francesca Odone**, MaLGa-DIBRIS, University of Genoa.

The paper studies gait authentication from smartphone acceleration, angular velocity,
and gravity. An unsupervised LSTM autoencoder learns a shared representation with
middle fusion; a personal One-Class SVM models each user's gait. Experiments use
50 participants and 63,316 gait segments from the MARCH dataset.

This repository contains the project website and paper PDF. It does not contain the
model implementation or dataset. The MARCH dataset is publicly available through the
[Malga-Vision/MARCH repository](https://github.com/Malga-Vision/MARCH).

## Preview and validation

The site is a single static HTML page, with self-hosted fonts, styles, and JavaScript.
No build step or package installation is required.

```bash
python3 tools/page_guard.py
python3 -m http.server 8000 --bind 127.0.0.1
```

Open [the local preview](http://localhost:8000/). The guard checks local references,
section anchors, metadata placeholders, the Content Security Policy, allowed external
links, and asset sizes.

## Page contents

| Path | Purpose |
| --- | --- |
| `index.html` | Paper title, authors, verbatim abstract, method, dataset, results, FAQ, citation, and metadata |
| `static/pdfs/paper.pdf` | Unmodified author-supplied six-page paper |
| `static/images/pipeline.png` | Figure 1: authentication pipeline |
| `static/images/segmentation.png` | Figure 2: ankle-IMU gait segmentation |
| `static/images/latent-size.png` | Figure 4: latent-size validation study |
| `static/images/fusion.png` | Figure 6: middle versus early fusion |
| `static/malga/` | Shared MaLGa styles, script, fonts, logos, and icons |
| `llms.txt`, `sitemap.xml` | Machine-readable summary and canonical page URL |
| `tools/projects.json` | Related lab projects, including this page |
| `tools/render_shared.py` | Related-project and footer renderer |

The figures are cropped directly from the supplied PDF. Tables I and II are transcribed
as accessible HTML tables. Results retain their original mean and standard-deviation
values, with FAR expressed as a fraction. The abstract and FAQ text are mirrored in
JSON-LD; keep the visible and structured versions synchronized when editing.

The page distinguishes smartphone authentication inputs from the additional ankle IMU
used for segmentation, and simulated impairment from actual injuries. The final
configuration uses the 32-dimensional representation selected in Section V-B and
reported in Table II. No code, arXiv, poster, or video links are shown because none were
provided. Add them when available.

Conference naming and dates follow the [official AVSS 2026 website](https://www.avss2026.org/).
AVSS 2026 is inferred from the supplied paper's conference directory; the PDF itself
contains no proceedings header. The citation omits unverified DOI, proceedings page
numbers, and publisher fields.

## Hosting

The canonical URL is configured for this repository's GitHub remote:

[https://gabrielebortolai.github.io/phone-authentication/](https://gabrielebortolai.github.io/phone-authentication/)

To publish, set **Settings > Pages > Source** to **GitHub Actions**, then push to the
repository's default branch. The existing **Check and deploy page** workflow runs the
page guard before publishing. Configuring the page locally does not publish it.

If the repository moves or uses a custom domain, update the canonical URL, social and
Scholar metadata, JSON-LD URLs, `llms.txt`, `sitemap.xml`, and this project's `page_url`
in `tools/projects.json`. Add the new host to `tools/allowed-domains.txt`.

## Refresh shared blocks

This page is hosted under a personal account, while related projects and branding belong
to the MaLGa organization. Preserve that distinction when regenerating the footer:

```bash
python3 tools/render_shared.py index.html --page-repo phone-authentication --page-owner GabrieleBortolai
python3 tools/page_guard.py
```

`--page-owner` changes the page-source link without changing the lab links. Each entry
in `tools/projects.json` may supply `page_url` for a page hosted outside the lab's default
GitHub Pages domain.

## Credits and licenses

Built with the [MaLGa academic page template](https://github.com/Malga-Vision/malga-academic-page-template).
The shared visual identity and security checks are retained.

- Website code: MIT; see [LICENSE](LICENSE).
- Paper text and figures: their respective authors and rights holders; the website's code license does not relicense the paper.
- Fira Sans: SIL Open Font License 1.1; Roboto Slab: Apache License 2.0. License files are in `static/malga/fonts/`.
- MaLGa and University of Genoa logos belong to their owners.

The research was supported by the MARCH project (FA86552317074), funded by the Air Force
Office of Scientific Research. See [SECURITY.md](SECURITY.md) for security reporting.
