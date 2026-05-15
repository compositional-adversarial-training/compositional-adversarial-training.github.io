# CAT Paper Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Convert the nerfies.github.io template into the CAT (Compositional Adversarial Training for Robust Visual Watermarking) academic project page.

**Architecture:** Single `index.html` rewrite using the existing Bulma CSS + FontAwesome + academicons stack. All figures are static `<img>` tags copied from the paper directory. Result tables are rendered as HTML `<table>` elements with Bulma styling. No new JS dependencies; the bulma-carousel and bulma-slider scripts remain in `<head>` but are unused.

**Tech Stack:** HTML5, Bulma CSS (already in `static/css/`), FontAwesome (already in `static/js/`), academicons (CDN), vanilla JS (existing `static/js/index.js` kept as-is)

---

## File Map

| File | Action | Responsibility |
|------|--------|----------------|
| `static/images/RobustWatermarkTeaser.png` | Create (copy) | Hero figure |
| `static/images/cat_overview-1.png` | Create (copy) | Method overview |
| `static/images/rand_vs_adv_d1.png` | Create (copy) | Motivation panel (a) |
| `static/images/rand_vs_adv_d2.png` | Create (copy) | Motivation panel (b) |
| `static/images/pixelseal_convergence.png` | Create (copy) | Convergence panel (a) |
| `static/images/videoseal_convergence.png` | Create (copy) | Convergence panel (b) |
| `static/images/rar_robustness.png` | Create (copy) | Autoregressive results |
| `static/images/taming_robustness.png` | Create (copy) | Autoregressive results |
| `static/images/rar_auc.png` | Create (copy) | Autoregressive ROC |
| `static/images/taming_auc.png` | Create (copy) | Autoregressive ROC |
| `static/images/qualitative_plot_1.png` | Create (copy) | Qualitative results |
| `static/images/qualitative_plot_2.png` | Create (copy) | Qualitative results |
| `static/images/qualitative_plot_3.png` | Create (copy) | Qualitative results |
| `static/images/qualitative_plot_4.png` | Create (copy) | Qualitative results |
| `static/images/qualitative_plot_5.png` | Create (copy) | Qualitative results |
| `static/css/index.css` | Modify | Add figure caption + CAT-row highlight styles |
| `index.html` | Rewrite | Full page content |

---

## Task 1: Copy figures into static/images/

**Files:**
- Create: `static/images/` (all figures listed above)

- [ ] **Step 1: Copy all figures**

```bash
PAPER=/fs/cml-projects/spec_decoding_furong/CAT4Robust-Watermark/figures
DEST=/fs/cml-projects/spec_decoding_furong/nerfies.github.io/static/images

cp "$PAPER/RobustWatermarkTeaser.png" "$DEST/"
cp "$PAPER/cat_overview-1.png" "$DEST/"
cp "$PAPER/rand_vs_adv_d1.png" "$DEST/"
cp "$PAPER/rand_vs_adv_d2.png" "$DEST/"
cp "$PAPER/pixelseal_convergence.png" "$DEST/"
cp "$PAPER/videoseal_convergence.png" "$DEST/"
cp "$PAPER/autoregressive_figures/rar_robustness.png" "$DEST/"
cp "$PAPER/autoregressive_figures/taming_robustness.png" "$DEST/"
cp "$PAPER/autoregressive_figures/rar_auc.png" "$DEST/"
cp "$PAPER/autoregressive_figures/taming_auc.png" "$DEST/"
cp "$PAPER/qualitative_figures/qualitative_plot_1.png" "$DEST/"
cp "$PAPER/qualitative_figures/qualitative_plot_2.png" "$DEST/"
cp "$PAPER/qualitative_figures/qualitative_plot_3.png" "$DEST/"
cp "$PAPER/qualitative_figures/qualitative_plot_4.png" "$DEST/"
cp "$PAPER/qualitative_figures/qualitative_plot_5.png" "$DEST/"
```

- [ ] **Step 2: Verify all files copied**

```bash
ls /fs/cml-projects/spec_decoding_furong/nerfies.github.io/static/images/
```

Expected: 15 new `.png` files plus the existing `favicon.svg`, `interpolate_end.jpg`, `interpolate_start.jpg`, `steve.webm`.

- [ ] **Step 3: Commit**

```bash
cd /fs/cml-projects/spec_decoding_furong/nerfies.github.io
git add static/images/
git commit -m "feat: add CAT paper figures to static/images"
```

---

## Task 2: Add CSS for captions and table row highlighting

**Files:**
- Modify: `static/css/index.css`

- [ ] **Step 1: Append new styles to index.css**

Open `static/css/index.css` and append the following at the end of the file:

```css
/* Figure captions */
.figure-caption {
  font-size: 0.9rem;
  color: #555;
  margin-top: 0.5rem;
  text-align: center;
}

.figure-caption-shared {
  font-size: 0.9rem;
  color: #333;
  margin-top: 0.75rem;
  text-align: center;
  font-style: italic;
}

/* Highlight CAT rows in result tables */
.cat-row {
  background-color: #fffbe6 !important;
  font-weight: 500;
}

/* Dense result tables */
.result-table {
  font-size: 0.75rem;
}

.result-table th {
  white-space: nowrap;
  font-size: 0.72rem;
}

/* Section spacing */
.section-heading {
  margin-top: 2rem;
  margin-bottom: 1rem;
}
```

- [ ] **Step 2: Commit**

```bash
cd /fs/cml-projects/spec_decoding_furong/nerfies.github.io
git add static/css/index.css
git commit -m "feat: add figure caption and table row highlight styles"
```

---

## Task 3: Rewrite index.html — head, navbar, hero

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace the full contents of index.html with the new skeleton through the hero section**

Replace the entire file with the following (subsequent tasks will append sections):

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="description"
        content="Compositional Adversarial Training (CAT) improves robust visual watermarking by training against a learned sequential differentiable adversary instead of random augmentation.">
  <meta name="keywords" content="CAT, watermarking, adversarial training, robust watermarking, VideoSeal, PixelSeal">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>CAT: Compositional Adversarial Training for Robust Visual Watermarking</title>

  <!-- Analytics removed -->

  <link href="https://fonts.googleapis.com/css?family=Google+Sans|Noto+Sans|Castoro"
        rel="stylesheet">

  <link rel="stylesheet" href="./static/css/bulma.min.css">
  <link rel="stylesheet" href="./static/css/bulma-carousel.min.css">
  <link rel="stylesheet" href="./static/css/bulma-slider.min.css">
  <link rel="stylesheet" href="./static/css/fontawesome.all.min.css">
  <link rel="stylesheet"
        href="https://cdn.jsdelivr.net/gh/jpswalsh/academicons@1/css/academicons.min.css">
  <link rel="stylesheet" href="./static/css/index.css">
  <link rel="icon" href="./static/images/favicon.svg">

  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
  <script defer src="./static/js/fontawesome.all.min.js"></script>
  <script src="./static/js/bulma-carousel.min.js"></script>
  <script src="./static/js/bulma-slider.min.js"></script>
  <script src="./static/js/index.js"></script>
</head>
<body>

<nav class="navbar" role="navigation" aria-label="main navigation">
  <div class="navbar-brand">
    <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false">
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
    </a>
  </div>
  <div class="navbar-menu">
    <div class="navbar-start" style="flex-grow: 1; justify-content: center;">
    </div>
  </div>
</nav>

