# Quantum Dream Weaver v4.0

**Quantum Dream Weaver v4.0** is a single-file browser-based generative art studio powered by TensorFlow.js. It explores random neural generator architectures, combines visual latent vectors with optional text embeddings, and produces abstract procedural images that can be evolved, scored, curated, remixed, saved, and reloaded.

This version is a direct upgrade of the original Quantum Dream Weaver v3.2.2. It keeps the existing meta-exploration, text conditioning, latent interpolation, style reference, architecture liking, model admixture, save/load, and PNG export features while adding a modern interface, reproducible seeds, gallery tools, pattern scoring, session export/import, palettes, post-processing effects, safer TensorFlow memory handling, and richer exploration controls.

---

## Features

### Meta-generative exploration

* Randomly samples neural generator architectures.
* Runs multiple architecture generations per epoch.
* Runs multiple latent nuance variations per architecture.
* Supports finite or infinite exploration loops.
* Allows search-space drift between epochs.
* Can bias future exploration toward liked outputs or a style reference.

### TensorFlow.js neural generator

* Runs fully in the browser using TensorFlow.js.
* Uses a custom serializable `DynamicQuantumLayer`.
* Supports dense neural generator blocks with optional residual connections.
* Adds harmonic modulation for richer abstract textures.
* Supports WebGL, WASM, or CPU TensorFlow.js backends.

### Text-conditioned generation

* Optional text prompt conditioning using Universal Sentence Encoder.
* Visual latent vectors can be combined with 512-dimensional text embeddings.
* Text embeddings are cached for faster repeated generation.
* If no prompt is used, the system works as a pure visual latent generator.

### Latent space tools

* Generate new patterns from the current architecture.
* Set latent point A and latent point B.
* Interpolate smoothly between two visual latent points.
* Run short traversal animations between nuance variations.
* Run long latent animation with configurable FPS.

### Artistic guidance

* Like a pattern to keep its architecture and latent vector.
* Maintain a pool of liked architectures for future mutation.
* Set the current architecture as a style reference.
* Remix from a style reference.
* Automatically like high-scoring outputs with auto-curation.

### Architecture admixture

* Select two compatible architectures as A and B.
* Blend matching model weights using an A/B mix slider.
* Create a new admixture model from the averaged weights.

### Pattern scoring

Each generated image is analysed with lightweight visual metrics:

* Entropy
* Contrast
* Edge flow
* Symmetry
* Balance
* Overall score

These scores can be used manually or with auto-curation to guide exploration.

### Gallery and sessions

* Pin outputs to a local gallery.
* Batch-generate multiple variations and add them to the gallery.
* Click gallery thumbnails to restore an output preview.
* Export a session JSON containing UI settings, gallery thumbnails, metadata, and style reference.
* Import a session JSON later.

> Session files do not contain TensorFlow model weights. Use **Save Arch** separately for model export.

### Export and persistence

* Save generated patterns as PNG images.
* Save TensorFlow.js model architecture and weights.
* Save matching metadata JSON.
* Load saved model JSON, weights BIN, and metadata JSON.
* Persist UI settings in `localStorage`.
* Reset UI settings when needed.

### Visual styling

* Light and dark themes.
* Responsive three-column studio layout.
* Pixel-art style canvas preview.
* Multiple palette modes:

  * Mono
  * Aurora
  * Plasma
  * Ocean
  * Ember
  * Ink
* Multiple post-processing effects:

  * None
  * Contrast+
  * Dream Bloom
  * Posterize
  * Edge Glow

---

## Demo

Open the HTML file directly in a modern browser.

No build step is required.

```bash
# Example
open quantum_dream_weaver_v4_advanced.html
```

For best performance, use a Chromium-based browser with WebGL enabled.

---

## Requirements

Quantum Dream Weaver v4.0 is designed as a standalone browser app.

Required at runtime:

* A modern browser
* Internet access for CDN dependencies
* WebGL recommended for faster TensorFlow.js execution

External libraries loaded from CDN:

* TensorFlow.js
* Universal Sentence Encoder for TensorFlow.js

---

## Quick Start

1. Download or clone the project.
2. Open `quantum_dream_weaver_v4_advanced.html` in your browser.
3. Choose an image size, latent dimension, palette, and post effect.
4. Optionally enter a text prompt such as:

```text
cosmic flow, ethereal ruins, bioluminescent circuitry
```

5. Click **Start Meta-Exploration**.
6. Like, pin, remix, interpolate, or save any generated pattern you enjoy.

---

## Controls Overview

### Meta-Exploration Control

| Control         | Description                                                       |
| --------------- | ----------------------------------------------------------------- |
| Epochs          | Number of exploration epochs. Use `0` for infinite exploration.   |
| Arch/Epoch      | Number of architecture candidates generated per epoch.            |
| Nuances         | Number of latent variations generated per architecture.           |
| Seed            | Text or number used for reproducible random exploration.          |
| Backend         | TensorFlow.js backend: WebGL, WASM, or CPU.                       |
| Mutation        | Controls how strongly architectures drift or mutate.              |
| Temperature     | Controls variation intensity in sampling and latent perturbation. |
| Style Bias      | Controls how much the style reference influences future search.   |
| Auto-Like Score | Minimum score required for auto-curation.                         |

### Architecture Search Space

