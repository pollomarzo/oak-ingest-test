# An Interim Dogfood Paper for the Engine Shim

+++ {"part": "abstract"}

This paper exists so the frozen shim can be exercised end-to-end against a live GitHub
repo — the two composite-action behavior spikes ([R18]) can only be pinned with a real
runner. It executes no code (no `paper-environment.yml`), so the micromamba step must be
skipped; only `oak build` runs for real at this stage [@fixture2026].

+++

## Introduction

One trivial section so the build has content to render to HTML and a typst PDF.