<section class="hero">
  <div class="hero-body">
    <div class="container is-max-desktop">
      <div class="columns is-centered">
        <div class="column has-text-centered">
          <h1 class="title is-1 publication-title">Compositional Adversarial Training for Robust Visual Watermarking</h1>
          <div class="is-size-5 publication-authors">
            <span class="author-block">Anirudh Satheesh,</span>
            <span class="author-block">Michael-Andrei Panaitescu-Liess,</span>
            <span class="author-block">Andrew Xu,</span>
            <span class="author-block">Georgios Milis,</span>
            <span class="author-block">Heng Huang,</span>
            <span class="author-block">Zikui Cai,</span>
            <span class="author-block">Furong Huang</span>
          </div>

          <div class="is-size-5 publication-authors">
            <span class="author-block">University of Maryland</span>
          </div>

          <div class="column has-text-centered">
            <div class="publication-links">
              <span class="link-block">
                <a href="#"
                   class="external-link button is-normal is-rounded is-dark">
                  <span class="icon">
                    <i class="fas fa-file-pdf"></i>
                  </span>
                  <span>Paper</span>
                </a>
              </span>
              <span class="link-block">
                <a href="#"
                   class="external-link button is-normal is-rounded is-dark">
                  <span class="icon">
                    <i class="ai ai-arxiv"></i>
                  </span>
                  <span>arXiv</span>
                </a>
              </span>
              <span class="link-block">
                <a href="https://github.com/Asatheesh6561/CAT"
                   class="external-link button is-normal is-rounded is-dark">
                  <span class="icon">
                    <i class="fab fa-github"></i>
                  </span>
                  <span>Code</span>
                </a>
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Verify the file was written correctly**

```bash
head -60 /fs/cml-projects/spec_decoding_furong/nerfies.github.io/index.html
```

Expected: DOCTYPE, head with correct title, navbar with empty start, hero with title and three buttons.

- [ ] **Step 3: Commit**

```bash
cd /fs/cml-projects/spec_decoding_furong/nerfies.github.io
git add index.html
git commit -m "feat: add CAT hero section with title, authors, buttons"
```

---

## Task 4: Add overview figure section

**Files:**
- Modify: `index.html` (append after hero `</section>`)

- [ ] **Step 1: Append the overview figure section**

Append the following immediately after the closing `</section>` of the hero:

```html
<section class="section" style="padding-top: 1rem; padding-bottom: 1rem;">
  <div class="container is-max-desktop">
    <div class="columns is-centered">
      <div class="column is-full-width has-text-centered">
        <img src="./static/images/RobustWatermarkTeaser.png"
             alt="CAT overview: bit accuracy and capacity improvements under single-step and compositional attacks"
             style="max-width: 100%;">
        <p class="figure-caption">
          CAT improves overall bit accuracy by 2.2% and watermark capacity by 17.0% for single-step and compositional attacks.
        </p>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Commit**

```bash
cd /fs/cml-projects/spec_decoding_furong/nerfies.github.io
git add index.html
git commit -m "feat: add overview figure section"
```

---

## Task 5: Add abstract and method overview figure

**Files:**
- Modify: `index.html` (append)

- [ ] **Step 1: Append the abstract section with cat_overview-1.png**

```html
<section class="section">
  <div class="container is-max-desktop">
    <div class="columns is-centered has-text-centered">
      <div class="column is-four-fifths">
        <h2 class="title is-3">Abstract</h2>
        <div class="content has-text-justified">
          <p>
            Robust watermarking is typically trained with random post-processing augmentation, but random
            sampling under-covers the combinatorial space of realistic attack pipelines and rarely encounters the
            rare compositions that actually break detection. This leads to unstable training and poor sample
            efficiency. We instead formulate watermark robustness as a min-max problem over a structured space
            of compositional transformations. We propose <strong>Compositional Adversarial Training (CAT)</strong>,
            a plug-in framework that learns a sequential differentiable adversary that observes the current
            watermarked image and selects an attack family at each step to maximally disrupt message recovery.
            CAT combines a straight-through Gumbel-Softmax attack selection with entropy regularization, allowing
            the backward pass to be end-to-end differentiable and aggregate gradient information across attack
            families, yielding faster, smoother convergence without collapsing to a single attack mode.
            We evaluate CAT on post-generation watermarks VideoSeal 0.0, VideoSeal 1.0, and PixelSeal and
            in-generation WMAR under both single-step and two-step attack suites, on in-distribution and multiple
            out-of-distribution image and video benchmarks. CAT consistently outperforms random-augmentation
            baselines trained with the same augmentation budget, with the largest gains on hard composed attacks
            and OOD evaluations; improving overall watermark capacity by up to <strong>63.5%</strong> in the
            single-step attack setting and <strong>13.0%</strong> in the compositional setting. In the autoregressive
            setting, CAT improves the TPR@FPR=1% by <strong>12%</strong> on average over random training on
            difficult geometric transformations.
          </p>
        </div>
        <figure class="image" style="margin-top: 2rem;">
          <img src="./static/images/cat_overview-1.png"
               alt="Conceptual overview of the CAT training pipeline">
        </figure>
        <p class="figure-caption" style="margin-top: 0.75rem;">
          Overview of the CAT training pipeline. The embedder writes message <em>m</em> into image <em>x</em>;
          the sequential adversarial augmenter repeatedly observes the current image, selects an attack family
          via straight-through Gumbel-Softmax, and applies differentiable attacks; the extractor recovers the
          message and the message loss drives both watermark and adversary updates. Entropy regularization keeps
          the attack policy diverse.
        </p>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Commit**

```bash
cd /fs/cml-projects/spec_decoding_furong/nerfies.github.io
git add index.html
git commit -m "feat: add abstract and method overview figure"
```

---

## Task 6: Add method section

**Files:**
- Modify: `index.html` (append)

- [ ] **Step 1: Append the method section**

