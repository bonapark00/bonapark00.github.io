---
layout: page
title: "LB-Edit: Look Before You Edit"
description: Attention-Guided Camera Placement and Multi-View Alignment for 3D Gaussian Splatting Editing
importance: 1
category: research
related_publications: true
---

**Authors:** Jaeyeon Park, Taeho Kang, Youngki Lee  
**Status:** Under Review (arXiv 2607.19777, Apr 2026)

---

## Overview

Text-driven 3D scene editing with 3D Gaussian Splatting (3DGS) typically applies a 2D diffusion editor to views rendered from fixed training cameras. This limits both the spatial coverage of edits and the user's ability to target specific objects in complex scenes.

We present **LB-Edit**, a framework that addresses two coupled problems:
- **Where** to place editing cameras for localized edits
- **How** to make per-view edits agree with one another for 3D consistency

---

## Method

**Attention-Guided Editing Camera Placement (ACP)** probes the diffusion model's self- and cross-attention at multiple candidate camera distances to find where attention is well-contained in the region of interest, then places a compact, geometrically diverse editing camera set at that attention-optimal distance.

**Multi-view Attention Alignment (MAA)** steers the editor toward the same edit across views along two axes:
- *Appearance alignment* via token-level self-attention feature correspondence
- *Spatial alignment* via a shared 3D cross-attention field lifted onto the Gaussians

---

## Results

- Highest user preference in instruction fidelity, multi-view consistency, and editing locality
- Uses as few as **5 editing views**
- Reduces editing latency by up to **7×** over existing methods (GSEditor, VcEdit, DGE)

---

## Links

- [Project Page](https://bonapark00.github.io/lbedit-project-page/)
- [arXiv](https://arxiv.org/abs/2607.19777)
