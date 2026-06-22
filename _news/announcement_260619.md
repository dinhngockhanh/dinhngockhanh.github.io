---
layout: post
title: We introduced DECODE, a novel deconvolution method to infer the neutral tail and mutation clusters from DNA-sequencing samples.
date: 2026-06-19 09:00:00-0500
inline: false
related_posts: false
---

We introduced <a href="https://doi.org/10.64898/2026.06.15.732415">DECODE</a> (**De**ciphering **C**ancer **O**rigin from **D**NA **E**volution), a novel tumor deconvolution method that can detect and characterize the neutral tail and mutation clusters in the site frequency spectrum (SFS) from a DNA-sequencing sample.
DECODE can be installed from <a href="https://github.com/dinhngockhanh/DECODE">GitHub</a>.

DECODE applies <a href="https://projecteuclid.org/journals/statistical-science/volume-35/issue-1/Statistical-Inference-for-the-Evolutionary-History-of-Cancer-Genomes/10.1214/19-STS7561.full">our mathematical framework for the SFS</a>, which incorporates corrections for sample-specific sequencing coverage and mutation calling biases to enhance the accuracy of detecting and characterizing the SFS tail and clusters.
To improve the reliability and efficiency, DECODE implements <a href="https://github.com/dinhngockhanh/abcsmcrf">ABC-SMC-DRF</a> to infer the tail and cluster parameters.

On synthetic data, DECODE outperformed existing methods across multiple metrics for intra-tumor heterogeneity (ITH) and accurately detected and characterized the SFS neutral tail, the shape of which reflects the tumor's expansion mode. 
In acute myeloid leukemia, accounting for the tail yielded more parsimonious clonal decompositions that are better aligned with the subclonal dynamics that drive relapse. 
Applied to The Cancer Genome Atlas, DECODE detected a neutral SFS tail in most samples across tumor types and uncovered a clinically meaningful link between ITH and survival in low-grade glioma. 
By jointly inferring clonality and expansion mode, DECODE provides two complementary readouts of tumor evolution from a single sample.