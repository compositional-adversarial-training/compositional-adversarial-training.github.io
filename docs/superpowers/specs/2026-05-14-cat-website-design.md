---
name: CAT Paper Website Design
description: Design spec for converting nerfies.github.io template into the CAT (Compositional Adversarial Training for Robust Visual Watermarking) project page
type: project
---

# CAT Paper Website Design

## Overview

Convert the nerfies.github.io single-page academic project template into the project website for "Compositional Adversarial Training for Robust Visual Watermarking." The site is a single long-scroll HTML page (`index.html`) using the existing Bulma CSS + FontAwesome + academicons stack. No new dependencies. Deployable on GitHub Pages with no build step.

---

## Paper Summary (for content reference)

**Title:** Compositional Adversarial Training for Robust Visual Watermarking  
**Authors:** Anirudh Satheesh, Michael-Andrei Panaitescu-Liess, Andrew Xu, Georgios Milis, Heng Huang, Zikui Cai, Furong Huang  
**Venue:** ICML 2026 (under review / workshop version available)  
**GitHub:** https://github.com/Asatheesh6561/CAT  
**arXiv:** placeholder (to be filled in)  
**PDF:** placeholder (to be filled in)

**Core contribution:** CAT replaces random post-processing augmentation in watermark training with a learned sequential differentiable adversary. A GRU controller with frozen DINOv2 features selects attack families via straight-through Gumbel-Softmax at each step; entropy regularization prevents collapse to a single attack. This yields up to 63.5% capacity gains (single-step) and 13.0% (compositional), with substantially faster convergence.

---

## Asset Inventory

All images are copied from `CAT4Robust-Watermark/figures/` and `CAT4Robust-Watermark/` into `static/images/` in the website directory.

| File | Source path | Usage |
|------|-------------|-------|
| `RobustWatermarkTeaser.png` | `figures/RobustWatermarkTeaser.png` | Hero figure |
| `cat_overview-1.png` | `figures/cat_overview-1.png` | Method section |
| `rand_vs_adv_d1.png` | `figures/rand_vs_adv_d1.png` | Results motivation (left panel) |
| `rand_vs_adv_d2.png` | `figures/rand_vs_adv_d2.png` | Results motivation (right panel) |
| `pixelseal_convergence.png` | `figures/pixelseal_convergence.png` | Convergence figure (left) |
| `videoseal_convergence.png` | `figures/videoseal_convergence.png` | Convergence figure (right) |
| `rar_robustness.png` | `figures/autoregressive_figures/rar_robustness.png` | Autoregressive results |
| `taming_robustness.png` | `figures/autoregressive_figures/taming_robustness.png` | Autoregressive results |
| `rar_auc.png` | `figures/autoregressive_figures/rar_auc.png` | Autoregressive ROC |
| `taming_auc.png` | `figures/autoregressive_figures/taming_auc.png` | Autoregressive ROC |
| `qualitative_plot_1.png` through `qualitative_plot_5.png` | `figures/qualitative_figures/` | Qualitative section |

---

## Page Structure

### Section 1: Navbar

Keep the nerfies navbar structure. Remove the "More Research" dropdown and home icon link — replace with an empty navbar (no links needed for now, or optionally in-page anchor links to Abstract / Method / Results).

### Section 2: Hero

- Title: "Compositional Adversarial Training for Robust Visual Watermarking"
- Authors (as `<span class="author-block">` with links where known):
  - Anirudh Satheesh
  - Michael-Andrei Panaitescu-Liess
  - Andrew Xu
  - Georgios Milis
  - Heng Huang
  - Zikui Cai
  - Furong Huang
- Affiliation: University of Maryland
- Three buttons:
  - **Paper** — icon `fas fa-file-pdf`, href placeholder (`#`), label "Paper"
  - **arXiv** — icon `ai ai-arxiv`, href placeholder (`#`), label "arXiv"
  - **Code** — icon `fab fa-github`, href `https://github.com/Asatheesh6561/CAT`, label "Code"
- Paper and arXiv buttons are visually present but link to `#` until real URLs are available. No "disabled" or "coming soon" text — just placeholders.

### Section 3: Overview Figure

Immediately below the hero, full-width within `is-max-desktop` container:
- Display `RobustWatermarkTeaser.png` as a static `<img>` (not a video)
- Caption: "CAT improves overall bit accuracy by 2.2% and capacity by 17.0% for single-step and compositional attacks."

### Section 4: Abstract

- `<h2>Abstract</h2>` centered
- Abstract text verbatim from the paper (the full paragraph from `sections/00_abstract.tex`)
- Below the abstract text: `cat_overview-1.png` displayed full-width within the column, with caption: "Overview of the CAT training pipeline. The embedder writes message m into image x; the sequential adversarial augmenter repeatedly selects and applies differentiable attacks via Gumbel-Softmax; the extractor recovers the message and the message loss drives both watermark and adversary updates."

### Section 5: Method

- `<h2>Method</h2>`
- **No figure** — `cat_overview-1.png` already shown in the abstract section covers the full method visually
- Text covering four key components (each as a paragraph or subsection):
  1. **Problem formulation** — min-max objective over compositional attack space T; embedder E_θ, extractor D_ψ, adversary A_φ
  2. **Sequential attack generator** — library of K differentiable primitives, GRU controller with frozen DINOv2 ViT-S/16 features, straight-through Gumbel-Softmax relaxation for discrete attack selection
  3. **Entropy regularization** — entropy bonus H(π_φ) prevents adversary collapse to single attack mode; keeps policy diverse throughout training
  4. **Training efficiency** — shared single-pass computational graph with watermark model; only 800K adversary parameters; 20–30% additional training overhead; inference unchanged