| Control                   | Description                                                       |
| ------------------------- | ----------------------------------------------------------------- |
| Min/Max Blocks            | Range for hidden quantum blocks.                                  |
| Min/Max Units             | Range for dense layer width.                                      |
| Min/Max Mod %             | Range for latent modulation units as a percentage of layer width. |
| Residual quantum blocks   | Adds residual pathways around quantum blocks.                     |
| Harmonic final modulation | Adds an extra harmonic modulation head before output.             |

### Pattern Generation

| Control                | Description                                        |
| ---------------------- | -------------------------------------------------- |
| Visual Latent Dim      | Size of the visual latent vector.                  |
| Image Size             | Output image resolution in pixels.                 |
| Palette                | Colour mapping for single-channel output.          |
| Post Effect            | Visual post-processing effect.                     |
| Animation FPS          | Target FPS for long latent animation.              |
| Batch Variations       | Number of outputs created during batch generation. |
| Native RGB output      | Makes the neural generator output RGB directly.    |
| Long latent animation  | Continuously animates latent perturbations.        |
| Short nuance traversal | Animates between first and last nuance in a loop.  |

---

## Keyboard Shortcuts

| Key   | Action                                         |
| ----- | ---------------------------------------------- |
| Space | Generate a new pattern with the current model. |
| L     | Like the current pattern.                      |
| S     | Save the current pattern as PNG.               |
| Esc   | Stop exploration or animation.                 |

---

## Saving and Loading Models

### Save architecture

Click **Save Arch** to export:

* TensorFlow.js model JSON
* TensorFlow.js weights BIN
* Quantum Dream Weaver metadata JSON

The metadata file includes architecture parameters, prompt state, image size, output mode, palette, post effect, seed, generation number, and timestamp.

### Load architecture

Click **Load Arch** and select all required files:

* `model.json`
* `model.weights.bin`
* `model-metadata.json`

The app restores the architecture, metadata, prompt settings, image size, and output settings, then generates a fresh preview.

---

## Session Export vs Model Export

Quantum Dream Weaver has two export systems:

### Session Export

Use **Export Session** to save:

* UI settings
* Seed
* Gallery thumbnails
* Style reference
* Current metadata

This is useful for saving a creative workspace.

### Model Export

Use **Save Arch** to save:

* Actual TensorFlow.js model architecture
* Model weights
* Metadata needed to reload the model

This is required if you want to preserve the generator itself.

---

## Suggested Workflow

1. Start with a small image size such as `64` or `96` for faster exploration.
2. Enter a text prompt if you want semantic direction.
3. Run one or two epochs.
4. Like strong outputs.
5. Set the best output as a style reference.
6. Increase image size once the style feels promising.
7. Use batch variations to generate a gallery.
8. Save the strongest PNGs.
9. Save the architecture if you want to preserve the generator.
10. Export the session to preserve the creative workspace.

---

## Performance Tips

* Use WebGL backend for best performance.
* Keep image size at `64`, `80`, or `96` while exploring.
* Increase image size only when saving final outputs.
* Avoid very large unit counts on slower machines.
* Text conditioning loads Universal Sentence Encoder, which may take time on first use.
* Native RGB output is heavier than palette-mapped mono output.

---

## Project Structure

This project can run as a single HTML file:

```text
quantum-dream-weaver/
├── quantum_dream_weaver_v4_advanced.html
└── README.md
```

No bundler, package manager, build process, or server is required.

---

## Technical Notes

Quantum Dream Weaver v4.0 uses a browser-based neural generator rather than a pre-trained image diffusion model. Each generated pattern comes from an untrained randomly initialized neural network architecture. The creative behaviour comes from:

* Random architecture sampling
* Custom quantum-inspired nonlinear layer modulation
* Latent vector perturbation
* Optional text embedding conditioning
* Search-space drift
* User-guided selection
* Weight admixture
* Palette and post-processing transformations

Because the models are randomly initialized, outputs are abstract, procedural, and exploratory rather than photorealistic.

---

## Browser Compatibility

Recommended:

* Chrome
* Edge
* Brave
* Other modern Chromium browsers

Also expected to work in recent versions of Firefox and Safari, although TensorFlow.js backend support and performance may vary.

---

## Troubleshooting

### The page is slow

Try reducing:

* Image size
* Max units
* Max hidden blocks
* Batch variation count

Also use the WebGL backend if available.

### Text prompts take time to start

The Universal Sentence Encoder model loads the first time a text prompt is used. After loading, prompt embeddings are cached.

### Loading a model fails

Make sure you selected all three saved files:

* Model JSON
* Weights BIN
* Metadata JSON

The metadata file usually ends with `-metadata.json`.

### Admixture fails

Admixture requires both selected models to have matching:

* Architecture
* Input dimension
* Image size
* Output channels
* Weight shapes

Select two compatible models before creating an admixture.

---

## Roadmap Ideas

Potential future upgrades:

* Animated GIF or WebM export
* IndexedDB model library
* Multi-style reference blending
* Prompt interpolation
* WebGPU backend support when available
* Higher-resolution tiled rendering
* Audio-reactive latent modulation
* Evolution tree visualization
* Side-by-side model comparison
* Local dataset-based aesthetic scoring

---

## License

Add your preferred license here.

Example:

```text
MIT License
```

---

## Acknowledgements

Built with:

* TensorFlow.js
* Universal Sentence Encoder
* Browser Canvas API

Quantum Dream Weaver is an experimental creative coding project for neural procedural art, latent exploration, and browser-based generative systems.