```html
<section class="section">
  <div class="container is-max-desktop">
    <div class="columns is-centered">
      <div class="column is-full-width">
        <h2 class="title is-3">Method</h2>

        <h3 class="title is-4">Problem Formulation</h3>
        <div class="content has-text-justified">
          <p>
            Given a watermarked image, we seek parameters for an embedder E<sub>θ</sub> and extractor D<sub>ψ</sub>
            that minimize message recovery error under worst-case compositional attacks. This yields a min-max objective:
            the watermark model minimizes message loss while a learned adversary A<sub>φ</sub> maximizes it over a
            structured library of realistic, differentiable attack families — covering value distortions, compression
            artifacts, and geometric transformations.
          </p>
        </div>

        <h3 class="title is-4">Sequential Attack Generator</h3>
        <div class="content has-text-justified">
          <p>
            The adversary instantiates as a controller over a library of <em>K</em> differentiable attack primitives.
            Starting from the watermarked image, it applies attacks sequentially for <em>T</em> steps, where each
            step's choice depends on the intermediate image produced by all previous steps. This lets the adversary
            discover order-sensitive compositions (e.g., blur → compression, resize → color distortion) that random
            augmentation rarely encounters. A <strong>frozen DINOv2 ViT-S/16 backbone</strong> extracts visual
            features at each step, and a lightweight <strong>GRU</strong> tracks the attack history to inform the
            next selection. A two-layer MLP maps the GRU hidden state to logits over attack families.
          </p>
        </div>

        <h3 class="title is-4">Differentiable Attack Selection</h3>
        <div class="content has-text-justified">
          <p>
            Discrete attack selection is made differentiable via a <strong>straight-through Gumbel-Softmax
            relaxation</strong>: the forward pass uses a one-hot sample (selecting one attack), while the backward
            pass uses the continuous relaxation so that gradients flow through the attack choice. All <em>K</em>
            primitives are evaluated in parallel and their outputs are combined as a weighted sum — enabling
            end-to-end training without a separate inner optimization loop.
          </p>
        </div>

        <h3 class="title is-4">Entropy Regularization and Training Efficiency</h3>
        <div class="content has-text-justified">
          <p>
            Without constraints, the adversary collapses to a single maximally destructive attack. An
            <strong>entropy bonus</strong> H(π<sub>φ</sub>) added to the adversary objective keeps the attack
            policy diverse throughout training, prevents premature over-specialization, and improves robustness
            beyond a single dominant failure mode. Because the adversary shares the watermark model's computational
            graph, no separate inner-loop optimization is needed — the adversary contributes only <strong>800K
            trainable parameters</strong> and <strong>20–30% additional training overhead</strong>, while leaving
            inference-time behavior entirely unchanged.
          </p>
        </div>

      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Commit**

```bash
cd /fs/cml-projects/spec_decoding_furong/nerfies.github.io
git add index.html
git commit -m "feat: add method section"
```

---

## Task 7: Add results — motivation figures and single-step table

**Files:**
- Modify: `index.html` (append)

- [ ] **Step 1: Append the results section header, motivation figures, and Table 1**

```html
<section class="section">
  <div class="container is-max-desktop">
    <div class="columns is-centered">
      <div class="column is-full-width">
        <h2 class="title is-3">Results</h2>

        <!-- Motivation figures -->
        <div class="columns is-vcentered">
          <div class="column has-text-centered">
            <img src="./static/images/rand_vs_adv_d1.png"
                 alt="Single-step augmentation training instability"
                 style="max-width: 100%;">
            <p class="figure-caption">(a) Single-step augmentation training</p>
          </div>
          <div class="column has-text-centered">
            <img src="./static/images/rand_vs_adv_d2.png"
                 alt="Compositional augmentation training instability"
                 style="max-width: 100%;">
            <p class="figure-caption">(b) Compositional augmentation training</p>
          </div>
        </div>
        <p class="figure-caption-shared" style="margin-bottom: 2rem;">
          Random augmentation creates unstable training due to inefficient augmentation allocations, whereas
          the learned adversary consistently targets the model's current weaknesses.
        </p>

        <!-- Single-step results -->
        <h3 class="title is-4 section-heading">Single-Step Attack Results (T=1)</h3>
        <div class="content">
          <p>
            Even a single learned attack step improves robustness over random augmentation under a fair
            compute-matched comparison. The largest gains appear for VideoSeal 1.0 and PixelSeal, especially on
            difficult geometric and combined attacks.
          </p>
        </div>

        <h4 class="title is-5">SA-1B (In-Distribution)</h4>
        <div class="table-container">
          <table class="table is-bordered is-striped is-hoverable is-fullwidth result-table">
            <thead>
              <tr>
                <th rowspan="2">Model (bits)</th>
                <th colspan="2">Identity</th>
                <th colspan="2">Value</th>
                <th colspan="2">Compression</th>
                <th colspan="2">Geometric</th>
                <th colspan="2">Combined</th>
                <th colspan="2">Overall</th>
              </tr>
              <tr>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>InvisMark (100)</td>
                <td>0.990</td><td>95.99</td><td>0.876</td><td>72.90</td>
                <td>0.954</td><td>88.45</td><td>0.828</td><td>63.25</td>
                <td>0.861</td><td>67.84</td><td>0.869</td><td>71.01</td>
              </tr>
              <tr>
                <td>TrustMark (100)</td>
                <td>0.996</td><td>98.92</td><td>0.956</td><td>86.28</td>
                <td>0.898</td><td>79.09</td><td>0.754</td><td>50.29</td>
                <td>0.993</td><td>97.90</td><td>0.889</td><td>76.08</td>
              </tr>
              <tr>
                <td>MBRS (256)</td>
                <td>0.987</td><td>242.60</td><td>0.915</td><td>185.99</td>
                <td>0.884</td><td>190.52</td><td>0.653</td><td>78.90</td>
                <td>0.959</td><td>217.48</td><td>0.834</td><td>158.92</td>
              </tr>
              <tr>
                <td>VideoSeal 0.0 (96)</td>
                <td>0.997</td><td>94.00</td><td>0.984</td><td>88.69</td>
                <td>0.980</td><td>86.86</td><td>0.945</td><td>75.58</td>
                <td>0.994</td><td>92.33</td><td>0.961</td><td>81.06</td>
              </tr>
              <tr class="cat-row">
                <td>+ CAT</td>
                <td>0.998</td><td>94.75</td><td>0.978</td><td>86.93</td>
                <td>0.986</td><td>89.21</td><td>0.953</td><td>78.60</td>
                <td>0.994</td><td>92.22</td><td><strong>0.966</strong></td><td><strong>82.85 ↑2.2%</strong></td>
              </tr>
              <tr>
                <td>VideoSeal 1.0 (256)</td>
                <td>0.898</td><td>135.17</td><td>0.879</td><td>123.45</td>
                <td>0.872</td><td>118.96</td><td>0.822</td><td>94.39</td>
                <td>0.892</td><td>130.60</td><td>0.846</td><td>106.41</td>
              </tr>
              <tr class="cat-row">
                <td>+ CAT</td>
                <td>0.941</td><td>175.63</td><td>0.857</td><td>129.47</td>
                <td>0.896</td><td>146.11</td><td>0.835</td><td>114.75</td>
                <td>0.921</td><td>160.39</td><td><strong>0.854</strong></td><td><strong>125.57 ↑18.0%</strong></td>
              </tr>
              <tr>
                <td>PixelSeal (128)</td>
                <td>0.918</td><td>76.46</td><td>0.895</td><td>68.65</td>
                <td>0.880</td><td>63.89</td><td>0.819</td><td>48.19</td>
                <td>0.902</td><td>70.27</td><td>0.849</td><td>56.21</td>
              </tr>
              <tr class="cat-row">
                <td>+ CAT</td>
                <td>0.986</td><td>117.73</td><td>0.956</td><td>102.90</td>
                <td>0.957</td><td>102.96</td><td>0.900</td><td>83.05</td>
                <td>0.973</td><td>109.36</td><td><strong>0.925</strong></td><td><strong>91.91 ↑63.5%</strong></td>
              </tr>
            </tbody>
          </table>
        </div>

        <h4 class="title is-5" style="margin-top: 1.5rem;">CLIC (Out-of-Distribution)</h4>
        <div class="table-container">
          <table class="table is-bordered is-striped is-hoverable is-fullwidth result-table">
            <thead>
              <tr>
                <th rowspan="2">Model (bits)</th>
                <th colspan="2">Identity</th>
                <th colspan="2">Value</th>
                <th colspan="2">Compression</th>
                <th colspan="2">Geometric</th>
                <th colspan="2">Combined</th>
                <th colspan="2">Overall</th>
              </tr>
              <tr>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>InvisMark (100)</td>
                <td>0.990</td><td>96.02</td><td>0.876</td><td>72.93</td>
                <td>0.691</td><td>35.10</td><td>0.825</td><td>62.83</td>
                <td>0.582</td><td>19.23</td><td>0.764</td><td>51.59</td>
              </tr>
              <tr>
                <td>TrustMark (100)</td>
                <td>0.993</td><td>98.39</td><td>0.959</td><td>87.60</td>
                <td>0.894</td><td>78.18</td><td>0.753</td><td>50.21</td>
                <td>0.947</td><td>84.07</td><td>0.878</td><td>73.03</td>
              </tr>
              <tr>
                <td>MBRS (256)</td>
                <td>0.987</td><td>243.37</td><td>0.922</td><td>191.47</td>
                <td>0.848</td><td>162.21</td><td>0.648</td><td>74.77</td>
                <td>0.775</td><td>105.06</td><td>0.786</td><td>128.44</td>
              </tr>
              <tr>
                <td>VideoSeal 0.0 (96)</td>
                <td>0.998</td><td>94.59</td><td>0.986</td><td>89.85</td>
                <td>0.977</td><td>86.11</td><td>0.948</td><td>76.61</td>
                <td>0.844</td><td>57.95</td><td>0.956</td><td>80.25</td>
              </tr>
              <tr class="cat-row">
                <td>+ CAT</td>
                <td>0.999</td><td>95.18</td><td>0.974</td><td>86.34</td>
                <td>0.982</td><td>87.96</td><td>0.957</td><td>79.74</td>
                <td>0.860</td><td>61.83</td><td><strong>0.961</strong></td><td><strong>81.84 ↑2.0%</strong></td>
              </tr>
              <tr>
                <td>VideoSeal 1.0 (256)</td>
                <td>0.900</td><td>136.47</td><td>0.883</td><td>125.61</td>
                <td>0.869</td><td>117.38</td><td>0.824</td><td>95.59</td>
                <td>0.766</td><td>78.96</td><td>0.842</td><td>105.00</td>
              </tr>
              <tr class="cat-row">
                <td>+ CAT</td>
                <td>0.946</td><td>179.81</td><td>0.853</td><td>129.33</td>
                <td>0.884</td><td>140.37</td><td>0.840</td><td>118.13</td>
                <td>0.723</td><td>81.29</td><td><strong>0.846</strong></td><td><strong>123.00 ↑17.1%</strong></td>
              </tr>
              <tr>
                <td>PixelSeal (128)</td>
                <td>0.921</td><td>77.60</td><td>0.900</td><td>70.26</td>
                <td>0.871</td><td>61.44</td><td>0.822</td><td>49.03</td>
                <td>0.748</td><td>40.15</td><td>0.844</td><td>55.26</td>
              </tr>
              <tr class="cat-row">
                <td>+ CAT</td>
                <td>0.992</td><td>121.32</td><td>0.946</td><td>101.38</td>
                <td>0.948</td><td>99.94</td><td>0.899</td><td>83.02</td>
                <td>0.842</td><td>72.27</td><td><strong>0.916</strong></td><td><strong>89.44 ↑61.8%</strong></td>
              </tr>
            </tbody>
          </table>
        </div>