### Section 6: Results

Six subsections in order:

#### 6a. Motivation

- Two figures side by side in a two-column Bulma layout:
  - Left: `rand_vs_adv_d1.png` — caption "(a) Single-step augmentation training"
  - Right: `rand_vs_adv_d2.png` — caption "(b) Compositional augmentation training"
- Shared caption below: "Random augmentation creates unstable training due to inefficient augmentation allocations, whereas the learned adversary consistently targets the model's current weaknesses."

#### 6b. Single-Step Attack Results (T=1)

- Brief introductory sentence about the single-step setting
- **Table 1** reproduced as an HTML `<table>` using Bulma table classes (`table is-bordered is-striped is-hoverable is-fullwidth`):
  - Two sub-tables or a single table with a dividing header row: SA-1B (ID) and CLIC (OOD)
  - Columns: Model (bits) | Identity Bit acc / Cap | Value Bit acc / Cap | Compression Bit acc / Cap | Geometric Bit acc / Cap | Combined Bit acc / Cap | Overall Bit acc / Cap
  - Rows: InvisMark, TrustMark, MBRS, VideoSeal 0.0, +CAT, VideoSeal 1.0, +CAT, PixelSeal, +CAT
  - Bold the Overall capacity improvements (e.g. ↑63.5%) as in the paper

#### 6c. Compositional Attack Results (T=2)

- Brief introductory sentence about the two-step setting
- **Table 2** reproduced as HTML:
  - Same structure as Table 1 but columns are: Val+Val | Val+Comp | Val+Geom | Comp+Comp | Comp+Geom | Geom+Geom | Overall
  - SA-1B and CLIC sub-tables

#### 6d. Training Convergence

- `<h3>Training Convergence</h3>`
- Two figures side by side:
  - Left: `pixelseal_convergence.png` — caption "(a) PixelSeal"
  - Right: `videoseal_convergence.png` — caption "(b) VideoSeal"
- Shared caption: "CAT substantially accelerates convergence for both PixelSeal and VideoSeal, reaching lower validation bit error earlier than random augmentation."

#### 6e. Image Quality

- `<h3>Image Quality</h3>`
- **Table 5** as HTML: PSNR / SSIM / MS-SSIM / LPIPS on SA-1B and DIV2K for all models

#### 6f. Video Watermarking

- `<h3>Video Watermarking</h3>`
- Brief intro sentence
- **Table 9** (single-step video results on Movie-Gen-Bench ID and SAV-Test OOD)
- **Table 10** (compositional video results)

#### 6g. Autoregressive Watermarking

- `<h3>Autoregressive Watermarking</h3>`
- Brief intro sentence about the WMAR framework, Taming and RAR-XL generators, TPR@FPR=1% metric
- **Table 11** (Taming results) and **Table 12** (RAR-XL results) side by side or stacked
- Four figures in a 2×2 grid:
  - `taming_robustness.png` — caption "Taming: continuous attack sweeps"
  - `rar_robustness.png` — caption "RAR-XL: continuous attack sweeps"
  - `taming_auc.png` — caption "Taming: ROC curves"
  - `rar_auc.png` — caption "RAR-XL: ROC curves"

### Section 7: Qualitative Results

- `<h2>Qualitative Results</h2>`
- Display `qualitative_plot_1.png` through `qualitative_plot_5.png` stacked vertically, each full-width within `is-max-desktop`
- Caption for each: "Watermarked images under single-step and compositional attacks. CAT (Ours) consistently recovers more bits than random augmentation across all attack types."

### Section 8: BibTeX

```bibtex
@article{satheesh2026cat,
  author    = {Satheesh, Anirudh and Panaitescu-Liess, Michael-Andrei and Xu, Andrew and Milis, Georgios and Huang, Heng and Cai, Zikui and Huang, Furong},
  title     = {Compositional Adversarial Training for Robust Visual Watermarking},
  journal   = {ICML},
  year      = {2026},
}
```

### Section 9: Footer

Standard nerfies footer:
- CC BY-SA 4.0 license notice
- Credit to nerfies template with link back to `https://github.com/nerfies/nerfies.github.io`
- Remove the Google Analytics script from the `<head>` (replace with a placeholder comment)

---

## Implementation Notes

- **No videos** — the nerfies template video carousel and all `<video>` tags are removed entirely
- **No slider/interpolation demo** — the interpolation panel is removed
- **Static images only** — all figures are `<img>` tags
- **Tables** — use Bulma `table` classes; wrap in `<div class="table-container">` for horizontal scroll on mobile; keep font size small (`is-size-7`) given the density of the result tables
- **Figures directory** — all images live in `static/images/`; copy step is part of implementation
- **CSS** — no new CSS files needed; minor additions (e.g. figure caption styling, table row highlighting for CAT rows) can go in `static/css/index.css`
- **Google Analytics** — remove the existing `gtag` script block; replace with a comment `<!-- Analytics removed -->`
- **arXiv / PDF buttons** — use `href="#"` for now; update when real links are available
- **Favicon** — keep existing `favicon.svg` or replace with a simple placeholder

---

## File Changes

1. `index.html` — complete rewrite of body content; keep all `<head>` link/script tags except remove gtag
2. `static/images/` — add all figures listed in Asset Inventory above (copy from paper directory)
3. `static/css/index.css` — minor additions for caption styling and CAT-row highlighting
4. `docs/superpowers/specs/2026-05-14-cat-website-design.md` — this file
