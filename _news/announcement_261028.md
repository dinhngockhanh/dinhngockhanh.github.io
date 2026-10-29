---
layout: post
title: Yanjie and Khanh led an IICD workshop on inferring clonality from DNA-sequencing data. The materials are freely available!
date: 2026-10-28 09:00:00-0500
inline: false
related_posts: false
---

Khanh and Yanjie led the <a href="https://cancerdynamics.columbia.edu/events/iicd-workshop-series-inferring-cancer-clonality-dna">IICD Inferring Clonality Workshop</a>, where we discussed in detail the important metrics for inferring mutations, copy number variants and clonality from DNA-sequencing data.
We described and implemented popular clustering methods such as [PhyloWGS](https://doi.org/10.1186/s13059-015-0602-8), [PyClone-VI](https://doi.org/10.1186/s12859-020-03919-2) and [SciClone](https://doi.org/10.1371/journal.pcbi.1003665).
We discussed the role of tail mutations, and the impact of coverage distribution and mutation filtering on the tail and cluster distributions.
We then examined [MOBSTER](https://doi.org/10.1038/s41588-020-0675-5) and our recently introduced [DECODE](https://doi.org/10.64898/2026.06.15.732415), currently the only two available clustering software that account for the tail.
Finally, we reviewed the applications of SciClone, MOBSTER and DECODE to infer clonal evolution in acute myeloid leukemia.

The coding materials for interactive sessions and presentation slides are freely available on our <a href="https://github.com/dinhngockhanh/IICDWorkshopInferringClonality">Github repository</a>. Feel free to contact us for more information!

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/261028_InferringClonality_1.jpeg" title="IICD Parameter Inference" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