```

- [ ] **Step 2: Commit**

```bash
cd /fs/cml-projects/spec_decoding_furong/nerfies.github.io
git add index.html
git commit -m "feat: add results section with motivation figures and single-step tables"
```

---

## Task 8: Add compositional attack table (Table 2)

**Files:**
- Modify: `index.html` (append inside the results `<section>`, after Task 7 content)

- [ ] **Step 1: Append compositional results — still inside the results section div, before its closing tags**

```html
        <!-- Compositional results -->
        <h3 class="title is-4 section-heading">Compositional Attack Results (T=2)</h3>
        <div class="content">
          <p>
            The advantage of CAT becomes clearest in the compositional setting, where the adversary applies a
            two-step attack sequence and must model both attack identity and order. Gains are concentrated on
            harder mixed and repeated attack pairs.
          </p>
        </div>

        <h4 class="title is-5">SA-1B (In-Distribution)</h4>
        <div class="table-container">
          <table class="table is-bordered is-striped is-hoverable is-fullwidth result-table">
            <thead>
              <tr>
                <th rowspan="2">Model (bits)</th>
                <th colspan="2">Val+Val</th>
                <th colspan="2">Val+Comp</th>
                <th colspan="2">Val+Geom</th>
                <th colspan="2">Comp+Comp</th>
                <th colspan="2">Comp+Geom</th>
                <th colspan="2">Geom+Geom</th>
                <th colspan="2">Overall</th>
              </tr>
              <tr>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>InvisMark (100)</td>
                <td>0.898</td><td>71.44</td><td>0.652</td><td>27.15</td>
                <td>0.875</td><td>68.63</td><td>0.474</td><td>0.85</td>
                <td>0.603</td><td>21.75</td><td>0.888</td><td>70.52</td>
                <td>0.813</td><td>57.92</td>
              </tr>
              <tr>
                <td>TrustMark (100)</td>
                <td>0.957</td><td>86.21</td><td>0.965</td><td>88.49</td>
                <td>0.786</td><td>52.86</td><td>0.974</td><td>90.92</td>
                <td>0.779</td><td>50.97</td><td>0.708</td><td>36.58</td>
                <td>0.834</td><td>62.14</td>
              </tr>
              <tr>
                <td>MBRS (256)</td>
                <td>0.917</td><td>182.87</td><td>0.836</td><td>130.67</td>
                <td>0.602</td><td>41.86</td><td>0.774</td><td>90.86</td>
                <td>0.554</td><td>15.81</td><td>0.495</td><td>0.98</td>
                <td>0.653</td><td>60.74</td>
              </tr>
              <tr>
                <td>VideoSeal 0.0 (96)</td>
                <td>0.972</td><td>83.44</td><td>0.985</td><td>87.84</td>
                <td>0.961</td><td>78.08</td><td>0.992</td><td>91.40</td>
                <td>0.974</td><td>82.79</td><td>0.930</td><td>72.83</td>
                <td>0.961</td><td>77.79</td>
              </tr>
              <tr class="cat-row">
                <td>+ CAT</td>
                <td>0.988</td><td>90.30</td><td>0.995</td><td>93.28</td>
                <td>0.979</td><td>86.26</td><td>0.999</td><td>95.34</td>
                <td>0.990</td><td>90.79</td><td>0.935</td><td>78.05</td>
                <td><strong>0.978</strong></td><td><strong>86.03 ↑10.6%</strong></td>
              </tr>
              <tr>
                <td>VideoSeal 1.0 (256)</td>
                <td>0.875</td><td>121.35</td><td>0.887</td><td>127.69</td>
                <td>0.827</td><td>95.41</td><td>0.897</td><td>134.39</td>
                <td>0.858</td><td>109.22</td><td>0.799</td><td>86.78</td>
                <td>0.829</td><td>96.13</td>
              </tr>
              <tr class="cat-row">
                <td>+ CAT</td>
                <td>0.840</td><td>121.57</td><td>0.891</td><td>145.41</td>
                <td>0.826</td><td>109.69</td><td>0.938</td><td>172.97</td>
                <td>0.894</td><td>141.66</td><td>0.825</td><td>111.74</td>
                <td><strong>0.827</strong></td><td><strong>108.30 ↑12.7%</strong></td>
              </tr>
              <tr>
                <td>PixelSeal (128)</td>
                <td>0.964</td><td>106.45</td><td>0.977</td><td>112.06</td>
                <td>0.954</td><td>100.25</td><td>0.987</td><td>117.75</td>
                <td>0.968</td><td>106.43</td><td>0.922</td><td>93.04</td>
                <td>0.952</td><td>98.76</td>
              </tr>
              <tr class="cat-row">
                <td>+ CAT</td>
                <td>0.974</td><td>113.81</td><td>0.990</td><td>121.27</td>
                <td>0.964</td><td>107.65</td><td>0.998</td><td>126.29</td>
                <td>0.982</td><td>116.19</td><td>0.928</td><td>100.21</td>
                <td><strong>0.965</strong></td><td><strong>107.73 ↑9.1%</strong></td>
              </tr>
            </tbody>
          </table>
        </div>

        <h4 class="title is-5" style="margin-top: 1.5rem;">CLIC (Out-of-Distribution)</h4>
        <div class="table-container">
          <table class="table is-bordered is-striped is-hoverable is-fullwidth result-table">
            <thead>
              <tr>
                <th rowspan="2">Model (bits)</th>
                <th colspan="2">Val+Val</th>
                <th colspan="2">Val+Comp</th>
                <th colspan="2">Val+Geom</th>
                <th colspan="2">Comp+Comp</th>
                <th colspan="2">Comp+Geom</th>
                <th colspan="2">Geom+Geom</th>
                <th colspan="2">Overall</th>
              </tr>
              <tr>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>InvisMark (100)</td>
                <td>0.902</td><td>72.69</td><td>0.653</td><td>27.61</td>
                <td>0.875</td><td>68.97</td><td>0.474</td><td>0.85</td>
                <td>0.600</td><td>21.29</td><td>0.883</td><td>69.50</td>
                <td>0.812</td><td>57.96</td>
              </tr>
              <tr>
                <td>TrustMark (100)</td>
                <td>0.964</td><td>88.76</td><td>0.968</td><td>89.85</td>
                <td>0.790</td><td>53.95</td><td>0.974</td><td>91.65</td>
                <td>0.782</td><td>51.93</td><td>0.710</td><td>37.13</td>
                <td>0.838</td><td>63.39</td>
              </tr>
              <tr>
                <td>MBRS (256)</td>
                <td>0.927</td><td>190.84</td><td>0.851</td><td>140.04</td>
                <td>0.608</td><td>45.61</td><td>0.791</td><td>100.83</td>
                <td>0.559</td><td>18.03</td><td>0.496</td><td>0.97</td>
                <td>0.660</td><td>65.18</td>
              </tr>
              <tr>
                <td>VideoSeal 0.0 (96)</td>
                <td>0.978</td><td>86.28</td><td>0.961</td><td>81.15</td>
                <td>0.968</td><td>80.81</td><td>0.937</td><td>77.05</td>
                <td>0.947</td><td>75.52</td><td>0.937</td><td>74.67</td>
                <td>0.957</td><td>77.31</td>
              </tr>
              <tr class="cat-row">
                <td>+ CAT</td>
                <td>0.992</td><td>91.87</td><td>0.991</td><td>91.84</td>
                <td>0.984</td><td>88.57</td><td>0.977</td><td>89.05</td>
                <td>0.988</td><td>89.97</td><td>0.940</td><td>79.73</td>
                <td><strong>0.981</strong></td><td><strong>87.34 ↑13.0%</strong></td>
              </tr>
              <tr>
                <td>VideoSeal 1.0 (256)</td>
                <td>0.881</td><td>124.44</td><td>0.886</td><td>127.38</td>
                <td>0.832</td><td>98.03</td><td>0.895</td><td>133.09</td>
                <td>0.854</td><td>106.99</td><td>0.800</td><td>87.42</td>
                <td>0.831</td><td>96.97</td>
              </tr>
              <tr class="cat-row">
                <td>+ CAT</td>
                <td>0.852</td><td>128.33</td><td>0.869</td><td>136.19</td>
                <td>0.839</td><td>117.17</td><td>0.909</td><td>157.25</td>
                <td>0.878</td><td>134.59</td><td>0.831</td><td>115.09</td>
                <td><strong>0.827</strong></td><td><strong>109.24 ↑12.7%</strong></td>
              </tr>
              <tr>
                <td>PixelSeal (128)</td>
                <td>0.973</td><td>111.00</td><td>0.939</td><td>98.69</td>
                <td>0.961</td><td>103.61</td><td>0.902</td><td>90.40</td>
                <td>0.926</td><td>92.72</td><td>0.927</td><td>94.93</td>
                <td>0.941</td><td>96.20</td>
              </tr>
              <tr class="cat-row">
                <td>+ CAT</td>
                <td>0.977</td><td>115.17</td><td>0.980</td><td>115.86</td>
                <td>0.967</td><td>108.95</td><td>0.969</td><td>114.39</td>
                <td>0.970</td><td>110.31</td><td>0.929</td><td>100.63</td>
                <td><strong>0.962</strong></td><td><strong>106.43 ↑10.6%</strong></td>
              </tr>
            </tbody>
          </table>
        </div>
