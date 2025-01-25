---
layout: page
title: Chromosomal instability and its impact on selection during cancer development
description: Mathematical and computational methods to extract the occurrence rates and selection coefficients of chromosomal instability from DNA-sequencing data
img: assets/img/project_CIN_inference_background.png
importance: 1
# category: work
related_publications: true
---

---

Cancer evolution has been studied extensively as a process of accumulating point mutations, which affect one or a few nucleotides at specific locations in the genome.
However, some cancers have been known to be driven mostly by copy number aberrations (CNAs).
These events can be inferred by examining the total and allele-specific copy numbers across the cancer genome.
Chromosomal instability (CIN) is said to occur when a tumor exhibits a high number of CNAs.

Recent developments in single-cell DNA-sequencing have provided an unparalleled view into the diversity and ongoing evolution within a tumor.
Direct Library Development+ (DLP+), developed by the [Sohrab Shah Lab](https://www.mskcc.org/research-areas/labs/sohrab-shah), is capable of producing genomic information for tens of thousands of cells, without bias due to amplification or non-uniform coverage {% cite laks2019clonal %}.
Using DLP+, researchers have uncovered varying levels of CIN in different cancers, both between patients with the same tumor characteristic and across different cancer types.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_CIN_inference_DLP_1.png" title="DLP+ pipeline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    DLP+ {% cite laks2019clonal %} provides copy number (CN) information at the cell level.  
    Left: Overview of DLP+ experimental and computational pipeline.  
    Right: Total copy numbers (top) and minor allele fractions (bottom) across the genome in one cell from an ovarian tumor.
</div>

By grouping cells with similar copy numbers into clones and tracking them over time, DLP+ data provides a picture of competition between different clones.
In some experiments, some clones were observed expanding through time, while others became extinct.
This indicates that selection plays an important role during tumor growth, and certain CNAs are preferred over others as cancer progresses {% cite salehi2021clonal %}.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_CIN_inference_DLP_2.png" title="DLP+ signatures" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Evolution of clones with distinct copy numbers from a triple-negative breast tumor over time {% cite salehi2021clonal %}.  
    Left: Phylogeny of cells based on their copy number profiles. Cells with similar copy numbers are grouped into a clone.  
    Right: Temporal trajectory of clonal fractions in the cell population (= number of cells in the clone, divided by number of cells in total).
</div>

Furthermore, applications of DLP+ have led to the realization that knock-outs of certain important genes, such as TP53 and BRCA1/2 in the mammary epithelium, are associated with a significant increase in CIN {% cite funnell2022single %}.
This manifests in higher number of polyploid cells (resulting from whole-genome duplications) and more chromosome missegregations.
These results explain the high numbers of CNAs that have been observed in ovarian and breast cancers.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_CIN_inference_DLP_3.png" title="DLP+ signatures" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Copy number changes associated with key genes being turned off in mammary epithelial cell lines {% cite funnell2022single %}.  
    Top: Total and allele-specific copy numbers in cells with TP53 knocked out (left) and both TP53 and BRCA1 knocked out (right).  
    Bottom: Statistics of cell populations, depending on whether TP53, BRCA1 or BRCA2 are knocked out.
</div>

---

We seek to systematically study how CIN arises and affects the selection landscape during tumor growth.
This requires a mathematical framework that incorporates different CNA mechanisms that occur during CIN.
We developed CINner, a simulation method to analyze
how CIN arises and affects the selection landscape during cancer growth {% cite dinh2024cinner %}.
CINner, available as an [R package on Github](https://github.com/dinhngockhanh/CINner),
is designed to efficiently model a cell population undergoing different types of CNAs and mutations,
which change the cell karyotypes and increase the clonal diversity.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project_CIN_inference_CINner_1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Mathematical model underlying CINner.
</div>

CINner currently supports different CNA mechanisms, including whole-genome duplications,
whole-chromosome and chromosome-arm missegregations, focal amplifications and deletions.
We included three different selection models, 
designed to model the fitness of chromosome-arm level CNAs or driver mutations, or both.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project_CIN_inference_CINner_2.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Schematics for the selection model of chromosome arms (left) and driver mutations (right).
</div>

When applied to whole genome sequencing data across all cancers in The Cancer Genome Atlas (TCGA),
CINner inferred selection parameters for individual chromosome arms.
These selection parameters strongly correlate with the gene imbalance on each arm from [Davoli et al.](https://www.cell.com/fulltext/S0092-8674(13)01287-7),
indicating that selection rates inferred from CINner are estimates for the combined effects of genes located on different genomic regions.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project_CIN_inference_CINner_3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Top: Schematic for the inference and analysis of cancer type-specific chromosome-arm selection parameters.
    Bottom: Comparison of selection rates inferred by CINner (x axis) from pan-cancer TCGA data, against gene balance score (y axis).
</div>

The same inference routine can be applied for individual cancer types, for which CINner finds selection parameters that faithfully recreate the copy number landscapes observed in data.
These parameters are inferred using samples without whole-genome duplication (WGD), from which chromosome arms can be classified as GAIN (if the selection rate > 1, hence gains of these arms are advantageous) or LOSS (if the selection rate < 1, in which case losses increase cell fitness).
The count and mean selection rate across these inferred GAIN and LOSS arms predict cancer-specific WGD prevalence well.
On the one hand, this confirms that WGD is an important event that remolds the selection landscape during cancer development, as has been observed experimentally.
On the other hand, this reconfirms CINner's ability to uncover biologically relevant parameters from sample cohorts of relatively small sizes.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project_CIN_inference_CINner_4.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Top: Comparison between gain/loss frequencies from data and CINner with inferred selection rates, for ovary adenocarcinoma.
    Bottom: Correlation between cancer-specific WGD proportion and count of GAIN arms (left) and mean selection rate of LOSS arms (right).
</div>

---

---

{% cite xiang2024inference %}

{% cite dinh2024approximate %}

{% cite mcpherson2024ongoing %}




<!-- The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
``` -->

{% endraw %}
