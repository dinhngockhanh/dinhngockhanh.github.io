---
layout: post
title: We introduced DECODE, a novel deconvolution method to infer the neutral tail and mutation clusters from DNA-sequencing samples.
date: 2026-06-19 09:00:00-0500
inline: false
related_posts: false
---

We introduced <a href="https://doi.org/10.64898/2026.06.15.732415">DECODE</a> (**De**ciphering **C**ancer **O**rigin from **D**NA **E**volution), a novel tumor deconvolution method that can detect and characterize the neutral tail and mutation clusters in the site frequency spectrum (SFS) from a DNA-sequencing sample.
DECODE can be installed from <a href="https://github.com/dinhngockhanh/DECODE">GitHub</a>.

DECODE is based on [our mathematical framework for the SFS](https://doi.org/10.1214/19-STS7561), which corrects for sample-specific sequencing coverage and mutation calling biases.
It implements [ABC-SMC-DRF](https://doi.org/10.1007/s11222-025-10748-x), our general likelihood-free inference method available as a stand-alone [R package](https://github.com/dinhngockhanh/abcsmcrf), which incorporates random forests into the framework of sequential Monte Carlo to accurately and efficiently infer the tail and cluster parameters.

On synthetic data, DECODE outperformed existing methods across multiple metrics for intra-tumor heterogeneity (ITH) and accurately detected and characterized the SFS neutral tail, the shape of which reflects the tumor's expansion mode. 
In acute myeloid leukemia, accounting for the tail yielded more parsimonious clonal decompositions that are better aligned with the subclonal dynamics that drive relapse. 
Applied to The Cancer Genome Atlas, DECODE detected a neutral SFS tail in most samples across tumor types and uncovered a clinically meaningful link between ITH and survival in low-grade glioma. 
By jointly inferring clonality and expansion mode, DECODE provides two complementary readouts of tumor evolution from a single sample.