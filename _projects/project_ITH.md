---
layout: page
title: Accurate detection of intra-tumor heterogeneity toward improved patient stratification
description: Computational methods to detect subclonal heterogeneity from DNA-sequencing data, utilizing advances in mathematical modeling and parameter inference
img: assets/img/project_ITH_background.png
importance: 2
# category: work
related_publications: true
---

---

Despite considerable efforts, recent evidence shows that currently available algorithms for estimating intratumor heterogeneity (ITH) [remain](https://doi.org/10.1038/s41587-019-0364-z) [limited](https://doi.org/10.1038/s41587-024-02250-y).
Detection of ITH and subclonal structure often exploits summary statistics of the DNA-sequencing data.
Among the most common statistics is the Site Frequency Spectrum (SFS), which tallies the number of mutations at a given Variant Allele Frequency (VAF).

We examined the expected SFS under two different mathematical frameworks, the Moran model and the branching process {% cite dinh2020statistical %}.
The SFS may consist of one or more mutation clusters, reflecting the overall cancer cell population and any subclones undergoing positive selection.
In addition, studies in population genetics had revealed that neutral mutations arising in all subclones further form a "tail" in the SFS, which most clustering algorithms do not incorporate.
Not considering the tail risks overestimating the subclone count, and thus the cancer sample's ITH.

We found that because the SFS tail mainly consists of mutations at low VAFs, both its shape and mass are particularly sensitive to the DNA-sequencing coverage distribution and the data cleaning process as part of mutation calling.
Therefore, better detection and characterization of the SFS tail requires the incorporation of both factors in the SFS formulation.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_ITH_statsci_1.png" title="Impact of sequencing coverage on SFS" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    SFS simulated from synthetic subclonal evolution (left) under different sequencing coverage assumptions (right).
    Mutations in the SFS tail arise within each subclone (green and blue), whereas mutations in each cluster are present in the MRCA of each subclone (red).
</div>

---

Based on this theoretical work, we developed DECODE (**De**ciphering **C**ancer **O**rigin from **D**NA **E**volution) {% cite chen2026accurate %}, a novel mutation clustering method available as an [R package on Github](https://github.com/dinhngockhanh/DECODE).
Given a DNA-sequencing sample, it first finds 3 distinct filtering strategies based on total and variant read counts (**step 1**) and extracts the empirical SFS under each strategy (**step 2**).
DECODE then infers the decomposition parameters under different clonality assumptions.
For each cluster count, it implements ABC-SMC-RF {% cite dinh2025approximate %} to infer the tail power, each cluster's mean VAF and each component's mutation count, that best fit the first 2 filtered SFS (**step 3**).
It then predicts the SFS under the 3rd filtering strategy, assuming the found parameters (**step 4**).
The Generalized Information Criterion (GIC) then quantifies the goodness of the prediction, against the model's complexity (**step 5**).
DECODE selects models with higher ITH if the GIC decreases (**step 6**), otherwise it finishes (**step 7**) and reports the model with minimum GIC as the parsimonious decomposition of the data (**step 8**).

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_ITH_DECODE_1.png" title="DECODE" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Schematic of DECODE's methodology.
</div>

Implementing the [ICGC-TCGA DREAM](https://doi.org/10.1038/s41587-019-0364-z) testing framework revealed that DECODE ranks among the top across inferring different aspects of clonal heterogeneity, including sample purity, subclone count, subclonal VAFs and mutation counts, and subclonal mutation assignments.
Furthermore, compared to [MOBSTER](https://github.com/caravagnalab/mobster) (currently the only other mutation clustering method that accounts for the SFS tail), DECODE identifies and characterizes the tail more accurately for samples with realistic sequencing depths.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_ITH_DECODE_2.png" title="DECODE" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: overall ranking of DECODE (red) against other algorithms (gray) across different ICGC-TCGA DREAM tests.
    Right: results from three ICGC-TCGA DREAM tests across different synthetic cancer samples.
</div>

To demonstrate DECODE's utility in inferring how cancer evolves, we analyzed paired diagnosis/relapse samples of Acute Myeloid Leukemia from [Shlush et al.](https://doi.org/10.1038/nature22993)
[SciClone](https://github.com/genome/sciclone) detects 4-7 subclones in each patient.
However, its inferred mean VAFs of subclones present at both time points tend to be constant.
The implied clonal equilibrium is biologically unrealistic, given that most patients achieved complete remission.
[MOBSTER](https://github.com/caravagnalab/mobster) detects the tail in only 1/20 samples, likely because the coverage depth is significantly lower than its sensitivity level.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_ITH_DECODE_3.png" title="DECODE" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: SciClone's decomposition of a paired diagnosis/relapse AML sample.
    Middle: SciClone's subclonal VAFs between diagnosis and relapse.
    Right: MOBSTER's decomposition of each diagnosis and relapse sample.
</div>

In contrast, DECODE detects the tail in all samples.
Additionally, the mutation assignments are highly consistent in each patient.
The results indicate that in most cases, AML relapse constitutes a continuation of the clonal evolution already present at diagnosis.
DECODE-inferred tail power is lower at diagnosis compared to relapse in 9/10 patients, implying higher cancer aggression in the latter even without increased clonality.
The dN/dS analysis further confirms that tail mutations are neutral and cluster mutations are positively selected.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_ITH_DECODE_4.png" title="DECODE" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: DECODE's decomposition of each diagnosis and relapse sample.
    Middle: Alluvial diagram of DECODE subclonal assignments for mutations at diagnosis and relapse.
    Right: Comparison of DECODE-inferred tail powers at diagnosis and relapse (top) and dN/dS analysis of mutations assigned to tails and clusters in each patient (bottom).
</div>

When applied to pan-cancer data from [The Cancer Genome Atlas](https://doi.org/10.1038/ng.2764), DECODE's mutation assignments are more consistent between same-patient biological replicates than [SciClone](https://github.com/genome/sciclone).
Its inferred tail powers for same-patient samples are also more in agreement than permuted pairs.
Sample purities estimated based on DECODE's truncal clusters agree with [ASCAT3](https://docs.gdc.cancer.gov/Encyclopedia/pages/ASCAT3/) in 84% of all samples.
Together, these results indicate that DECODE's results are consistent and robust.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_ITH_DECODE_5.png" title="DECODE" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Adjusted Rand indices (ARI) for DECODE's and SciClone's deconvolutions of same-patient biological replicates in TCGA.
    Middle: Differences in DECODE-inferred tail powers among same-patient biological replicates and permuted samples.
    Right: Sample purities estimated by ASCAT3 against those predicted from DECODE-inferred truncal clusters.
</div>

Subdividing each TCGA cohort into low- and high-clonality samples revealed a significant ITH-related hazard ratio in low-grade gliomas (LGG).
The association is even stronger in LGG tumors of grade 3, indicating that DECODE-inferred clonality may provide prognostic information beyond what histology and staging capture in some cancer types.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_ITH_DECODE_6.png" title="DECODE" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Volcano plot summarizing the association between cluster count and overall survival across TCGA cohorts.
    Right: Kaplan–Meier overall survival curves for the TCGA lower-grade glioma (LGG) cohort, comprising all samples (top) or only grade 3 tumors (bottom).
</div>

---

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