```

- [ ] **Step 2: Commit**

```bash
cd /fs/cml-projects/spec_decoding_furong/nerfies.github.io
git add index.html
git commit -m "feat: add compositional attack result tables"
```

---

## Task 9: Add convergence figures, image quality table, video results

**Files:**
- Modify: `index.html` (append, still inside the results section)

- [ ] **Step 1: Append convergence, image quality, and video sections**

```html
        <!-- Convergence -->
        <h3 class="title is-4 section-heading">Training Convergence</h3>
        <div class="columns is-vcentered">
          <div class="column has-text-centered">
            <img src="./static/images/pixelseal_convergence.png"
                 alt="PixelSeal training convergence: CAT vs random augmentation"
                 style="max-width: 100%;">
            <p class="figure-caption">(a) PixelSeal</p>
          </div>
          <div class="column has-text-centered">
            <img src="./static/images/videoseal_convergence.png"
                 alt="VideoSeal training convergence: CAT vs random augmentation"
                 style="max-width: 100%;">
            <p class="figure-caption">(b) VideoSeal</p>
          </div>
        </div>
        <p class="figure-caption-shared" style="margin-bottom: 2rem;">
          CAT substantially accelerates convergence for both PixelSeal and VideoSeal, reaching lower validation
          bit error earlier than random augmentation. This advantage persists from single-step to compositional training.
        </p>

        <!-- Image quality -->
        <h3 class="title is-4 section-heading">Image Quality</h3>
        <div class="content">
          <p>CAT preserves visual quality while improving robustness. All CAT-trained models remain very close
          to their compute-matched random-augmentation baselines on standard perceptual metrics.</p>
        </div>
        <div class="table-container">
          <table class="table is-bordered is-striped is-hoverable is-fullwidth result-table">
            <thead>
              <tr>
                <th rowspan="2">Model</th>
                <th colspan="4">SA-1B</th>
                <th colspan="4">DIV2K</th>
              </tr>
              <tr>
                <th>PSNR ↑</th><th>SSIM ↑</th><th>MS-SSIM ↑</th><th>LPIPS ↓</th>
                <th>PSNR ↑</th><th>SSIM ↑</th><th>MS-SSIM ↑</th><th>LPIPS ↓</th>
              </tr>
            </thead>
            <tbody>
              <tr><td>InvisMark</td><td>48.77</td><td>0.9955</td><td>0.9964</td><td>0.0018</td><td>49.11</td><td>0.9943</td><td>0.9960</td><td>0.0016</td></tr>
              <tr><td>TrustMark</td><td>41.37</td><td>0.9943</td><td>0.9917</td><td>0.0029</td><td>41.19</td><td>0.9935</td><td>0.9919</td><td>0.0027</td></tr>
              <tr><td>MBRS</td><td>45.58</td><td>0.9959</td><td>0.9965</td><td>0.0032</td><td>45.22</td><td>0.9954</td><td>0.9966</td><td>0.0034</td></tr>
              <tr><td>VideoSeal 0.0</td><td>42.50</td><td>0.9934</td><td>0.9949</td><td>0.0049</td><td>42.11</td><td>0.9910</td><td>0.9944</td><td>0.0057</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>42.21</td><td>0.9935</td><td>0.9953</td><td>0.0040</td><td>41.81</td><td>0.9911</td><td>0.9947</td><td>0.0046</td></tr>
              <tr><td>VideoSeal 1.0</td><td>42.58</td><td>0.9936</td><td>0.9950</td><td>0.0046</td><td>42.19</td><td>0.9913</td><td>0.9945</td><td>0.0053</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>42.17</td><td>0.9934</td><td>0.9951</td><td>0.0039</td><td>41.75</td><td>0.9909</td><td>0.9946</td><td>0.0045</td></tr>
              <tr><td>PixelSeal</td><td>43.22</td><td>0.9958</td><td>0.9965</td><td>0.0021</td><td>42.71</td><td>0.9940</td><td>0.9961</td><td>0.0023</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>42.64</td><td>0.9956</td><td>0.9963</td><td>0.0021</td><td>42.17</td><td>0.9937</td><td>0.9958</td><td>0.0024</td></tr>
            </tbody>
          </table>
        </div>

        <!-- Video results -->
        <h3 class="title is-4 section-heading">Video Watermarking</h3>
        <div class="content">
          <p>CAT is most helpful on the hardest compositional and temporal video corruptions, evaluated on
          in-distribution Movie-Gen-Bench and out-of-distribution SA-V.</p>
        </div>

        <h4 class="title is-5">Single-Step Video Results</h4>
        <div class="table-container">
          <table class="table is-bordered is-striped is-hoverable is-fullwidth result-table">
            <thead>
              <tr>
                <th rowspan="2">Model (bits)</th>
                <th colspan="2">Identity</th>
                <th colspan="2">Value</th>
                <th colspan="2">Compression</th>
                <th colspan="2">Geometric</th>
                <th colspan="2">Temporal</th>
                <th colspan="2">Combined</th>
                <th colspan="2">Overall</th>
              </tr>
              <tr>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
              </tr>
            </thead>
            <tbody>
              <tr><td colspan="15" style="background:#f5f5f5; font-weight:bold;">Movie-Gen-Bench (ID)</td></tr>
              <tr><td>RivaGAN (32)</td><td>0.889</td><td>20.36</td><td>0.691</td><td>9.42</td><td>0.726</td><td>9.86</td><td>0.747</td><td>10.39</td><td>0.809</td><td>14.43</td><td>0.511</td><td>1.27</td><td>0.754</td><td>11.39</td></tr>
              <tr><td>VideoSeal 0.0 (96)</td><td>0.951</td><td>69.97</td><td>0.930</td><td>62.37</td><td>0.843</td><td>45.80</td><td>0.942</td><td>67.88</td><td>0.905</td><td>59.74</td><td>0.724</td><td>16.74</td><td>0.912</td><td>60.95</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>0.952</td><td>70.04</td><td>0.934</td><td>63.67</td><td>0.915</td><td>59.00</td><td>0.946</td><td>68.95</td><td>0.941</td><td>67.57</td><td>0.870</td><td>44.80</td><td><strong>0.936</strong></td><td><strong>65.76 ↑7.9%</strong></td></tr>
              <tr><td>VideoSeal 1.0 (256)</td><td>0.861</td><td>107.64</td><td>0.823</td><td>87.28</td><td>0.742</td><td>65.12</td><td>0.848</td><td>103.34</td><td>0.809</td><td>90.11</td><td>0.601</td><td>9.66</td><td>0.815</td><td>90.48</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>0.849</td><td>100.44</td><td>0.829</td><td>89.90</td><td>0.828</td><td>89.43</td><td>0.843</td><td>98.74</td><td>0.847</td><td>100.01</td><td>0.792</td><td>69.22</td><td><strong>0.838</strong></td><td><strong>95.47 ↑5.5%</strong></td></tr>
              <tr><td>PixelSeal (128)</td><td>0.805</td><td>37.54</td><td>0.719</td><td>20.34</td><td>0.683</td><td>19.89</td><td>0.789</td><td>34.95</td><td>0.754</td><td>30.59</td><td>0.561</td><td>2.60</td><td>0.750</td><td>28.96</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>0.806</td><td>37.84</td><td>0.728</td><td>21.93</td><td>0.726</td><td>23.98</td><td>0.796</td><td>36.62</td><td>0.778</td><td>33.62</td><td>0.651</td><td>10.65</td><td><strong>0.768</strong></td><td><strong>31.37 ↑8.3%</strong></td></tr>
              <tr><td colspan="15" style="background:#f5f5f5; font-weight:bold;">SAV-Test (OOD)</td></tr>
              <tr><td>RivaGAN (32)</td><td>0.941</td><td>25.13</td><td>0.740</td><td>13.02</td><td>0.776</td><td>13.66</td><td>0.812</td><td>14.94</td><td>0.868</td><td>19.17</td><td>0.502</td><td>2.05</td><td>0.811</td><td>15.68</td></tr>
              <tr><td>VideoSeal 0.0 (96)</td><td>0.945</td><td>68.05</td><td>0.914</td><td>57.84</td><td>0.834</td><td>43.75</td><td>0.933</td><td>65.09</td><td>0.897</td><td>57.69</td><td>0.716</td><td>16.33</td><td>0.903</td><td>58.21</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>0.952</td><td>70.46</td><td>0.908</td><td>57.43</td><td>0.889</td><td>53.14</td><td>0.923</td><td>63.18</td><td>0.926</td><td>63.30</td><td>0.794</td><td>29.14</td><td><strong>0.913</strong></td><td><strong>59.97 ↑3.0%</strong></td></tr>
              <tr><td>VideoSeal 1.0 (256)</td><td>0.851</td><td>101.68</td><td>0.823</td><td>87.24</td><td>0.739</td><td>63.77</td><td>0.842</td><td>100.10</td><td>0.804</td><td>87.90</td><td>0.599</td><td>9.54</td><td>0.811</td><td>88.22</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>0.841</td><td>95.59</td><td>0.827</td><td>89.13</td><td>0.808</td><td>82.13</td><td>0.834</td><td>94.25</td><td>0.832</td><td>93.66</td><td>0.752</td><td>55.46</td><td><strong>0.826</strong></td><td><strong>90.53 ↑2.6%</strong></td></tr>
              <tr><td>PixelSeal (128)</td><td>0.798</td><td>36.26</td><td>0.687</td><td>16.19</td><td>0.671</td><td>17.79</td><td>0.763</td><td>29.82</td><td>0.733</td><td>26.26</td><td>0.525</td><td>0.95</td><td>0.727</td><td>24.72</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>0.798</td><td>36.10</td><td>0.691</td><td>16.93</td><td>0.704</td><td>20.66</td><td>0.765</td><td>30.26</td><td>0.750</td><td>28.00</td><td>0.552</td><td>2.45</td><td><strong>0.737</strong></td><td><strong>25.85 ↑4.6%</strong></td></tr>
            </tbody>
          </table>
        </div>

        <h4 class="title is-5" style="margin-top: 1.5rem;">Compositional Video Results</h4>
        <div class="table-container">
          <table class="table is-bordered is-striped is-hoverable is-fullwidth result-table">
            <thead>
              <tr>
                <th rowspan="2">Model (bits)</th>
                <th colspan="2">Val+Val</th>
                <th colspan="2">Val+Geom</th>
                <th colspan="2">Comp+Comp</th>
                <th colspan="2">Comp+Geom</th>
                <th colspan="2">Geom+Geom</th>
                <th colspan="2">Geom+Temp</th>
                <th colspan="2">Temp+Temp</th>
                <th colspan="2">Overall</th>
              </tr>
              <tr>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
                <th>Bit acc. ↑</th><th>Cap. ↑</th>
              </tr>
            </thead>
            <tbody>
              <tr><td colspan="17" style="background:#f5f5f5; font-weight:bold;">Movie-Gen-Bench (ID)</td></tr>
              <tr><td>RivaGAN (32)</td><td>0.701</td><td>8.57</td><td>0.740</td><td>10.03</td><td>0.715</td><td>9.03</td><td>0.740</td><td>10.01</td><td>0.772</td><td>11.05</td><td>0.820</td><td>14.54</td><td>0.873</td><td>18.98</td><td>0.758</td><td>11.39</td></tr>
              <tr><td>VideoSeal 0.0 (96)</td><td>0.947</td><td>69.20</td><td>0.978</td><td>82.26</td><td>0.825</td><td>40.55</td><td>0.975</td><td>81.26</td><td>0.961</td><td>76.52</td><td>0.978</td><td>82.34</td><td>0.904</td><td>60.87</td><td>0.967</td><td>79.19</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>0.937</td><td>66.09</td><td>0.973</td><td>80.01</td><td>0.937</td><td>65.17</td><td>0.974</td><td>80.32</td><td>0.960</td><td>75.96</td><td>0.976</td><td>81.39</td><td>0.960</td><td>74.65</td><td><strong>0.972</strong></td><td><strong>79.52 ↑0.4%</strong></td></tr>
              <tr><td>VideoSeal 1.0 (256)</td><td>0.823</td><td>87.28</td><td>0.869</td><td>113.11</td><td>0.658</td><td>33.70</td><td>0.867</td><td>112.26</td><td>0.839</td><td>99.39</td><td>0.869</td><td>113.42</td><td>0.749</td><td>66.80</td><td>0.853</td><td>106.90</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>0.829</td><td>89.90</td><td>0.860</td><td>107.49</td><td>0.809</td><td>78.77</td><td>0.857</td><td>105.42</td><td>0.835</td><td>95.19</td><td>0.859</td><td>106.48</td><td>0.835</td><td>93.55</td><td><strong>0.855</strong></td><td><strong>104.51</strong></td></tr>
              <tr><td>PixelSeal (128)</td><td>0.926</td><td>82.75</td><td>0.979</td><td>111.32</td><td>0.684</td><td>26.08</td><td>0.974</td><td>108.33</td><td>0.951</td><td>100.14</td><td>0.981</td><td>112.26</td><td>0.812</td><td>64.48</td><td>0.956</td><td>104.64</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>0.929</td><td>85.54</td><td>0.978</td><td>111.36</td><td>0.935</td><td>87.67</td><td>0.975</td><td>109.22</td><td>0.959</td><td>102.94</td><td>0.982</td><td>113.45</td><td>0.964</td><td>103.51</td><td><strong>0.976</strong></td><td><strong>110.10 ↑5.2%</strong></td></tr>
              <tr><td colspan="17" style="background:#f5f5f5; font-weight:bold;">SAV-Test (OOD)</td></tr>
              <tr><td>RivaGAN (32)</td><td>0.757</td><td>12.04</td><td>0.804</td><td>14.42</td><td>0.765</td><td>12.57</td><td>0.791</td><td>13.93</td><td>0.844</td><td>16.31</td><td>0.886</td><td>19.91</td><td>0.929</td><td>23.94</td><td>0.816</td><td>15.71</td></tr>
              <tr><td>VideoSeal 0.0 (96)</td><td>0.921</td><td>61.62</td><td>0.960</td><td>75.47</td><td>0.777</td><td>32.79</td><td>0.957</td><td>74.38</td><td>0.939</td><td>69.05</td><td>0.959</td><td>75.16</td><td>0.866</td><td>53.00</td><td>0.947</td><td>72.21</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>0.905</td><td>56.81</td><td>0.958</td><td>73.96</td><td>0.877</td><td>51.74</td><td>0.953</td><td>72.46</td><td>0.935</td><td>67.30</td><td>0.956</td><td>73.34</td><td>0.920</td><td>63.76</td><td><strong>0.951</strong></td><td><strong>72.13</strong></td></tr>
              <tr><td>VideoSeal 1.0 (256)</td><td>0.823</td><td>87.24</td><td>0.864</td><td>110.45</td><td>0.656</td><td>33.32</td><td>0.862</td><td>109.44</td><td>0.834</td><td>95.91</td><td>0.864</td><td>110.56</td><td>0.744</td><td>65.24</td><td>0.848</td><td>104.30</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>0.827</td><td>89.13</td><td>0.850</td><td>101.99</td><td>0.782</td><td>69.44</td><td>0.848</td><td>101.16</td><td>0.827</td><td>91.11</td><td>0.849</td><td>101.94</td><td>0.814</td><td>85.39</td><td><strong>0.844</strong></td><td><strong>99.05</strong></td></tr>
              <tr><td>PixelSeal (128)</td><td>0.832</td><td>53.45</td><td>0.915</td><td>83.98</td><td>0.653</td><td>20.14</td><td>0.907</td><td>80.49</td><td>0.875</td><td>70.21</td><td>0.914</td><td>83.08</td><td>0.773</td><td>50.66</td><td>0.891</td><td>78.13</td></tr>
              <tr class="cat-row"><td>+ CAT</td><td>0.897</td><td>73.02</td><td>0.956</td><td>98.80</td><td>0.855</td><td>64.09</td><td>0.951</td><td>96.65</td><td>0.928</td><td>88.32</td><td>0.957</td><td>99.07</td><td>0.908</td><td>83.58</td><td><strong>0.948</strong></td><td><strong>96.18 ↑23.1%</strong></td></tr>
            </tbody>
          </table>
        </div>
