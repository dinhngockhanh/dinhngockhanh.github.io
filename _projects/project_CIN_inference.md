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
We developed CINner, an algorithm to simulate
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
designed to quantify the fitness of chromosome-arm level CNAs or driver mutations, or both.

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
    Bottom: Comparison of selection rates inferred by CINner (x axis) from pan-cancer TCGA data, against gene balance scores (y axis).
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

With CINner, we now have a framework to uncover selection parameters for individual genomic regions.
However, we are also interested in finding the rates at which CNA mechanisms occur, such as chromosome missegregations.
This requires more information than what bulk genomic data can offer.
This is because if a particular CNA is frequently observed in data, it can be explained by a spectrum of parameters in CINner.
On one extreme, it could be because the CNA occurrence is high, therefore the event takes place often across different patients even if it does not significantly impact cancer fitness.
On the other extreme, it could be because the selection rate associated with the CNA event is high, in which case it takes a long time to emerge but always expands across the entire tumor when it does.
The parameters therefore are confounded in bulk data alone.

In {% cite xiang2024inference %}, we developed a parameter inference routine that employs both bulk data and information from single-cell (sc) sequencing, such as DLP+.
The algorithm uses [ABC-rf](https://academic.oup.com/bioinformatics/article/35/10/1720/5132692), an Approximate Bayesian Computation (ABC) method with random forests that produces reliable posterior distributions with high tolerance for noise.
The ABC framework summarizes both data and model simulations with statistics, for which we considered a wide range of measurements based on bulk CN, single-cell CN profiles, and the phylogeny for cells in the single-cell samples.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project_CIN_inference_theory_1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Top: The inference method relies on ABC-rf to find parameter posterior distributions.
    Bottom: Overview of some statistics based on single-cell phylogeny (left) and distance between observed and simulated CN profiles (right).
</div>

Using this framework, we are able to uncover the true values of both the missegregation probability and the selection parameters for individual chromosomes.
This comparison was performed with synthetic tests, where we know the true values against which the parameter posterior distributions can be compared.
The posterior distributions are unimodal, which indicates identifiability, and center around the ground truth values.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project_CIN_inference_theory_2.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Inference of missegregation probability (top left) and selection parameters for individual chromosomes in synthetic testing.
    For each parameter, the posterior distribution (dark blue; broken lines indicate mean, median and mode) is inferred from a uniform prior distribution (light blue), compared to the ground truth value (black line).
    The inference is accurate if the posterior distribution centers around ground truth value.
</div>

Importantly, the accuracy and uncertainty of the results (quantified as Root mean square error (RMSE) and standard deviation of the posteriors, respectively) do not increase significantly for small sample sizes of either single-cell or bulk cohorts.
Minimum error can be achieved with as few as 40 sc and 50 bulk samples, while minimum uncertainty is reached with 20 and 30 bulk samples.
These requirements are already satisfied with currently available data for some cancer types.
We expect that as DNA sequencing becomes an essential part of cancer diagnosis, our simulation and inference framework will become a pivotal tool to analyze the data toward better understanding of cancer evolution and adaptation.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project_CIN_inference_theory_3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    RMSE and standard deviation of the posterior distributions, as a function of sample size of the single-cell cohort (left) and the bulk data (right)
</div>

---

ABC-rf's insensitivity to noise is essential for incorporating a large number of statistics in our inference method.
It therefore offers an incredible advantage over traditional ABC methods, which require selecting substantially important hyperparameters and therefore are not flexible for such expansive problems and models such as ours.
However, ABC-rf often requires a large training set and therefore long running time.
To improve its performance, we developed Approximate Bayesian Computation sequential Monte Carlo with (distributional) random forests (ABC-SMC-RF) {% cite dinh2024approximate %}.

A tree in the random forest grows from a root node, composed of a subsample or bootstrap sample of the training set.
The algorithm then repeatedly divides each node, each time by choosing a particular statistic and segregating the node's simulations into those whose values are lower or higher than a threshold.
The choice of statistic and threshold at each node is made such that the simulations in each child node are most "similar" to each other, with respect to the given statistic.
Finally, the algorithm traverses each tree with the statistics measured from the data.
Simulations in the same leaf that the data ends up in are deemed closer to the data, hence the parameters of those simulations form an approximation for the posterior distribution.

ABC-SMC-RF incorporates the random forest within the framework of sequential Monte Carlo (SMC).
In SMC, the posterior distribution is improved through successive iterations from the prior distribution.
Each iteration in ABC-SMC-RF samples the parameters from the previous iteration's posterior, perturbs the parameters to maintain parameter diversity, then infers the next posterior distribution with random forest.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project_CIN_inference_abcsmcdrf_1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Schematic for the combination of ABC-SMC-RF and CINner toward inferring parameter posterior distributions.
    Middle: Schematic for constructing a tree in the random forest.
    Right: Schematic for inferring a parameter estimate from the tree.
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