```

- [ ] **Step 2: Commit**

```bash
cd /fs/cml-projects/spec_decoding_furong/nerfies.github.io
git add index.html
git commit -m "feat: add convergence, image quality, and video result tables"
```

---

## Task 10: Add autoregressive results and close the results section

**Files:**
- Modify: `index.html` (append, then close the results section)

- [ ] **Step 1: Append autoregressive subsection and close the results section**

```html
        <!-- Autoregressive results -->
        <h3 class="title is-4 section-heading">Autoregressive Watermarking</h3>
        <div class="content">
          <p>
            We evaluate CAT in the autoregressive image-generation setting using the WMAR framework on
            Taming and RAR-XL generators. Robustness is measured via TPR@FPR=1% under no attack, value
            perturbations, geometric perturbations, adversarial purification, and neural compression.
          </p>
        </div>

        <div class="columns">
          <div class="column">
            <h4 class="title is-5">Taming</h4>
            <div class="table-container">
              <table class="table is-bordered is-striped is-hoverable is-fullwidth result-table">
                <thead>
                  <tr>
                    <th>Method</th>
                    <th>None</th><th>Value</th><th>Geometric</th>
                    <th>Adv. Purif.</th><th>Neural Comp.</th>
                  </tr>
                </thead>
                <tbody>
                  <tr><td>BASE</td><td>1.00</td><td>0.26</td><td style="color:#c0392b; font-weight:bold;">0.01</td><td>0.69</td><td>0.71</td></tr>
                  <tr><td>Random Aug.</td><td>1.00</td><td>0.94</td><td style="color:#c0392b; font-weight:bold;">0.38</td><td>0.92</td><td>0.90</td></tr>
                  <tr><td>Random Aug.+Sync</td><td>0.99</td><td>0.90</td><td>0.74</td><td>0.92</td><td>0.89</td></tr>
                  <tr class="cat-row"><td>CAT</td><td>1.00</td><td>0.94</td><td>0.52</td><td>0.89</td><td>0.87</td></tr>
                  <tr class="cat-row"><td>CAT+Sync</td><td>0.99</td><td>0.89</td><td><strong>0.71</strong></td><td>0.89</td><td>0.87</td></tr>
                </tbody>
              </table>
            </div>
          </div>
          <div class="column">
            <h4 class="title is-5">RAR-XL</h4>
            <div class="table-container">
              <table class="table is-bordered is-striped is-hoverable is-fullwidth result-table">
                <thead>
                  <tr>
                    <th>Method</th>
                    <th>None</th><th>Value</th><th>Geometric</th>
                    <th>Adv. Purif.</th><th>Neural Comp.</th>
                  </tr>
                </thead>
                <tbody>
                  <tr><td>BASE</td><td>1.00</td><td>0.53</td><td style="color:#c0392b; font-weight:bold;">0.04</td><td>0.63</td><td>0.77</td></tr>
                  <tr><td>Random Aug.</td><td>0.99</td><td>0.97</td><td style="color:#c0392b; font-weight:bold;">0.25</td><td>1.00</td><td>1.00</td></tr>
                  <tr><td>Random Aug.+Sync</td><td>0.99</td><td>0.95</td><td style="color:#c0392b; font-weight:bold;">0.38</td><td>1.00</td><td>1.00</td></tr>
                  <tr class="cat-row"><td>CAT</td><td>1.00</td><td>0.92</td><td style="color:#c0392b; font-weight:bold;">0.35</td><td>0.99</td><td>0.98</td></tr>
                  <tr class="cat-row"><td>CAT+Sync</td><td>1.00</td><td>0.86</td><td><strong>0.72</strong></td><td>0.99</td><td>0.97</td></tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
        <p class="figure-caption-shared" style="margin-bottom: 1.5rem;">
          TPR@FPR=1% — higher is better. Values below 0.50 indicate failed detection.
        </p>

        <div class="columns">
          <div class="column has-text-centered">
            <img src="./static/images/taming_robustness.png"
                 alt="Taming: continuous attack sweeps" style="max-width: 100%;">
            <p class="figure-caption">(a) Taming: continuous attack sweeps</p>
          </div>
          <div class="column has-text-centered">
            <img src="./static/images/rar_robustness.png"
                 alt="RAR-XL: continuous attack sweeps" style="max-width: 100%;">
            <p class="figure-caption">(b) RAR-XL: continuous attack sweeps</p>
          </div>
        </div>
        <div class="columns" style="margin-top: 1rem;">
          <div class="column has-text-centered">
            <img src="./static/images/taming_auc.png"
                 alt="Taming: ROC curves" style="max-width: 100%;">
            <p class="figure-caption">(c) Taming: ROC curves</p>
          </div>
          <div class="column has-text-centered">
            <img src="./static/images/rar_auc.png"
                 alt="RAR-XL: ROC curves" style="max-width: 100%;">
            <p class="figure-caption">(d) RAR-XL: ROC curves</p>
          </div>
        </div>

      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Commit**

```bash
cd /fs/cml-projects/spec_decoding_furong/nerfies.github.io
git add index.html
git commit -m "feat: add autoregressive watermarking results"
```

---

## Task 11: Add qualitative results section

**Files:**
- Modify: `index.html` (append)

- [ ] **Step 1: Append qualitative results section**

```html
<section class="section">
  <div class="container is-max-desktop">
    <div class="columns is-centered">
      <div class="column is-full-width">
        <h2 class="title is-3">Qualitative Results</h2>
        <div class="content">
          <p>Watermarked images under single-step and compositional attacks. CAT (Ours) consistently
          recovers more bits than random augmentation across all attack types while maintaining
          imperceptible watermarks.</p>
        </div>

        <figure class="image" style="margin-bottom: 1.5rem;">
          <img src="./static/images/qualitative_plot_1.png" alt="Qualitative results example 1" style="max-width: 100%;">
        </figure>
        <figure class="image" style="margin-bottom: 1.5rem;">
          <img src="./static/images/qualitative_plot_2.png" alt="Qualitative results example 2" style="max-width: 100%;">
        </figure>
        <figure class="image" style="margin-bottom: 1.5rem;">
          <img src="./static/images/qualitative_plot_3.png" alt="Qualitative results example 3" style="max-width: 100%;">
        </figure>
        <figure class="image" style="margin-bottom: 1.5rem;">
          <img src="./static/images/qualitative_plot_4.png" alt="Qualitative results example 4" style="max-width: 100%;">
        </figure>
        <figure class="image" style="margin-bottom: 1.5rem;">
          <img src="./static/images/qualitative_plot_5.png" alt="Qualitative results example 5" style="max-width: 100%;">
        </figure>

      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Commit**

```bash
cd /fs/cml-projects/spec_decoding_furong/nerfies.github.io
git add index.html
git commit -m "feat: add qualitative results section"
```

---

## Task 12: Add BibTeX section and footer, close body/html

**Files:**
- Modify: `index.html` (append — final content)

- [ ] **Step 1: Append BibTeX section and footer**

```html
<section class="section" id="BibTeX">
  <div class="container is-max-desktop content">
    <h2 class="title">BibTeX</h2>
    <pre><code>@article{satheesh2026cat,
  author    = {Satheesh, Anirudh and Panaitescu-Liess, Michael-Andrei and Xu, Andrew and Milis, Georgios and Huang, Heng and Cai, Zikui and Huang, Furong},
  title     = {Compositional Adversarial Training for Robust Visual Watermarking},
  note      = {Under review, ICML 2026},
  year      = {2026},
}</code></pre>
  </div>
</section>


<footer class="footer">
  <div class="container">
    <div class="columns is-centered">
      <div class="column is-8">
        <div class="content has-text-centered">
          <p>
            This website is licensed under a <a rel="license"
              href="http://creativecommons.org/licenses/by-sa/4.0/">Creative
            Commons Attribution-ShareAlike 4.0 International License</a>.
            The website template is borrowed from <a href="https://github.com/nerfies/nerfies.github.io">Nerfies</a>.
          </p>
        </div>
      </div>
    </div>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Verify the file is well-formed**

```bash
grep -c "<section" /fs/cml-projects/spec_decoding_furong/nerfies.github.io/index.html
grep -c "</section>" /fs/cml-projects/spec_decoding_furong/nerfies.github.io/index.html
```

Expected: both counts match (should be 6: hero, overview, abstract, method, results, qualitative, bibtex — actually 7).

```bash
grep -c "<div" /fs/cml-projects/spec_decoding_furong/nerfies.github.io/index.html
grep -c "</div>" /fs/cml-projects/spec_decoding_furong/nerfies.github.io/index.html
```

Expected: both counts match exactly.

- [ ] **Step 3: Commit**

```bash
cd /fs/cml-projects/spec_decoding_furong/nerfies.github.io
git add index.html
git commit -m "feat: add BibTeX section and footer — complete CAT project page"
```

---

## Self-Review

**Spec coverage check:**

| Spec requirement | Task |
|-----------------|------|
| Copy all figures to static/images/ | Task 1 |
| CSS for captions and CAT-row highlighting | Task 2 |
| Navbar (empty) | Task 3 |
| Hero: title, authors, affiliation, 3 buttons | Task 3 |
| Overview figure (RobustWatermarkTeaser.png) | Task 4 |
| Abstract verbatim + cat_overview-1.png | Task 5 |
| Method section (4 subsections, no figure) | Task 6 |
| Results: rand_vs_adv_d1.png + d2.png side by side | Task 7 |
| Table 1 single-step SA-1B | Task 7 |
| Table 1 single-step CLIC | Task 7 |
| Table 2 compositional SA-1B | Task 8 |
| Table 2 compositional CLIC | Task 8 |
| Convergence figures side by side | Task 9 |
| Table 5 image quality | Task 9 |
| Tables 9 & 10 video results | Task 9 |
| Tables 11 & 12 + 4 autoregressive figures | Task 10 |
| Qualitative plots 1–5 | Task 11 |
| BibTeX block | Task 12 |
| Footer with CC license + nerfies credit | Task 12 |
| Remove Google Analytics | Task 3 (replaced with comment) |

**Placeholder scan:** No TBDs, TODOs, or vague instructions found. All table data is fully spelled out with exact numbers from the paper.

**Type consistency:** All image paths use `./static/images/<filename>.png` consistently across all tasks. CSS class names (`cat-row`, `result-table`, `figure-caption`, `figure-caption-shared`, `section-heading`) are defined in Task 2 and used consistently in Tasks 7–11.
